---
title: Primary 主题移植演示
author: Cecilia May · ported to Typora
tags: [theme, obsidian, warm]
---

[TOC]

# Welcome to Primary

Primary is soft, chewy, comforting — like a chocolate chip cookie, or a warm
brownie. It merges **play** with *work*, and it was ported here from the Obsidian
theme of the same name.

Fine-tuned to pixel and colour perfection, Primary aims to take away the need to
think about customization, so that you can **focus on what matters** — the
concepts, that link, this great idea. <u>Underlined text</u> stays quiet,
~~struck-through text~~ steps back, and `inline code` wears a warm little chip.
Highlights come in three flavours: ==plain==, **==bold==** and *==italic==*.

Read more at [the Primary documentation](https://github.com/primary-theme/obsidian),
jump to [Callouts](#callouts), or mail <hello@example.com>.

## Headings

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

## Lists

- Bullet — the marker uses a muted clay tone
  - Second level turns terracotta
    - Third level turns slate blue
- Another item

1. First
2. Second
3. Third

- [x] functional but artistic experience
- [x] exceptional quality, down to the finest details
- [ ] timeless design
- [ ] easily extensible, customizable

## Blockquote

> Primary is an opinionated **Obsidian** theme that merges *play* with work.
>
> A second paragraph inside the same quote.

## Callouts

Typora's five native alerts are mapped onto Primary's own callout palette —
tinted header, cream body, one soft pixel of shadow.

> [!NOTE]
> Useful information that users should know, even when skimming.

> [!TIP]
> Helpful advice for doing things better or more easily — the mint one.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

For the full Obsidian set — including custom titles — drop in a raw HTML block.
Typora strips `class` / `data-*` while rendering, so these four are styled **on
export only**; inside the editor use the `> [!NOTE]` syntax above.

<div class="callout" data-callout="info">
  <div class="callout-title">Info</div>
  <div class="callout-content"><p>Blue-green tinted, straight from Primary's own palette.</p></div>
</div>

<div class="callout" data-callout="question">
  <div class="callout-title">Question · 这是自定义标题</div>
  <div class="callout-content"><p>Anything Obsidian can do with <code>&gt; [!question]</code> works here.</p></div>
</div>

<div class="callout" data-callout="danger">
  <div class="callout-title">Danger</div>
  <div class="callout-content"><p>Reds and corals for the things you should not do.</p></div>
</div>

<div class="callout" data-callout="example">
  <div class="callout-title">Example</div>
  <div class="callout-content"><p>A dusty rose example block.</p></div>
</div>

## Tags

Typora strips `class` from user HTML while rendering, so the pills hang off a
Markdown link instead — point a link at `#tag` and it becomes a Primary pill:

<<<<<<< Updated upstream:docs/primary-demo.md
[#primary-features](#tag) [#tags](#tag) [#obsidian](#tag)

Swap the target for one of the three tints:

[#yellow-pill](#tag-1) [#red-pill](#tag-2) [#blue-pill](#tag-3)
=======
[#fafa](#tag-1)

<span class="tag">#primary-features</span> <span class="tag">#tags</span>
<span class="tag tag-1">#yellow-pill</span> <span class="tag tag-2">#red-pill</span>
<span class="tag tag-3">#blue-pill</span>
>>>>>>> Stashed changes:primary-demo.md

## 中文排版

中文字形来自 **HarmonyOS Sans SC**，而拉丁字母、数字与标点仍由 **Inter** 渲染——
Inter 覆盖不到的字符会自动回退到中文黑体字面，两者基线一致，混排不会跳字。
这四个字体都已随主题打包成 woff2 放在 `primary-fonts/`，
**换一台没有安装这些字体的电脑打开，排版也不会变**。

正文里的**加粗中文**、*倾斜中文*、`行内中文代码`都跟随同一套配色：
加粗偏陶土红，斜体偏石板蓝。行距保持 Primary 原有的松弛感，
段落之间留白充裕，长段落阅读不吃力。

代码块中的中文则由 **Maple Mono NF CN** 承担，等宽网格严格 2:1，
中英文混排时纵向严格对齐：

```text
配置项      说明                    默认值
theme.name  主题名称                Primary
theme.mode  明暗模式 light / dark   light
font.cjk    中文字体                HarmonyOS Sans SC
font.mono   代码字体                Maple Mono NF CN
```

> [!NOTE]
> 提示类告示块同样支持中文标题与正文，图标与配色不受文字语种影响。

## Code

```javascript
// Generate a random number between 1 and 10
function generateRandomNumber() {
  return Math.floor(Math.random() * 10) + 1;
}
```

```css
.callout {
  background: color-mix(in srgb, rgb(var(--callout-rgb)) 32.5%, var(--p-bg));
  border-radius: 8px;
}
```

```python
def fib(n: int) -> int:
    """Return the n-th Fibonacci number."""
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

## Table

| Token   | Light       | Dark      | Meaning   |
| ------- | ----------- | --------- | --------- |
| `bold`  | terracotta  | coral     | emphasis  |
| `italic`| slate blue  | sky       | asides    |
| `link`  | warm red    | warm red  | anchors   |
| `mark`  | three tints | three tints | highlight |

## Math

Inline math such as $e^{i\pi} + 1 = 0$ sits nicely in the text flow, and display
math gets breathing room:

$$
\text{MSE} = \frac{1}{n}\sum_{i=1}^{n}\left(y_i - \hat{y}_i\right)^2
$$

## Horizontal rule

---

## Footnotes

Primary was voted Best Theme in Obsidian October 2021[^1].

[^1]: Obsidian October 2021, Best Theme category.
