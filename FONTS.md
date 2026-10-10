# Fonts — what the theme uses and how it stays portable

The theme uses **four families**, and all four ship inside `primary-fonts/` as
`woff2`. Nothing needs to be installed for the theme to look the way it was
designed to look.

| Role | Family | Files | Faces | Size | Licence |
| --- | --- | --- | --- | --- | --- |
| Latin body & UI | **Inter** (variable) | `InterVar.woff2`, `InterVar-Italic.woff2` | roman + italic, 100–900 | 0.69 MiB | SIL OFL 1.1 |
| Chinese (CJK) | **HarmonyOS Sans SC** | `HarmonyOS-Sans-SC-Regular.woff2`, `-Bold.woff2` | 400 + 700 | 8.28 MiB | Huawei font terms — see §5 |
| Code | **Maple Mono NF CN** | `MapleMono-NF-CN-{Regular,Bold,Italic}.woff2` | 400 + 700 + italic | 18.47 MiB | SIL OFL 1.1 |
| Code fallback | Cascadia Code (variable) | `CascadiaCode.woff2` | 200–700 | 0.19 MiB | SIL OFL 1.1 |

Total: **27.6 MiB**, in eight files, next to the two CSS files.

---

## 1. How a face gets chosen

Every `@font-face` in `primary.css` / `primary-dark.css` puts `local()` **before**
the file:

```css
@font-face {
  font-family: "HarmonyOS Sans SC";
  font-weight: 400;
  src: local("HarmonyOS Sans SC"),                       /* installed? use it */
       local("HarmonyOS_Sans_SC"),                       /* …or by PostScript name */
       url("./primary-fonts/HarmonyOS-Sans-SC-Regular.woff2") format("woff2");
}
```

That ordering gives one stylesheet two behaviours:

| The machine | What happens | Cost |
| --- | --- | --- |
| has the font installed | `local()` matches, the bundled file is **never read** | zero |
| does not have it | the browser reads the bundled file | one local file read |

Nothing is downloaded and nothing is installed — this is a desktop app reading a
file next to the stylesheet. The `local()` branch exists purely so a machine that
*does* have the font never pays for it.

Browsers only fetch a font when a glyph actually needs it, so a document with no
Chinese in it never reads the 8.28 MiB CJK pair at all. (The code face is
different: Maple Mono NF CN is first in `--p-font-mono`, so it *is* read
wherever a code fence appears, Latin or not.)

### What is still system-dependent

Nothing that affects layout. The stacks keep their system families as a second
layer, but those are only reached for glyphs the bundled fonts have no design
for:

```css
--p-font-text: "Inter", "HarmonyOS Sans SC", -apple-system, …, "PingFang SC",
               "Hiragino Sans GB", "Microsoft YaHei", …, sans-serif;
--p-font-mono: "Maple Mono NF CN", "Maple Mono NF", "Cascadia Code", …, monospace;
```

So emoji come from whatever the OS has (none of these fonts carry emoji), and a
rare CJK ideograph that HarmonyOS Sans SC happens not to cover falls through to
PingFang SC / Microsoft YaHei rather than showing a tofu box.

---

## 2. Why these two CJK families

Every machine already has *some* CJK font, so the point of bundling is not that
Chinese would otherwise be invisible — it is that no two systems agree on
metrics, so the same document reflows differently on every machine. These two
are the families the look was designed around.

**HarmonyOS Sans SC** sits second in `--p-font-text`, right behind Inter. Inter
covers Latin / Greek / Cyrillic, and everything it lacks — i.e. all CJK — falls
through to HarmonyOS. Behind Inter rather than in front of it means Latin keeps
Primary's intended Inter metrics while Chinese gets a designed face instead of
the OS default. To make HarmonyOS drive the Latin text too, swap the first two
families.

**Maple Mono NF CN** is the *CN* build of Maple Mono: it carries Chinese glyphs
inside the same monospace grid as the Latin, at a strict **2 : 1** ratio — two
Latin advances equal one Chinese advance.

```
latin advance 600 / CJK advance 1200  →  ratio 2.000
4 × "M" = 76.80px      2 × "中" = 76.80px
```

That is what makes tables written inside code fences line up across both
scripts, which the bundled `Cascadia Code` cannot do at all — it has no CJK
coverage, so Chinese would drop out of the grid onto whatever the OS picked.
The italic face is a real italic design, not a slant, and the theme italicises
code comments, which is why it is bundled too.

### Family structure, as the OS reports it

Worth knowing before you edit a stack:

* **`HarmonyOS Sans SC`** — Regular and Bold are linked into this one family, so
  `font-weight: 400` / `700` resolve against it. `Light`, `Medium`, `Thin` and
  `Black` are registered as **separate families** (`HarmonyOS Sans SC Light`, …),
  so asking for `font-weight: 300` does *not* reach Light — it synthesises or
  falls back. There is no italic design at all; italic Chinese is synthesised by
  the browser.
* **`Maple Mono NF CN`** — Regular, Bold and Italic are linked into this family.
  `Thin` … `ExtraBold` are separate families.

---

## 3. How the files were produced

```
python dev/pack_system_fonts.py --font-dir "C:/Windows/Fonts"
python dev/pack_system_fonts.py --report      # sizes only, no conversion
```

The script reads the TTFs and re-containers them as `woff2`. It is a **pure
re-containerisation: no table is added, removed or modified.**

That is deliberate, and it is the one non-obvious thing in this repository.
Stripping "web-useless" tables is the obvious optimisation, but `gasp` is not
one of them — it tells the rasteriser which ppem sizes get grid-fitting and
which anti-aliasing to use. Measured, with everything else identical:

| Maple Mono NF CN Regular | vs the installed font |
| --- | --- |
| `gasp` dropped | ~0.2 % of ink coverage differs |
| `gasp` kept | 0.000 % — pixel-identical |

`DSIG` is the one table that does disappear, and the WOFF spec requires it:
it is a signature over the original sfnt bytes, meaningless once the container
changes, so fontTools removes it on save.

| Source (`C:\Windows\Fonts`) | Output (`src/fonts`) | Source | → woff2 |
| --- | --- | --- | --- |
| `HarmonyOS_Sans_SC_Regular.ttf` | `HarmonyOS-Sans-SC-Regular.woff2` | 7.88 MiB | 4.08 MiB |
| `HarmonyOS_Sans_SC_Bold.ttf` | `HarmonyOS-Sans-SC-Bold.woff2` | 7.78 MiB | 4.20 MiB |
| `MapleMono-NF-CN-Regular.ttf` | `MapleMono-NF-CN-Regular.woff2` | 19.61 MiB | 5.96 MiB |
| `MapleMono-NF-CN-Bold.ttf` | `MapleMono-NF-CN-Bold.woff2` | 19.57 MiB | 6.07 MiB |
| `MapleMono-NF-CN-Italic.ttf` | `MapleMono-NF-CN-Italic.woff2` | 20.30 MiB | 6.43 MiB |
| | **total** | **75.14 MiB** | **26.75 MiB** (36 %) |

The Inter and Cascadia files were not produced here: they were extracted
verbatim from the original Primary theme repository (`src/css/fonts/`), where
they are embedded as base64 `data:` URIs.

---

## 4. How the packaging is verified

There is a trap in the `local()`-first design worth being explicit about: **on a
machine where the fonts are installed, the bundled files are never read.** A
truncated or corrupted `woff2` would therefore look perfectly fine during
development and only break on the machine the bundling was meant to help. Three
checks exist for that reason. All three pass.

**`python dev/verify_fonts.py`** — compares each `woff2` against the system TTF
it came from:

```
HarmonyOS-Sans-SC-Regular.woff2   29221 glyphs ·  29063 codepoints · 58126 widths compared · OK
HarmonyOS-Sans-SC-Bold.woff2      29221 glyphs ·  29063 codepoints · 58126 widths compared · OK
MapleMono-NF-CN-Regular.woff2     33637 glyphs ·  33091 codepoints · 59292 widths compared · OK
MapleMono-NF-CN-Bold.woff2        33637 glyphs ·  33091 codepoints · 59292 widths compared · OK
MapleMono-NF-CN-Italic.woff2      33760 glyphs ·  33092 codepoints · 59294 widths compared · OK

MapleMono-NF-CN-Regular.woff2    latin 600 · CJK 1200 · ratio 2.000 OK
MapleMono-NF-CN-Bold.woff2       latin 600 · CJK 1200 · ratio 2.000 OK
```

Table set, glyph count, character coverage, units per em and **every** horizontal
advance width are compared, plus the 2 : 1 grid. The `MUST_HAVE` list doubles as
a "was the right build bundled" check: the CJK codepoints only exist in Maple
Mono's *CN* build and the `U+E0B0` / `U+F015` codepoints only in the *NF* build.

**`dev/probe_bundled_fonts.html`** — loads the files in Chromium with `url()`
only, no `local()`, so nothing can short-circuit:

```
── 1 · can the browser decode the bundled files
  32px "Probe CJK" / bold / "Probe Mono" regular+bold+italic   status=loaded
  negative control (bad url)                                   status=error (as expected)
── 2 · rendering matches the installed font
  CJK regular   vs installed 0.000%   vs fallback 43.4%
  CJK bold      vs installed 0.000%   vs fallback 33.0%
  mono regular  vs installed 0.000%   vs fallback 78.0%
  mono bold     vs installed 0.000%   vs fallback 69.4%
  mono italic   vs installed 0.000%   vs fallback 79.5%
── 3 · 2:1 grid   4 latin = 2 CJK  76.80px = 76.80px   ratio 1.0000
RESULT 12/12 ALL PASS
```

The negative control matters: without a face that is *expected* to reach
`error`, a "loaded" verdict proves nothing about the status check itself. Advance
widths are useless for this on CJK — every CJK font advances exactly 1em — so
the comparison is over anti-aliased ink coverage instead, where a font that
silently fell back shows up as a 30–80 % difference.

**`python dev/probe_theme_fallback.py`** — the end-to-end version. It takes
`dist/primary.css`, strips *every* `local()` out of it (10 of them across 8
faces), and renders the result. That page is exactly what a machine with none of
these fonts installed sees:

```
face status without any local():  HarmonyOS Sans SC loaded · Maple Mono NF CN loaded
body text:  CJK via --p-font-text   theme=619132 ref=619132 os-fallback=431740  PASS
code:       code via --p-font-mono  theme=596812 ref=596812 os-fallback=335243  PASS
RESULT 2/2 ALL PASS
```

`ref` is a separate face pointing straight at the same file by url only, so the
test is self-contained: the theme's own stack lands on the bundled file, and
provably not on a system font.

---

## 5. Licences

Two different situations, and only one of them is the OFL.

| Font | Licence | Bundled here |
| --- | --- | --- |
| **Inter** — Rasmus Andersson | SIL OFL 1.1 | yes, unmodified |
| **Cascadia Code** — Microsoft | SIL OFL 1.1 | yes, unmodified |
| **Maple Mono NF CN** — subframe7536 | SIL OFL 1.1 | yes, unmodified |
| **HarmonyOS Sans SC** — Huawei | Huawei's own font terms | yes, unmodified |

Under the OFL, all three of the first group may be redistributed unmodified
alongside this theme. The terms that apply:

* Redistribution **unmodified** is permitted, bundled with a larger work.
* The fonts may **not be sold on their own**.
* Any **modified** version must itself be released under the OFL and must not
  use the reserved font names. This port does not modify them.
* The licence notice must travel with the fonts — so keep `FONTS.md` and the CSS
  together when you redistribute the theme.

**HarmonyOS Sans SC is the exception.** It is free to download and use, including
commercially, under Huawei's own font terms — but those terms are *not* the OFL
and they are not reproduced here. Before redistributing this theme publicly,
read Huawei's terms for the font on their developer site and satisfy yourself
that bundling the file is permitted. If you would rather not take that on, drop
the two files — see below. The theme degrades cleanly: Chinese then comes from
whichever CJK font the machine already has.

---

## 6. Changing, dropping or adding fonts

### Dropping a bundled font

Delete the file(s) from **both** `src/fonts/` and `primary-fonts/`. The matching
`local()` / `url()` pair in the `@font-face` rule then simply has no url left to
match, and the stack falls through to the next family — which is what the
`local()` entry is for. `build.py` will warn if an `@font-face` points at a file
that is not there, so run it after deleting to catch a half-done job:

```
! fonts: @font-face points at a file that is not in src/fonts/: X.woff2
```

To keep the look but lose the weight, the CJK pair is the one worth cutting;
Chinese then falls back to `Microsoft YaHei` / `PingFang SC` and the code face's
CJK drops out of the 2 : 1 grid.

### Using different fonts

Both stacks are plain custom properties at the top of the `:root` block, in
**both** `primary.css` and `primary-dark.css`:

```css
:root {
  --p-font-text: "Inter", "HarmonyOS Sans SC", …;
  --p-font-mono: "Maple Mono NF CN", "Maple Mono NF", "Cascadia Code", …;
}
```

Edit them in `src/palette-light.css` and `src/palette-dark.css` and rebuild, or
edit the two `dist` / installed CSS files directly if you are not using the build
script. Typora picks the change up on the next file switch or restart.

### Adding another bundled family

1. Drop the `woff2` into `src/fonts/`.
2. Add a matching `@font-face` in the `00 · Fonts` section of `src/theme.css`,
   with `local()` first and `url("./primary-fonts/…")` second.
3. Put its family name into `--p-font-text` or `--p-font-mono`.
4. `python build.py` — it fails if the rule and the files disagree, and
   `dev/verify_fonts.py` will pick up the new pair if you add it to `PAIRS`.
