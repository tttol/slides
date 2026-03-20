# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A repository for managing presentation slides. Slides are written in [Marp](https://marp.app/) (Markdown Presentation Ecosystem) format.

## Slide Format

- Each slide is created as a Markdown file (`.md`)
- Marp settings (theme, pagination, styles, etc.) are defined in the YAML front matter at the top of each file
- Slide separators use `---` (horizontal rule)
- Per-slide class assignments are possible via HTML comments like `<!-- _class: title -->`

## Common CSS Styles
This css style must be applied all slides.
```css
style: |
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
  }
  table {
    margin: 0 auto;
  }
  th {
    background-color: #d4eeff;
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
