# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A repository for managing presentation slides. Slides are written in [Marp](https://marp.app/) (Markdown Presentation Ecosystem) format.

## Slide Format

- Each slide is created as a Markdown file (`.md`)
- Marp settings (theme, pagination, styles, etc.) are defined in the YAML front matter at the top of each file
- HTML is enabled project-wide via `.marprc.yml` (`html: true`). Do NOT write `html: true` in slide front matter — it is silently ignored by Marp
- Slide separators use `---` (horizontal rule)
- Per-slide class assignments are possible via HTML comments like `<!-- _class: title -->`

## Common CSS Styles
This css style must be applied all slides.
```css
style: |
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500&display=swap');
  section {
    font-family: 'Noto Sans JP', sans-serif;
    background: linear-gradient(to bottom, #7a9df5, #ffffff);
  }
  section.title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-image: linear-gradient(rgba(255,255,255,0.80), rgba(255,255,255,0.60)), url('../images/redrock.jpeg');
    background-size: cover;
    background-position: center;
  }
  section.title h1 {
    font-size: 2.5em;
    color: #000;
  }
  strong {
    color: #000;
  }
  code {
    background-color: #e8f0fe;
    color: #1a73e8;
    font-family: 'Fira Code', monospace;
  }
  table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 10px 25px rgba(0,0,0,0.05);
    border: 1px solid #94a3b8;
    background-color: #ffffff;
  }
  th {
    background-color: #cbd5e1;
    color: #475569;
    font-weight: 700;
    padding: 20px 32px;
    text-align: left;
    border-bottom: 2px solid #94a3b8 !important;
    border-right: 1px solid #94a3b8 !important;
    letter-spacing: 0.05em;
  }
  th:last-child {
    border-right: none !important;
  }
  td {
    padding: 20px 32px;
    border-bottom: 1px solid #94a3b8 !important;
    border-right: 1px solid #94a3b8 !important;
    vertical-align: middle;
    color: #475569;
  }
  td:last-child {
    border-right: none !important;
  }
  tr:last-child td {
    border-bottom: none !important;
  }
  tr:nth-child(even) td {
    background-color: #fafafa;
  }
  pre {
    background-color: #1e1e1e;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    border: 1px solid #333;
    padding: 32px;
    padding-top: 56px;
    position: relative;
    overflow: hidden;
  }
  pre::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 40px;
    background-color: #2d2d2d;
    border-bottom: 1px solid #111;
    border-radius: 12px 12px 0 0;
  }
  pre::after {
    content: '';
    position: absolute;
    top: 14px;
    left: 16px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background-color: #ff5f56;
    box-shadow: 20px 0 0 #ffbd2e, 40px 0 0 #27c93f;
  }
  pre code {
    background-color: transparent;
    color: #d4d4d4;
    font-family: 'Fira Code', monospace;
    font-size: 18px;
    line-height: 1.6;
  }
  .hljs-keyword { color: #56b6c2; }
  .hljs-meta { color: #c678dd; }
  .hljs-title { color: #e5c07b; }
  .hljs-title.class_ { color: #e5c07b; }
  .hljs-title.function_ { color: #61afef; }
  .hljs-comment { color: #7f848e; font-style: italic; }
  .hljs-string { color: #98c379; }
  .hljs-number { color: #d19a66; }
  .hljs-built_in { color: #e5c07b; }
  .callout {
    border-radius: 8px;
    padding: 12px 18px 14px;
    margin: 14px 0;
    border-left: 5px solid;
  }
  .callout::before {
    display: block;
    font-weight: 700;
    font-size: 0.8em;
    margin-bottom: 8px;
    letter-spacing: 0.05em;
  }
  .callout-info {
    background-color: #dbeafe;
    border-color: #3b82f6;
    color: #1e3a5f;
  }
  .callout-info::before {
    content: 'ℹ  INFO';
    color: #2563eb;
  }
  .callout-warn {
    background-color: #fef3c7;
    border-color: #f59e0b;
    color: #78350f;
  }
  .callout-warn::before {
    content: '⚠  WARN';
    color: #d97706;
  }
  .callout-erro {
    background-color: #fee2e2;
    border-color: #ef4444;
    color: #7f1d1d;
  }
  .callout-erro::before {
    content: '✖  ERRO';
    color: #dc2626;
  }
  .callout-important {
    background-color: #ede9fe;
    border-color: #8b5cf6;
    color: #3b0764;
  }
  .callout-important::before {
    content: '★  IMPORTANT';
    color: #7c3aed;
  }
```

## Build / Preview

Slides can be built and previewed with Marp CLI:

```bash
# Preview (display in browser)
npx @marp-team/marp-cli --preview <markdown-file>

# PDF output
npx @marp-team/marp-cli --pdf <markdown-file>

# HTML output
npx @marp-team/marp-cli <markdown-file>
```

Preview is also available via the "Marp for VS Code" extension.

## Repository Structure

Each presentation is stored in a directory named after its topic (e.g., `ここが辛いよLambda/`).
Shared images are stored in the `images/` directory and referenced from slides using relative paths (`../images/`).

## Marp Tips

### Specifying Image Size
Inline image sizes are specified within the alt text:
- Height: `![h:400](image.png)`
- Width: `![w:600](image.png)`

### Background Images
- Global background: specify `background-image` in the `style` section of the front matter
- Per-slide background: use the `![bg](image.png)` syntax
- Split layout: `![bg left:30%](image.png)` places the image on the left and text on the right

### Per-Slide Styles
To apply CSS to a specific slide only, use `<style scoped>`:
```markdown
<style scoped>
section {
  text-align: center;
}
</style>
```
This has higher specificity than the global `style` section and reliably overrides the theme's default styles.

### Callout Blocks
Use `<div>` with callout classes to display GitHub-style callout blocks.
Available classes: `callout-info`, `callout-warn`, `callout-erro`, `callout-important`

```html
<div class="callout callout-info">
Informational message here.
</div>

<div class="callout callout-warn">
Warning message here.
</div>

<div class="callout callout-erro">
Error message here.
</div>

<div class="callout callout-important">
Important message here.
</div>
```
