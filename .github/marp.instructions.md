# Marpit Instructions

## Overview

Marpit is a framework for creating beautiful slide decks from Markdown. It powers Marp, converting Markdown and theme sets into HTML/CSS presentations. Marpit is extensible and can be used programmatically or via CLI.

---

## Getting Started

### 1. Install Marpit

```sh
npm install @marp-team/marpit
```

### 2. Create a Marpit Instance

```js
import { Marpit } from "@marp-team/marpit";
const marpit = new Marpit();
```

### 3. Render Markdown

```js
const { html, css, comments } = marpit.render("# Hello, Marpit!");
```

---

## Customization

### Constructor Options

- **Markdown parser options:**
  ```js
  const marpit = new Marpit({ markdown: { html: true, breaks: true } });
  ```
- **Custom container elements:**
  ```js
  import { Marpit, Element } from "@marp-team/marpit";
  const marpit = new Marpit({
    container: [
      new Element("article", { id: "presentation" }),
      new Element("div", { class: "slides" }),
    ],
    slideContainer: new Element("div", { class: "slide" }),
  });
  ```
- **Enable inline SVG slides (experimental):**
  ```js
  const marpit = new Marpit({ inlineSVG: true });
  ```

### Themes

- **Add a theme:**
  ```js
  const theme = marpit.themeSet.add(`
  /* @theme my-theme */
  section { background: #123; color: #fff; }
  `);
  ```
- **Set default theme:**
  ```js
  marpit.themeSet.default = theme;
  ```
- **Use theme in Markdown:**
  ```markdown
  <!-- theme: my-theme -->
  ```

---

## Advanced Usage

- **Output HTML as array:**
  ```js
  const { html } = marpit.render(markdown, { htmlAsArray: true });
  // html is an array of HTML per slide
  ```
- **Presenter notes:**

  - HTML comments (except directives) in Markdown are collected as presenter notes:

    ```markdown
    # Slide

    <!-- This is a note -->
    ```

  - Access notes via the `comments` property in the render result.

- **Plugins:**
  - Extend with Marpit, markdown-it, or PostCSS plugins:
    ```js
    marpit.use(marpitPlugin).use(markdownItPlugin).use(postcssPlugin);
    ```

---

## Writing Marpit Markdown

Marpit Markdown is compatible with standard Markdown editors. Slides look good even as plain Markdown.

### Slide Separation

- Separate slides with a horizontal ruler (`---`, `___`, `***`, or `- - -`).

  ```markdown
  # Slide 1

  foo

  ---

  # Slide 2

  bar
  ```

  _Tip: Leave an empty line before the ruler for best compatibility._

### Directives

- **Global settings:** Use YAML front-matter at the top:
  ```markdown
  ---
  marp: true
  theme: gaia
  paginate: true
  ---
  ```
- **Slide/page-specific:** Use HTML comments:
  ```markdown
  <!-- _backgroundColor: '#f8f8f8' -->
  <!-- _class: lead -->
  <!-- theme: my-theme -->
  ```

### Images

- Standard Markdown image syntax is supported:
  ```markdown
  ![alt text](https://via.placeholder.com/640x480.png)
  ```
- Marpit extends image syntax for advanced slide design (e.g., background images, sizing via directives).

### Fragmented Lists

- Reveal list items one by one with the fragment marker:
  ```markdown
  - Item 1
  - <!-- _fragment --> Item 2
  - <!-- _fragment --> Item 3
  ```

### Custom Theme CSS

- Write custom theme CSS with the `@theme` meta comment:
  ```css
  /* @theme custom */
  section {
    background: #222;
    color: #fff;
  }
  ```

### Inline SVG Slides

- Enable with the Marpit option `inlineSVG: true` for SVG output.

---

## References

- [Marpit API Documentation (JSDoc)](https://marpit-api.marp.app/)
- [Marpit: Markdown slide deck framework](https://marpit.marp.app/)
- [Marp CLI Documentation](https://marp.app/cli/)
- [Marp VS Code Extension](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)
- [Marpit on npm](https://www.npmjs.com/package/@marp-team/marpit)
- [Marpit on GitHub](https://github.com/marp-team/marpit)
