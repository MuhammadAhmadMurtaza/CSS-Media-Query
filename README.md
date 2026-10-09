<div align="center">

# 🎨 CSS Fundamentals: Media Queries, Variables & a Landing Page

**Three projects on responsive design, reusable values, and putting it all together**

</div>

---

## 📖 About This Repository

This repository contains mini-projects I built while learning CSS. Each folder holds a single `index.html` file, so every concept is easy to see, edit, and experiment with.

No frameworks, no build tools. Just HTML and CSS.

---

## 📑 Table of Contents

1. [Project Structure](#-project-structure)
2. [Experiment 1: Media Queries](#-experiment-1-media-queries)
3. [Experiment 2: CSS Variables](#-experiment-2-css-variables)
4. [Project: Aether Studio Landing Page](#-project-aether-studio-landing-page)
5. [How to Run](#-how-to-run)
6. [Key Takeaways](#-key-takeaways)
7. [Roadmap](#-roadmap)

---

## 📂 Project Structure

```
css-fundamentals/
│
├── 09-media-queries/
│   └── index.html
│
├── 10-css-variables/
│   └── index.html
│
├── 11-aether-studio-landing/
│   └── index.html
│
└── README.md
```

> 💡 Rename the folders to match your own layout. Each `index.html` is fully standalone.

---

## 📱 Experiment 1: Media Queries

📁 `09-media-queries/index.html`

### 🎯 Goal
Make a page **respond to the device**: screen width, orientation, and media type, using one stylesheet instead of separate versions.

### 🔑 Concepts Covered

<table>
  <tr>
    <th>Concept</th>
    <th>Example</th>
    <th>What it does</th>
  </tr>
  <tr>
    <td>Media type</td>
    <td><code>screen</code></td>
    <td>Targets screens. Others are <code>print</code> and <code>all</code>.</td>
  </tr>
  <tr>
    <td>Width condition</td>
    <td><code>(max-width: 455px)</code></td>
    <td>Applies when the viewport is <b>455px wide or narrower</b>.</td>
  </tr>
  <tr>
    <td>Orientation condition</td>
    <td><code>(orientation: portrait)</code></td>
    <td>Applies when the viewport is taller than it is wide.</td>
  </tr>
  <tr>
    <td>Logical operators</td>
    <td><code>and</code>, <code>not</code>, <code>only</code>, comma</td>
    <td>Combine or negate conditions. <code>only</code> hides the rule from very old browsers.</td>
  </tr>
  <tr>
    <td>Flex direction swap</td>
    <td><code>flex-direction: column</code></td>
    <td>Stacks flex items vertically instead of in a row.</td>
  </tr>
</table>

### 🧪 Code Highlight

```css
body {
  background-color: red;
}

@media screen and (orientation: portrait) {
  body {
    border: 2px solid purple;
  }
}

@media only screen and (max-width: 455px) {
  body {
    background-color: blue;
  }

  .boxes {
    flex-direction: column;
  }
}

.boxes {
  display: flex;
}

.box {
  width: 344px;
  height: 344px;
  background-color: steelblue;
  padding: 3px;
  margin: 3px;
}
```

### 🧠 What Happens Here

<table>
  <tr>
    <td>🖥️</td>
    <td><b>Wide screen:</b> the background is red, and the three boxes sit side by side in a flex row.</td>
  </tr>
  <tr>
    <td>📱</td>
    <td><b>455px or narrower:</b> the background turns blue and the boxes stack into a single column.</td>
  </tr>
  <tr>
    <td>🔄</td>
    <td><b>Portrait orientation:</b> a purple border is added around the body. This can happen on a phone and also on a desktop window that is taller than it is wide.</td>
  </tr>
</table>

> ℹ️ Media queries do **not** add specificity. A rule inside `@media` has the same weight as outside it, so when two rules conflict, the usual specificity and source-order rules decide the winner.

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Open the file and **drag the browser window narrower**. At 455px the background switches to blue and the boxes stack.
2. Open DevTools (`F12`) and use the **device toolbar** to test phone sizes and rotate between portrait and landscape.
3. Change `max-width: 455px` to `min-width: 455px` and watch the behavior flip: the rule now applies to wide screens.
4. Add a `print` query: `@media print { body { background: white; } }` and check **Print Preview**.
5. Combine conditions: `@media (min-width: 600px) and (max-width: 900px) { ... }` to target tablets only.

</details>

### 📚 Common Breakpoints (for reference)

| Device | Typical width |
|---|---|
| Small phones | up to 480px |
| Tablets | 481px to 768px |
| Small laptops | 769px to 1024px |
| Desktops | 1025px and above |

---

## 🎛️ Experiment 2: CSS Variables

📁 `10-css-variables/index.html`

### 🎯 Goal
Define values **once** and reuse them everywhere, so a whole theme can change from a single line.

### 🔑 Concepts Covered

<table>
  <tr>
    <th>Concept</th>
    <th>Syntax</th>
    <th>What it does</th>
  </tr>
  <tr>
    <td>Declaring a variable</td>
    <td><code>--color: rgb(255, 0, 247);</code></td>
    <td>Custom property names always start with <code>--</code>.</td>
  </tr>
  <tr>
    <td><code>:root</code> scope</td>
    <td><code>:root { ... }</code></td>
    <td>Makes variables available to the <b>entire page</b>.</td>
  </tr>
  <tr>
    <td>Using a variable</td>
    <td><code>var(--color)</code></td>
    <td>Inserts the stored value wherever you need it.</td>
  </tr>
  <tr>
    <td>Fallback value</td>
    <td><code>var(--color, blue)</code></td>
    <td>Uses <code>blue</code> only if <code>--color</code> is not defined.</td>
  </tr>
  <tr>
    <td>Scoped override</td>
    <td><code>li:first-child { --color: ...; }</code></td>
    <td>Redefining a variable on one element changes it for that element and its children only.</td>
  </tr>
  <tr>
    <td><code>:first-child</code></td>
    <td><code>ul li:first-child</code></td>
    <td>Targets only the first item in a list.</td>
  </tr>
</table>

### 🧪 Code Highlight

```css
:root {
  --color: rgb(255, 0, 247);
  --seccolor: rgb(231, 164, 246);
  --defpad: 23px;
  --defop: 0.2;
}

.nav {
  background-color: var(--color);
}

ul {
  display: flex;
}

ul li {
  opacity: var(--defop);
  list-style: none;
  padding: var(--defpad);
  border: 2px solid var(--seccolor);
}

ul li:first-child {
  background-color: var(--color, blue);
}

.container {
  background-color: var(--seccolor);
}
```

### 🎨 Variables in This Project

<table>
  <tr>
    <th>Variable</th>
    <th>Value</th>
    <th>Used for</th>
  </tr>
  <tr>
    <td><code>--color</code></td>
    <td><code>rgb(255, 0, 247)</code></td>
    <td>Nav background, first list item background</td>
  </tr>
  <tr>
    <td><code>--seccolor</code></td>
    <td><code>rgb(231, 164, 246)</code></td>
    <td>List item borders, container background</td>
  </tr>
  <tr>
    <td><code>--defpad</code></td>
    <td><code>23px</code></td>
    <td>Padding of each list item</td>
  </tr>
  <tr>
    <td><code>--defop</code></td>
    <td><code>0.2</code></td>
    <td>Opacity of each list item</td>
  </tr>
</table>

### 🧠 Good to Know

<table>
  <tr>
    <td>💡</td>
    <td>The fallback in <code>var(--color, blue)</code> is never used here because <code>--color</code> <b>is</b> defined in <code>:root</code>. It is only a safety net.</td>
  </tr>
  <tr>
    <td>💡</td>
    <td><code>opacity: 0.2</code> fades the <b>whole</b> list item: background, text, and border together.</td>
  </tr>
  <tr>
    <td>💡</td>
    <td>Unlike Sass variables, CSS variables are live in the browser, so they can be changed with JavaScript or overridden per element.</td>
  </tr>
</table>

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Change `--color` in `:root` to another value and watch the nav and the first list item update together.
2. Uncomment `--color: rgb(243, 87, 8);` inside `ul li:first-child`. Only that one item changes, because the variable is overridden in its own scope.
3. Rename `--color` in one place only and see the fallback `blue` appear.
4. Raise `--defop` from `0.2` to `1` to make the list items fully opaque.
5. Add a dark theme by redefining the variables inside a media query: `@media (prefers-color-scheme: dark) { :root { --color: #222; } }`.

</details>

---

## 🏢 Project: Aether Studio Landing Page

📁 `11-aether-studio-landing/index.html`

### 🎯 Goal
Bring together layout, responsive design, and interaction to build a **real landing page** for a fictional creative agency.

### 🧱 Page Structure

<table>
  <tr>
    <th>Section</th>
    <th>Contents</th>
    <th>Layout technique</th>
  </tr>
  <tr>
    <td><b>Hero</b></td>
    <td>Badge, headline, description, two buttons, tagline, and a featured image card</td>
    <td>Flexbox, two columns</td>
  </tr>
  <tr>
    <td><b>Services</b></td>
    <td>Three cards: Brand Design, Web Experiences, Growth Solutions</td>
    <td>CSS Grid with <code>auto-fit</code></td>
  </tr>
</table>

### 🧪 Corrected Hero Card Markup

```html
<div class="hero-card">
  <img src="..." alt="Creative Workspace">

  <div class="card-info">
    <span class="rating">★ 4.9</span>
    <h3>Modern Creative Spaces</h3>
    <p>Award-winning design environments that inspire innovation.</p>
  </div>
</div>
```

### 🔑 Concepts Covered

<table>
  <tr>
    <th>Concept</th>
    <th>Where it's used</th>
    <th>Why it matters</th>
  </tr>
  <tr>
    <td>Flexbox layout</td>
    <td><code>.hero</code>, <code>.btns</code>, <code>.icon</code></td>
    <td><code>justify-content</code>, <code>align-items</code>, and <code>gap</code> control alignment and spacing.</td>
  </tr>
  <tr>
    <td>Responsive grid</td>
    <td><code>.cards</code></td>
    <td><code>repeat(auto-fit, minmax(280px, 1fr))</code> creates as many columns as fit, with <b>no media query needed</b>.</td>
  </tr>
  <tr>
    <td>Hover animations</td>
    <td><code>.primary</code>, <code>.card</code></td>
    <td><code>transition</code> plus <code>transform: translateY()</code> creates a smooth lift effect.</td>
  </tr>
  <tr>
    <td><code>object-fit: cover</code></td>
    <td><code>.hero-card img</code></td>
    <td>Fills a fixed-height area without stretching the image.</td>
  </tr>
  <tr>
    <td>Typographic scale</td>
    <td><code>h1</code> at 65px, <code>line-height: 1.1</code></td>
    <td>Tight line height suits large headings, while loose line height (<code>1.8</code>) suits body text.</td>
  </tr>
  <tr>
    <td>Accent color with <code>span</code></td>
    <td><code>.hero h1 span</code></td>
    <td>Colors part of a heading without extra markup.</td>
  </tr>
  <tr>
    <td>Pill badge</td>
    <td><code>.badge</code></td>
    <td><code>inline-block</code> with large <code>border-radius</code> and letter spacing.</td>
  </tr>
  <tr>
    <td><code>float</code></td>
    <td><code>.rating</code></td>
    <td>Pushes the rating badge to the right of the card info.</td>
  </tr>
  <tr>
    <td>Responsive breakpoint</td>
    <td><code>@media (max-width: 950px)</code></td>
    <td>Stacks the hero into one column and shrinks the headline to 48px.</td>
  </tr>
</table>

### 🧪 Code Highlight

```css
/* Hero: two columns on desktop */
.hero {
  padding: 80px 8%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 70px;
  min-height: 90vh;
}

/* Services: responsive grid with no media query */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 25px;
}

/* Hover lift effect */
.card {
  transition: 0.3s;
}
.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
}

/* Stack the hero on smaller screens */
@media (max-width: 950px) {
  .hero {
    flex-direction: column;
  }
  .hero h1 {
    font-size: 48px;
  }
  .hero-card {
    width: 100%;
  }
}
```

### 🎨 Design Tokens

<table>
  <tr>
    <th>Use</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Page background</td>
    <td><code>#f7f8fa</code></td>
  </tr>
  <tr>
    <td>Primary accent (teal)</td>
    <td><code>#00a7b5</code></td>
  </tr>
  <tr>
    <td>Badge text</td>
    <td><code>#0b7e84</code></td>
  </tr>
  <tr>
    <td>Badge background</td>
    <td><code>#eefafb</code></td>
  </tr>
  <tr>
    <td>Services section background</td>
    <td><code>#f3f0ec</code></td>
  </tr>
  <tr>
    <td>Icon background</td>
    <td><code>#eafbfd</code></td>
  </tr>
  <tr>
    <td>Font</td>
    <td><code>Segoe UI, sans-serif</code></td>
  </tr>
</table>

> 💡 **Idea for improvement:** these colors repeat many times in the file. Moving them into CSS variables, as in Experiment 2, would let you re-theme the whole page by editing one line.

### 🐛 Common Pitfall: A Broken Tag

A missing closing quote or bracket, like `<div class="9</div>`, can swallow the markup after it. The browser then guesses what you meant, and elements such as the card info and the rating badge may not render. If part of your layout vanishes, validate your HTML first.

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Resize the window and watch the three service cards reflow from three columns to two to one, with no media query involved.
2. Narrow the window below 950px to see the hero stack into a single column.
3. Replace `auto-fit` with `auto-fill` and compare the behavior when there are fewer cards than columns.
4. Move the teal accent `#00a7b5` into a variable, `--accent`, and replace every occurrence with `var(--accent)`.
5. Add a fourth service card and see the grid adjust automatically.
6. Add `transition` to `.secondary` and give it a hover state so both buttons feel consistent.

</details>

---

## 🚀 How to Run

No installation needed.

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git

# 2. Move into the project
cd <your-repo-name>

# 3. Open any project in your browser
open 11-aether-studio-landing/index.html      # macOS
start 11-aether-studio-landing/index.html     # Windows
xdg-open 11-aether-studio-landing/index.html  # Linux
```

💡 **Tip:** Use the VS Code **Live Server** extension to see changes instantly as you edit. For responsive work, keep DevTools open in device mode.

---

## 🎓 Key Takeaways

<table>
  <tr>
    <td>✅</td>
    <td>Media queries let one stylesheet adapt to width, orientation, and media type.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Switching <code>flex-direction</code> from row to column is a simple, powerful way to make layouts mobile-friendly.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>CSS variables remove repetition: define in <code>:root</code>, use with <code>var()</code>, and add a fallback when needed.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Variables can be overridden in a narrower scope, which makes theming flexible.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>repeat(auto-fit, minmax(...))</code> builds responsive grids without writing breakpoints.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Small touches like hover lifts, soft shadows, and generous spacing make a page feel professional.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Validate your HTML when something disappears. One broken tag can affect everything after it.</td>
  </tr>
</table>

---

## 🗺️ Roadmap

- [x] `display` property
- [x] Viewport units and box model
- [x] CSS specificity
- [x] `overflow`
- [x] Lists and `list-style`
- [x] `box-shadow` and `text-shadow`
- [x] Positioning (`relative`, `absolute`, `fixed`, `sticky`)
- [x] Card component
- [x] Media queries
- [x] CSS variables
- [x] First full landing page
- [ ] Flexbox in depth
- [ ] CSS Grid in depth
- [ ] Keyframe animations
- [ ] Mobile-first workflow

---

<div align="center">

### ⭐ If you found this helpful, consider giving the repo a star!

Made with ❤️ while learning CSS

</div>
