<div align="center">

**English** &nbsp;·&nbsp; [简体中文](README.zh-CN.md)

# Primary for Typora

**A faithful port of [Primary](https://github.com/primary-theme/obsidian) — Cecilia May's warm, paper-and-terracotta Obsidian theme — to Typora.**

Same palette, same typography, same signature callouts, code chips and pill tags. The fonts ship with it, so a document looks the same on a machine that has none of them installed.

![License](https://img.shields.io/badge/license-GPL--3.0-blue.svg)
![Typora](https://img.shields.io/badge/Typora-1.x-4d4d4d.svg)
![Fonts](https://img.shields.io/badge/fonts-4%20families%20bundled-2e7d32.svg)
[![Download](https://img.shields.io/badge/download-zip-2ea44f.svg)](https://github.com/tangolee/primary-typora-theme/releases/latest)

[Install](#install) · [Screenshots](#screenshots) · [What the theme covers](#what-the-theme-covers) · [Caret animation](#caret-animation) · [Background patterns](#background-patterns) · [Customising](#customising) · [Fonts](#fonts) · [Repository layout](#repository-layout) · [Compatibility](#compatibility) · [Licence](#licence)

![Primary for Typora — the demo document in light mode (left) and dark mode (right)](docs/screenshot-hero.png)

</div>

---

## Install

### 1 · Get the files

**The release download is the short path:** [primary-typora-theme.zip](https://github.com/tangolee/primary-typora-theme/releases/latest/download/primary-typora-theme.zip) — the six CSS files and `primary-fonts/`, 27.8 MiB, and nothing else. Unzip and it is ready to drop in.

| Option               | How                                                                                                                                                               |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Download the ZIP** | [primary-typora-theme-main.zip](https://github.com/tangolee/primary-typora-theme/archive/refs/heads/main.zip) — the whole theme, fonts, demo and previews, ~30 MB |
| **Clone**            | `git clone https://github.com/tangolee/primary-typora-theme.git`                                                                                                  |

### 2 · Drop them into Typora's theme folder

Copy the six CSS files and `primary-fonts/` into:

| Platform | Theme folder                                  |
| -------- | --------------------------------------------- |
| Windows  | `%APPDATA%\typora\themes`                     |
| macOS    | `~/Library/Application Support/typora/themes` |
| Linux    | `~/.config/typora/themes`                     |

The quickest route is **File → Preferences → Appearance → Open Theme Folder**, then paste them in.

| Item                                                       | What it is                                                    |
| ---------------------------------------------------------- | ------------------------------------------------------------- |
| `primary.css` · `primary-dark.css`                         | the theme itself                                              |
| `primary-fonts/`                                           | the bundled fonts — eight woff2 files                         |
| `primary-dots.css` · `primary-dots-dark.css`               | the theme **plus** Primary's dotted paper                     |
| `primary-grid.css` · `primary-grid-dark.css`               | the theme **plus** Primary's lined paper                      |
| `primary-LICENSE.txt` · `primary-FONTS.md`                 | provenance — GPL-3.0, and the fonts' own terms; optional      |

The last four are the optional paper texture and are ~2 KB each — skip them if you don't want one, keep them if you might. See [Background patterns](#background-patterns).

> `primary-fonts/` has to sit **next to** the CSS files. That is where the relative `url()`s point. Leave it out and the theme still works, but Chinese and code fall back to whatever the system happens to have — which is exactly the inconsistency the bundled fonts exist to remove.

### 3 · Switch it on

**File → Preferences → Appearance → Themes → Theme → Primary.** Typora labels a theme with its file name, hyphens turned into spaces, so the six files above appear as **Primary**, **Primary Dark**, **Primary Dots**, **Primary Dots Dark**, **Primary Grid** and **Primary Grid Dark**.

Typora does **not** pair `X` with `X-dark` on its own. To get the dark build, tick **Use separate theme in dark mode** and set **Dark Theme → Primary Dark**; from then on Typora swaps between the two as the system colour scheme changes. Leave the box unticked and the one theme you picked is used in both modes.

Recommended settings for the intended look:

- **Appearance** — the default *Unibody*, or *Minimal* window style.
- **Markdown → Syntax support** — leave *Math* and *Diagrams* on so the maths styling applies.

### Updating or removing

- **Update** — replace all six CSS files. The font folder only changes when the fonts themselves do.
- **Remove** — delete the six CSS files and `primary-fonts/`, then pick another theme. An unused theme file does nothing, so there is no harm in leaving the pattern themes where they are.

---

## Screenshots

Both builds share one token set, so the two are the same design in two temperatures — warm off-white paper, or warm charcoal.

<details>

<summary><b>Full-page screenshots</b> (light · dark · side by side)</summary>

  


**Light** — `docs/screenshot-light.png`

![The full demo document in light mode](docs/screenshot-light.png)

**Dark** — `docs/screenshot-dark.png`

![The full demo document in dark mode](docs/screenshot-dark.png)

**Side by side** — `docs/screenshot-compare.png`

![Light and dark, side by side](docs/screenshot-compare.png)

</details>

### Preview it without installing

These pages open in any browser and are fully self-contained — the CSS is inlined and the fonts are read from `primary-fonts/`:

| File                                                 | What it shows                                                  |
| ---------------------------------------------------- | -------------------------------------------------------------- |
| `docs/preview-light.html` · `docs/preview-dark.html`           | every element at a glance                                      |
| `docs/preview-demo-light.html` · `docs/preview-demo-dark.html` | the bundled demo document, rendered                            |
| `docs/probe-fallback.html`                                | an A/B page proving the bundled fonts match the installed ones |

> **One caveat about the previews.** Typora strips `class`, `id` and `data-*` from raw HTML while rendering, then restores them on export. These pages are built to match the **exported / printed** result, so the Obsidian-style callouts below appear styled here and in exported HTML/PDF — but not inside the editor. In the editor, use the `> [!NOTE]` syntax; see [Callouts](#callouts).

---

## What the theme covers

### Palette

The colour system is rebuilt from Primary's own ramps — the warm grey ramp and every named hue, each in four steps plus an alpha tint — so nothing is approximated:

- **Light** — warm off-white paper, deep coffee-brown headings, terracotta red as the accent.
- **Dark** — warm charcoal, never pure black; coral accents, mellowed tints.
- Both builds share one token set: raw ramps (`--p-gray-*`, `--p-red-*`, `--p-blue-*`, …) feeding semantic tokens such as `--p-bg`, `--p-text`, `--p-text-title`, `--p-border`, `--p-link`, `--p-bold`, `--p-italic` and `--p-callout-*-rgb`.

### Typography

The theme runs on four families, **all four bundled** in `primary-fonts/` as woff2 — nothing has to be installed:

| Role              | Family                   | Files                                         | Size      | Licence           |
| ----------------- | ------------------------ | --------------------------------------------- | --------- | ----------------- |
| Latin body & UI   | **Inter** (variable)     | `InterVar.woff2`, `InterVar-Italic.woff2`     | 0.69 MiB  | SIL OFL 1.1       |
| **Chinese (CJK)** | **HarmonyOS Sans SC**    | `HarmonyOS-Sans-SC-{Regular,Bold}.woff2`      | 8.28 MiB  | Huawei font terms |
| **Code**          | **Maple Mono NF CN**     | `MapleMono-NF-CN-{Regular,Bold,Italic}.woff2` | 18.47 MiB | SIL OFL 1.1       |
| Code fallback     | Cascadia Code (variable) | `CascadiaCode.woff2`                          | 0.19 MiB  | SIL OFL 1.1       |

- Inter sits first in the text stack, so Latin, Greek and Cyrillic keep Primary's intended Inter metrics. Everything Inter lacks — all of CJK — falls straight through to **HarmonyOS Sans SC**, so Chinese gets a properly designed face instead of whatever the OS happens to pick.
- Code is **Maple Mono NF CN**, the CN build of Maple Mono. It carries Chinese glyphs inside the same monospace grid at a strict **2 : 1** ratio, so two Latin characters are exactly as wide as one Chinese character. Tables written inside code fences therefore line up across both scripts — something the original Cascadia Code cannot do, having no CJK coverage at all.
- Headings are semibold in warm deep brown, with generous breathing room; body line-height is Primary's own relaxed measure.

The two CJK families are the ones that matter for portability: every system in the world has *some* CJK font, but no two agree on metrics, so without a bundled face the same document would look different on every machine. See [Fonts](#fonts).

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

External anchors are Primary red, wiki-style `[[links]]` are ochre, resolved links green. Underlines are intentionally soft (≈22 % alpha, 1.5 px).

### Lists

Three-level bullet markers step through clay → terracotta → slate blue. Ordered lists use Primary's muted numerals. Task lists get square rounded checkboxes that fill with Primary green when checked.

### Callouts

Two routes, both styled to Primary's callout recipe — **tinted header + cream body + one soft pixel of shadow** — and neither draws a side rule, because Primary's callouts are rounded, fully tinted cards. Typora's own stylesheet puts a GitHub-style `border-left` bar on native alerts, so the theme cancels it.

**A. Native Typora alerts** (GitHub- and Obsidian-compatible syntax) — these work in the editor:

```markdown
> [!NOTE]
> Useful information that users should know, even when skimming.
```

`[!NOTE]` `[!TIP]` `[!IMPORTANT]` `[!WARNING]` `[!CAUTION]` are all mapped onto Primary's own callout colours, with a hue-tinted icon carrying the accent while the title stays in text colour.

**B. The full Obsidian set via a raw HTML block.** Primary ships a callout colour for every Obsidian type, and Typora's five alerts cannot cover that, so the theme also styles Obsidian's own markup directly — rounded card, tinted title row, a filled dot in the callout's hue:

```html
<div class="callout" data-callout="question">
  <div class="callout-title">Question · 自定义标题</div>
  <div class="callout-content"><p>Anything works here, including <code>code</code>.</p></div>
</div>
```

> **Editor vs. export.** Typora strips `class`, `id` and `data-*` from user HTML while rendering and restores them on export, so route B applies to **HTML / PDF output only**. Inside the editor, stick to route A.

Supported `data-callout` values:

`note` · `abstract` `summary` `tldr` · `info` · `todo` · `tip` `hint` · `important` · `success` `check` `done` · `question` `help` `faq` · `warning` `caution` `attention` · `failure` `fail` `missing` · `danger` `error` · `bug` · `example` · `quote` `cite`

> **A note on `caution`.** The two routes follow their own conventions on purpose. In route **B** (Obsidian markup) `caution` aliases `warning`, exactly as in Obsidian. In route **A**, Typora's native `> [!CAUTION]` follows the GitHub semantics it inherits, so it takes Primary's strongest red instead — which also keeps it visually distinct from `> [!WARNING]` sitting right above it.

### Tags

Two obstacles have to be routed around here, and it is worth being precise about both.

**Typora has no hashtag syntax.** `#tag` stays plain text — it never becomes an element, so no CSS selector can reach it.

**Typora also strips `class`, `id` and `data-*` from user HTML when rendering.** They survive export, but in the editor they are gone, so `<span class="tag">#tag</span>` renders as a bare, unstyled span. That is why class-based pills appear to do nothing.

The portable way out is a **Markdown link**. Typora builds link DOM itself, so the `href` is always there to select on — point a link at the reserved `#tag` target and it becomes a pill:


```markdown
[#primary-features](#tag)   [#obsidian](#tag-1)   [#warm](#tag-3)
```

| Link target | Pill                     |
| ----------- | ------------------------ |
| `#tag`      | the default neutral pill |
| `#tag-1`    | Primary's yellow tint    |
| `#tag-2`    | Primary's red tint       |
| `#tag-3`    | Primary's blue tint      |

`#tag*` is deliberately not a real heading id, so every tag link is inert — it exists purely as a styling hook. For export targets (HTML, PDF) the class-based form is styled as well:

```html
<span class="tag">#primary-features</span>
<span class="tag tag-1">#yellow-pill</span>
```

### Code

Inline code wears Primary's warm "chip". Fenced code blocks sit on a warm tinted surface with a full syntax palette re-derived from Primary's colour ramp — keywords, strings, numbers, comments, functions, properties and punctuation all keep the theme's own hues instead of a generic one.

### Tables, rules and the rest

- Tables: tinted header row, hairline rules, no heavy grid.
- `<hr>` draws Primary's short centred rule.
- Maths (inline and display), footnotes, images, `[TOC]` and YAML front matter (as a soft raised card) are all styled.
- Sidebar, outline, file tree, title bar, menus, dialogs, scrollbars, focus mode and print/export are themed too, so the whole app stays coherent.

---

## Caret animation

Typora draws its caret two different ways, with wildly different ceilings. The theme does as much as each one allows.

|              | Live-preview body                                                     | Source view, code fences, maths                                                               |
| ------------ | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Drawn by     | the browser's own caret                                               | CodeMirror — a real, absolutely positioned `div.CodeMirror-cursor` painted with `border-left` |
| Tint it      | yes                                                                   | yes                                                                                           |
| Fade it      | yes                                                                   | yes                                                                                           |
| **Slide it** | **no — impossible**                                                   | **yes**                                                                                       |
| Lives in     | section `19 · CARET`, the `@supports (caret-animation: manual)` block | section `19 · CARET`, the `.CodeMirror` block                                                 |

**The live preview cannot have a gliding caret.** The browser owns that caret; `caret-color` is the only property that reaches it, and nothing can move or reshape it. So the theme gives it the one effect CSS can still deliver — a soft fade. Where the engine exposes `caret-animation: manual`, the theme takes the blink away from the engine so the fade is not fighting it; where it does not, the whole block is skipped by `@supports` and Typora's own caret is left untouched.

**Code fences, maths blocks and the source view do glide.** Those run on CodeMirror, where the caret is an ordinary element whose `left` / `top` / `height` CodeMirror rewrites on every keystroke. A `transition` on those turns the jump into a slide — the same trick VSCode-Animations uses.

### Three presets

They differ only in where `--p-caret-fade` points:

| Preset              | `--p-caret-fade`            | Effect                                   |
| ------------------- | --------------------------- | ---------------------------------------- |
| `phase` *(default)* | `transparent`               | the caret fades right out and comes back |
| `breathe`           | `var(--p-caret-color-soft)` | it only dims — never quite disappears    |
| `solid`             | `var(--p-caret-color)`      | no blink at all; a permanently lit caret |

```css
:root {
  --p-caret-color: var(--p-red-30);  /* the tint                        */
  --p-caret-fade:  transparent;      /* the dim end of the fade         */
  --p-caret-width: 2px;              /* CodeMirror stroke width         */
  --p-caret-glide: 70ms;             /* 0s gives a teleporting caret back */
  --p-caret-blink: 1.1s;             /* one full cycle                  */
}
```

To switch the animation off entirely, append this to a user stylesheet:

```css
#write { animation: none; caret-animation: auto; }
.CodeMirror div.CodeMirror-cursor { transition: none; animation: none; }
```

Both the fade and the glide are dropped under `prefers-reduced-motion: reduce`; the caret then simply stays lit.

---

## Customising

Every knob lives in the `01 · ROOT VARIABLES` block at the top of the CSS file. The most useful ones:

```css
:root {
  --p-bg:              /* page background                */
  --p-text:            /* body text                      */
  --p-text-title:      /* headings                       */
  --p-text-muted:      /* secondary text, code chrome    */
  --p-border:          /* hairlines                      */
  --p-link:            /* link colour                    */
  --p-bold:            /* **bold**                       */
  --p-italic:          /* *italic*                       */
  --p-hl-yellow:       /* ==highlight== tints            */
  --p-callout-opacity: /* how strong the callout tints are */
  --p-font-text:       /* body font stack                */
  --p-font-mono:       /* code font stack                */
  --p-caret-*          /* see above                      */
}
```

Because the two builds share one token set, **editing a token in `primary.css` does not change `primary-dark.css`** — change both if you want the tweak to follow the mode switch.

### Putting a coloured bar back on callouts

If you prefer GitHub's look over Primary's, the theme deliberately cancels the built-in side rule. Append this to the CSS file to restore one:

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

### Background patterns

Primary ships a signature paper texture — a dotted or lined canvas. It used to be two commented-out blocks near the bottom of the theme CSS, which meant switching it on required opening that file and writing CSS. That is a poor trade for a look, so it is four small themes instead:

| Theme in the menu       | File                     | Paper                                     |
| ----------------------- | ------------------------ | ----------------------------------------- |
| **Primary Dots**        | `primary-dots.css`       | one 1 px dot every 50 px                  |
| **Primary Dots Dark**   | `primary-dots-dark.css`  | the same, on the dark palette             |
| **Primary Grid**        | `primary-grid.css`       | a 1 px rule every 50 px, on both axes     |
| **Primary Grid Dark**   | `primary-grid-dark.css`  | the same, on the dark palette             |

Drop the files in beside the theme and pick one from **Appearance → Themes**. That is the entire procedure — nothing to edit, nothing to uncomment.

Two things worth knowing if you plan to go further:

- **They import, they don't copy.** Each is about 2 KB and opens with `@import url("./primary.css")`, so a pattern theme can never drift out of step with the theme it belongs to. The one requirement is that `primary.css` stays next to it.
- **The ink is mixed, not picked.** Both patterns draw with `color-mix(in srgb, var(--p-text) 15%, transparent)` — 6 % for the grid, which lays down far more ink than a field of dots. Mixing from the text colour rather than naming a grey is deliberate: the ramps run 10 (lightest) to 140 (darkest) in *both* palettes, so a fixed grey number lands on opposite sides of the page background depending on the build, and no single step gives a matched pair. The rule that consumes the variable lives in section `20 · BACKGROUND PATTERN` of the theme, and `--p-bg-pattern` defaults to `none`, so `primary.css` on its own renders exactly as it always did.

To change the texture rather than choose one — a wider pitch, a fainter ink — edit `--p-bg-pattern-size` and `--p-pattern-ink` in the pattern file. If you would rather not carry a second file at all, the same thing can be appended to the bottom of `primary.css`:

```css
content, #write {
  background-image: radial-gradient(circle, color-mix(in srgb, var(--p-text) 15%, transparent) 1px, transparent 1px);
  background-size: 50px 50px;
}
```

That works, but it will not survive an update — see [Updating or removing](#updating-or-removing).

---

## Fonts

All four families ship in `primary-fonts/` — **27.6 MiB in eight woff2 files**. How each one is declared is deliberate:

| Family                | Declaration                            | What that buys                                                |
| --------------------- | -------------------------------------- | ------------------------------------------------------------- |
| **HarmonyOS Sans SC** | `local()` first, then the bundled file | 8.3 MiB is never read on a machine that already has the font  |
| **Maple Mono NF CN**  | `local()` first, then the bundled file | 18.5 MiB is never read on a machine that already has the font |
| **Inter**             | bundled file only                      | 0.69 MiB — cheaper to always read than to negotiate           |
| **Cascadia Code**     | bundled file only                      | 0.19 MiB, and it is a fallback that is rarely reached         |

Nothing is installed and nothing is downloaded: this is a desktop app reading local files.

The bundled woff2 files are re-wrapped copies of the fonts themselves, so `gasp` and hinting tables were kept rather than stripped for size. `FONTS.md` documents where every file came from, the licence for each, and what it takes to regenerate or drop the bundle.

---

## Repository layout

The first seven entries are the theme itself. Everything in `docs/` is documentation — read it, or ignore it and just copy the CSS files and the font folder.

```text
primary-typora-theme/
├── primary.css            the light build — the whole theme, and the file to edit
├── primary-dark.css       the dark build, same token set
├── primary-dots.css       light build + dotted paper        ┐
├── primary-dots-dark.css  dark build + dotted paper         │  optional background
├── primary-grid.css       light build + lined paper         │  patterns, ~2 KB each
├── primary-grid-dark.css  dark build + lined paper          ┘
├── primary-fonts/         eight woff2 files, must stay next to the CSS
├── docs/                  not needed to install — what it holds:
│   ├── primary-demo.md        the demo document: every element in one file
│   ├── preview-*.html         self-contained browser previews
│   ├── probe-fallback.html    font-fallback A/B page
│   └── screenshot-*.png       the images used above
├── FONTS.md               font provenance, licences, verification
├── README.md
├── README.zh-CN.md
└── LICENSE                GPL-3.0
```

---

## Compatibility

- **Typora 1.x** on Windows, macOS and Linux. The CSS files are plain CSS custom-property sheets — there is no build step, no preprocessor and no JavaScript.
- **The caret fade needs `caret-animation`** (Chromium 140 or newer). On an older runtime the `@supports` gate drops that block and nothing else changes.
- **The pattern themes use `@import`**, which the browser resolves relative to the theme file itself — the same mechanism several published Typora themes rely on to load their own fonts. Typora also follows it when exporting, so the exported CSS carries the pattern too. The only rule is that `primary.css` has to stay beside them.
- **Raw-HTML styling is export-only.** Typora's renderer removes `class` / `id` / `data-*` from user HTML; it puts them back when you export or print. The theme is written so nothing depends on them in the editor: tags are Markdown links, Obsidian callouts are the export-time layer on top of the five native alerts.
- **Five alert types, the whole callout palette.** Typora only parses `[!NOTE] [TIP] [IMPORTANT] [WARNING] [CAUTION]`; every other callout colour Primary ships is reachable through route B above.
- **Almost all of the download is the fonts.** If you would rather not carry 27.6 MiB of them, delete `primary-fonts/` and the `@font-face` block — everything else keeps working.

---

## Licence

The original Primary theme is released under the **GNU General Public License v3.0**. This Typora port is a derivative work — it reuses Primary's design and colour ramps — so it is released under the **same GPL-3.0**. A copy is included as [`LICENSE`](LICENSE).

Practically, for a theme that means: use it, modify it, share it freely — but if you redistribute a modified version, it has to stay under the GPL-3.0 as well.

The bundled fonts are a separate matter:

| Font              | Licence                                                       | Bundling                            |
| ----------------- | ------------------------------------------------------------- | ----------------------------------- |
| Inter             | SIL OFL 1.1                                                   | permitted, redistributed unmodified |
| Cascadia Code     | SIL OFL 1.1                                                   | permitted, redistributed unmodified |
| Maple Mono NF CN  | SIL OFL 1.1                                                   | permitted, redistributed unmodified |
| HarmonyOS Sans SC | Huawei's own font terms (free to use, including commercially) | see the caveat in `FONTS.md`        |

**Read [`FONTS.md`](FONTS.md) before redistributing this theme publicly** — it lists where each file came from and flags the one family whose terms are not the OFL.

## Credits

- Original theme: **[Primary](https://github.com/primary-theme/obsidian)** by Cecilia May — winner of Obsidian October 2021's Best Theme. All design credit belongs there; this port would not exist without it.
- Fonts bundled here, all redistributed unmodified: **Inter** by Rasmus Andersson, **Cascadia Code** by Microsoft and **Maple Mono NF CN** by subframe7536 (all SIL OFL 1.1), plus **HarmonyOS Sans SC** by Huawei. See [`FONTS.md`](FONTS.md).
- The Obsidian→Typora selector mapping, both palettes, the alert/callout bridges, the caret animation, the font packaging and the preview harness in this repository are original work.

---

Found something off, or a selector Typora renders differently on your machine? [Open an issue](https://github.com/tangolee/primary-typora-theme/issues) — screenshots and the Typora version help a lot.
