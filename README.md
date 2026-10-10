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

Two separate obstacles have to be routed around here, and it is worth being  
precise about both.

**Typora has no hashtag syntax.** `#tag` stays plain text — it never becomes an  
element, so no CSS selector can reach it.

**Typora also strips `class`, `id` and `data-*` from user HTML when rendering.**  
The attributes survive export, but in the live preview they are gone, so  
`<span class="tag">#tag</span>` renders as a bare, unstyled span. That is why  
the earlier class-based pills appeared to do nothing.

The portable way out is a **Markdown link**. Typora builds link DOM itself, so  
the `href` is always present to select on — point a link at the reserved `#tag`  
target and it becomes a pill:

```markdown
[#primary-features](#tag)
```

| Link target | Pill                     |
| ----------- | ------------------------ |
| `#tag`      | the default neutral pill |
| `#tag-1`    | Primary's yellow tint    |
| `#tag-2`    | Primary's red tint       |
| `#tag-3`    | Primary's blue tint      |

`#tag*` is deliberately not a real heading id, so every tag link is inert — it  
exists purely as a styling hook. For export targets (HTML, PDF) the  
class-based form is still supported and styled:

```html
<span class="tag">#primary-features</span>
<span class="tag tag-1">#yellow-pill</span>
```

### 

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
