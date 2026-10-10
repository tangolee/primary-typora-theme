# Primary for Typora

A faithful port of Cecilia May's **Primary** theme for Obsidian to Typora.

Primary is "soft, chewy, comforting" — a warm, paper-like light theme and its  
matching warm charcoal dark theme, with the same typography, the same terracotta  
/ slate-blue / ochre accent language, and the same signature callouts, code  
chips and pill tags.

---
<img width="906" height="1500" alt="screenshot-compare" src="https://github.com/user-attachments/assets/822f7160-bf6b-439c-8c65-7ec884829a29" />


## Installation

1. Copy `primary.css`, `primary-dark.css` **and the `primary-fonts/` folder**  
   into Typora's theme directory:

   | Platform | Path                                          |
   | -------- | --------------------------------------------- |
   | Windows  | `%APPDATA%\typora\themes`                     |
   | macOS    | `~/Library/Application Support/typora/themes` |
   | Linux    | `~/.config/typora/themes`                     |

   The `primary-fonts` folder must sit **next to** the two CSS files — the theme  
   loads every one of its four families from it with a relative path. It is ~27 MB  
   and it is not optional if you want the intended look on a machine that has  
   none of these fonts installed.

2. In Typora open **File → Preferences → Appearance → Themes** and pick  
   **Primary**. Enable **Appearance → Themes → Dark mode** (or *Follow system*)  
   to get `primary-dark.css`.

3. Recommended Typora settings for the intended look:

   - **Appearance** — *Unibody* or *Minimal* window style.
   - **Markdown → Syntax support → Math / Diagrams** on, for the math styling.
   - **Appearance → Open Theme Folder** is the fastest way to install by hand.

> **No fonts need to be installed.** Inter, HarmonyOS Sans SC, Maple Mono NF CN  
> and Cascadia Code all ship in `primary-fonts/`. Each `@font-face` lists  
> `local()` *before* the file, so an installed copy is used and the bundled one  
> is never read — the files only kick in where they are actually needed.

> A ready-made demo is bundled: open `demo/primary-demo.md` with the theme  
> selected to see every element in one page, or open `dist/preview-light.html` /  
> `dist/preview-dark.html` in any browser for the same page without Typora.  
> Flat screenshots live at `dist/screenshot-light.png`, `dist/screenshot-dark.png`  
> and `dist/screenshot-compare.png`.

---

## What was ported

### Palette

The whole colour system is rebuilt from Primary's own ramps, so nothing is  
approximated:

- **Light** — warm off-white paper (`#FAF4ED`-ish), deep coffee-brown headings,  
  terracotta red as the primary accent.
- **Dark** — warm charcoal (never pure black), coral accents, mellowed tints.
- Both modes share one token set: `--p-bg`, `--p-text`, `--p-text-title`,  
  `--p-accent`, `--p-link`, `--p-code-*`, `--p-callout-*-rgb`, …

### Typography

The theme runs on four families, **all four bundled** in `primary-fonts/` as  
woff2 — nothing has to be installed:

| Role              | Family                   | File                        | Size      | Licence           |
| ----------------- | ------------------------ | --------------------------- | --------- | ----------------- |
| Latin body & UI   | **Inter** (variable)     | `InterVar*.woff2`           | 0.69 MiB  | SIL OFL 1.1       |
| **Chinese (CJK)** | **HarmonyOS Sans SC**    | `HarmonyOS-Sans-SC-*.woff2` | 8.28 MiB  | Huawei font terms |
| **Code**          | **Maple Mono NF CN**     | `MapleMono-NF-CN-*.woff2`   | 18.47 MiB | SIL OFL 1.1       |
| Code fallback     | Cascadia Code (variable) | `CascadiaCode.woff2`        | 0.19 MiB  | SIL OFL 1.1       |

- Inter sits first in the text stack, so Latin, Greek and Cyrillic keep Primary's  
  intended Inter metrics. Everything Inter lacks — i.e. all CJK — falls straight  
  through to **HarmonyOS Sans SC**, so Chinese gets a properly designed face  
  instead of whatever the OS happens to pick.
- Code is **Maple Mono NF CN**, the CN build of Maple Mono. It carries Chinese  
  glyphs inside the same monospace grid at a strict **2 : 1** ratio, so two Latin  
  characters are exactly as wide as one Chinese character. Tables written inside  
  code fences therefore align across both scripts — something the original  
  Cascadia Code cannot do, as it has no CJK coverage at all.
- Headings are semibold (650) in warm deep brown, with generous breathing room.
- Body line-height is Primary's own relaxed measure.

The two CJK families are the ones that actually matter for portability: every  
system in the world has *some* CJK font, but no two agree on metrics, so without  
a bundled face the same document would look different on every machine. See  
`FONTS.md` for how the files were produced and how to regenerate or drop them.

### Emphasis

| Markup             | Light                              | Dark                 |
| ------------------ | ---------------------------------- | -------------------- |
| `**bold**`         | terracotta red                     | coral                |
| `*italic*`         | slate blue                         | sky                  |
| `***both***`       | near-black                         | near-white           |
| `~~strike~~`       | muted + hairline                   | muted + hairline     |
| `<u>underline</u>` | soft 1.5px underline               | soft 1.5px underline |
| `==mark==`         | three tints: plain / bold / italic | same                 |

### Links

External anchors are Primary red, wiki-style `[[links]]` are ochre, resolved  
links green. Underlines are intentionally soft (≈22 % alpha, 1.5 px).

### Lists

Three-level bullet markers step through clay → terracotta → slate blue. Ordered  
lists use Primary's muted numerals. Task lists get square rounded checkboxes  
that fill with Primary green when checked.

### Callouts

Two routes, both styled to Primary's callout recipe — **tinted header + cream  
body + one soft pixel of shadow** — and neither draws a side rule, because  
Primary's callouts are rounded, fully tinted cards. Typora's built-in stylesheet  
puts a GitHub-style `border-left` bar on native alerts, so the theme cancels it.

**A. Native Typora alerts** (GitHub / Obsidian compatible syntax):

```markdown
> [!NOTE]
> Useful information that users should know, even when skimming.
```

`[!NOTE] [!TIP] [!IMPORTANT] [!WARNING] [!CAUTION]` are all mapped onto  
Primary's own callout colours, with a hue-tinted icon carrying the accent while  
the title stays in text colour.

**B. Full Obsidian set via a raw HTML block.** Primary ships fourteen callout  
colours; Typora's five alerts can't cover them, so the theme also styles  
Obsidian's own markup directly:

```html
<div class="callout" data-callout="question">
  <div class="callout-title">Question · 自定义标题</div>
  <div class="callout-content"><p>Anything works here, including <code>code</code>.</p></div>
</div>
```

Supported `data-callout` values:

`note` · `abstract` `summary` `tldr` · `info` · `todo` · `tip` `hint` ·  
`important` · `success` `check` `done` · `question` `help` `faq` ·  
`warning` `caution` `attention` · `failure` `fail` `missing` ·  
`danger` `error` · `bug` · `example` · `quote` `cite`

> **A note on `caution`.** The two routes follow their own conventions on  
> purpose. In route **B** (Obsidian markup) `caution` aliases `warning`, exactly  
> as in Obsidian. In route **A**, Typora's native `> [!CAUTION]` follows the  
> GitHub semantics it inherits, so it takes Primary's strongest red instead —  
> which also keeps it visually distinct from `> [!WARNING]` sitting right above  
> it.

### Tags

Typora has **no hashtag syntax** — `#tag` is plain text and is not parsed into  
an element, so it cannot be reached by CSS alone. The theme therefore ships the  
pill styling on a small span:

```html
<span class="tag">#primary-features</span>
```

- bare `.tag` — the default neutral pill
- add `.tag-1` / `.tag-2` / `.tag-3` for Primary's three alternating pill  
  tints (yellow / red / blue), exactly as in the original.

### Code

Inline code wears Primary's warm "chip". Fenced code blocks use a warm tinted  
surface with a full syntax palette re-derived from Primary's colour ramp —  
keywords, strings, numbers, comments, functions, properties and punctuation all  
keep the theme's own hues rather than a generic one.

### Tables, rules, misc

- Tables: tinted header row, hairline rules, no heavy grid.
- `<hr>` draws Primary's short centred rule.
- Math (inline + display), footnotes, images and `[TOC]` are all styled.
- YAML front matter renders as a soft raised card.
- Sidebar, outline, file tree, title bar, menus, dialogs, scrollbars, focus mode  
  and print/export are themed too, so the whole app stays coherent.

---

## Customising

Every knob lives in the `:root` block at the top of the CSS file. The most  
useful ones:

```css
:root {
  --p-bg:            /* page background            */
  --p-text:          /* body text                  */
  --p-text-title:    /* headings                   */
  --p-accent:        /* terracotta accent          */
  --p-link:          /* link colour                */
  --p-radius:        /* global corner radius (8px) */
  --p-font-text:     /* body font stack            */
  --p-font-mono:     /* code font stack            */
}
```

Because the two builds share one token set, **editing a token in  
`primary.css` does not change `primary-dark.css`** — change both if you want  
the tweak to follow the mode switch.

### Putting a coloured bar back on callouts

If you prefer GitHub's look over Primary's, the theme deliberately cancels the  
built-in side rule. Append this to the CSS file to restore one:

```css
/* side rule in the callout's own hue */
#write .md-alert,
#write .callout { border-left: 4px solid rgb(var(--callout-rgb, var(--callout-color))); }

/* or, to keep Typora's five GitHub colours instead */
#write .md-alert { border-left: .25em solid #000; }
#write .md-alert.md-alert-note      { border-left-color: #0969da; }
#write .md-alert.md-alert-important { border-left-color: #8250df; }
#write .md-alert.md-alert-warning   { border-left-color: #9a6700; }
#write .md-alert.md-alert-tip       { border-left-color: #1f883d; }
#write .md-alert.md-alert-caution   { border-left-color: #cf222e; }
```

The `#write` prefix is needed so the rule outranks the theme's own `border: none`.

### Optional signature paper texture

At the bottom of the CSS there is an *OPTIONAL* block containing Primary's  
dotted and lined background patterns. Un-comment one of them to turn Typora's  
canvas into Primary's dotted paper.

---

## Building from source

```
src/theme.css           shared rules (contains the /*@@ROOT@@*/ placeholder)
src/palette-light.css   :root block for the light build
src/palette-dark.css    :root block for the dark build
src/fonts/*.woff2       all four families, copied into dist/primary-fonts/

python build.py                     # → dist/primary.css, dist/primary-dark.css
                                    #   also lints for unresolved custom properties
python build.py --install           # …also copies into Typora's themes folder
python dev/pack_system_fonts.py     # rebuild src/fonts/*.woff2 from C:\Windows\Fonts
python dev/verify_fonts.py          # assert the woff2 files match their originals
python dev/make_preview.py          # → dist/preview-light.html / preview-dark.html
python dev/render_demo_md.py        # → dist/preview-demo-{light,dark}.html
python dev/probe_base.py            # asserts Typora's base.css is fully overridden
python dev/probe_theme_fallback.py  # renders the theme with every local() stripped
```

`dev/make_preview.py` inlines the built CSS on top of a pinned copy of the  
rules from Typora's own `base.css` / `base-control.css`, so the theme can be  
eyeballed (and screenshotted) in any browser without launching Typora. That copy  
is **verbatim on purpose**: anything the theme fails to neutralise will show up  
in the preview instead of only appearing inside the app.

`dev/render_demo_md.py` goes one step further and renders `demo/primary-demo.md`  
itself — converting `> [!NOTE]` alerts, `- [x]` task items, `==mark==`, `~~strike~~`  
and `[TOC]` into the exact markup Typora emits — then asserts that every raw HTML  
block in the demo survived the round-trip. It exits non-zero if anything was  
swallowed, so it doubles as a regression test for the demo.

`dev/probe_base.py` is the guard for the layering itself. It renders the built  
theme over those pinned base rules and reads back **computed** styles, failing if  
a property still carries the base value — i.e. if the theme lost the cascade.  
Two real bugs shipped before it existed, both from base rules being silently  
inherited:

| Symptom                                         | Cause in Typora's `base.css`                                 | Fix                               |
| ----------------------------------------------- | ------------------------------------------------------------ | --------------------------------- |
| Coloured rule on the left edge of every callout | `.md-alert { border-left: .25em solid #000 }` plus a per-type `border-left-color` | `border: none` on `.md-alert`     |
| Task-list checkboxes collapsed to a 1px speck   | `#write input[type=checkbox] { width: inherit; height: inherit }` — an **ID** selector that outranks any class rule, and with `appearance: none` an `auto` replaced element has zero intrinsic size | `#write`-prefixed checkbox sizing |

The two mechanics worth remembering when extending the theme: a rule in  
`base.css` that uses an ID selector can only be beaten by matching or exceeding  
that ID, and any property the theme never mentions simply passes through.

### Verifying the bundled fonts

`local()` sitting before `url()` in every `@font-face` means that on a machine  
where the fonts *are* installed, the bundled files are never read — so a  
truncated or corrupted woff2 would go unnoticed during development and only  
break on the machine the bundling was meant to help. Two checks exist for that:

- `dev/verify_fonts.py` compares each woff2 against the system TTF it came from:  
  table set, glyph count, character coverage, units per em, and **every**  
  horizontal advance width. It also re-asserts the 2 : 1 CJK/Latin grid.
- `dev/probe_bundled_fonts.html` loads the files in Chromium with `url()` only —  
  no `local()` — and checks that each face reaches `loaded`, that the rendered  
  pixels match the installed font, and that a deliberately broken URL reaches  
  `error` (without that negative control a "loaded" verdict would prove nothing).
- `dev/probe_theme_fallback.py` is the end-to-end version: it strips *every*  
  `local()` out of the built `dist/primary.css` and renders the result, which is  
  exactly what a machine with none of these fonts installed sees. It passes only  
  if the theme's own `--p-font-text` / `--p-font-mono` stacks land on the bundled  
  files and not on a system fallback.

Run them with:

```
python dev/verify_fonts.py
python dev/probe_theme_fallback.py

"C:/Program Files/Google/Chrome/Application/chrome.exe" --headless=new \
  --virtual-time-budget=30000 --dump-dom dev/probe_bundled_fonts.html
```

One gotcha these checks exist for: dropping a "web-useless" table while  
re-compressing is the obvious optimisation, but `gasp` steers rasterisation —  
without it the bundled Maple Mono rendered ~0.2 % differently from the installed  
font. That is why the pack script is a *pure* re-containerisation, and why  
`verify_fonts.py` compares the table set before anything else.

---

## Licence

The original Primary theme is released under the **GNU General Public License  
v3.0** (`LICENSE` in the upstream repository). This Typora port is a derivative  
work — it reuses Primary's design and colour ramps — so it is released under the  
**same GPL-3.0 licence**. A copy is included as `LICENSE`.

Practically, for a theme that means: use it, modify it, share it freely — but if  
you redistribute a modified version, it must stay under the GPL-3.0 as well.

The bundled fonts are a separate matter:

| Font              | Licence                                                      | Bundling                            |
| ----------------- | ------------------------------------------------------------ | ----------------------------------- |
| Inter             | SIL OFL 1.1                                                  | permitted, redistributed unmodified |
| Cascadia Code     | SIL OFL 1.1                                                  | permitted, redistributed unmodified |
| Maple Mono NF CN  | SIL OFL 1.1                                                  | permitted, redistributed unmodified |
| HarmonyOS Sans SC | Huawei's own font terms (free to use, including commercially) | see the caveat below                |

**Read `FONTS.md` before redistributing this theme publicly.** It lists where  
each file came from, and flags the one family whose terms are not the OFL.

## Credits

- Original theme: **[Primary](https://github.com/primary-theme/obsidian)** by  
  Cecilia May — winner of Obsidian October 2021's Best Theme. All design credit  
  belongs there. The port would not exist without it.
- Fonts bundled with this port, all redistributed unmodified:
  **Inter** by Rasmus Andersson, **Cascadia Code** by Microsoft and
  **Maple Mono NF CN** by subframe7536 (all SIL OFL 1.1), plus
  **HarmonyOS Sans SC** by Huawei. See `FONTS.md`.
- The Obsidian→Typora selector mapping, both palettes, the alert/callout bridges,  
  the font packaging/verification tooling and the demo/preview harness in this  
  repository are original work.
