# Common-Style-Solution

Tips &amp; Snippets for Modern CSS 😎

Live Demo: [css.sdwh.dev](https://css.sdwh.dev)

A comprehensive, developer-friendly demonstration and interactive playground for modern CSS features and techniques, crafted with the **Cascadia Code** font and illustrated with open-source vector graphics from **OpenMoji** and **Tabler Icons**.

---

## 📚 Chapters & Demonstrations

1. **[Position](html/position.html)**: `static`, `relative`, `absolute`, `fixed`, `sticky`, absolute centering tricks (`transform: translate(-50%, -50%)`), and `z-index` stacking context.
2. **[Flexbox](html/flex.html)**: Interactive live playground for `justify-content`, `align-items`, and `flex-direction`, plus `flex-grow` proportional ratios and practical UI recipes (Auto-margin Navbar, Media Object, Centering).
3. **[Grid](html/grid.html)**: The zero-media-query auto-fit grid (`repeat(auto-fit, minmax(160px, 1fr))`), Bento Box layouts with row/column spanning, semantic `grid-template-areas`, and 1-line centering with `place-items: center`.
4. **[Animation](html/animation.html)**: Smooth CSS transitions, pure CSS toggle switches, `@keyframes` library (floating rocket, spin loader, pulse heartbeat, error shake), skeleton loading shimmer, animated gradient text, and an infinite ticker marquee.
5. **[Pseudo Classes & Elements](html/pseudoClass.html)**: Preserved decorative background shapes via `::before` & `transform`, pure CSS tooltips with `attr(data-tooltip)`, corner ribbon badges, the modern `:has()` parent selector, and micro-selectors (`::selection`, `::marker`).
6. **[Transforms](html/transform.html)**: 2D transforms (`rotate`, `scale`, `skew`, `translate`, `transform-origin`), 3D perspective flip cards with `backface-visibility: hidden`, and 3D isometric layered UI stacks.
7. **[Effects & Shadows](html/effects.html)**: Linear, radial, and conic gradients, gradient border cards, elevation shadow hierarchy, `box-shadow` vs. `filter: drop-shadow()` comparison, glassmorphism frosted glass (`backdrop-filter`), and a live CSS filter playground.
8. **[Clip-Path & Shapes](html/clipPath.html)**: Geometric clipping presets (circle, polygon, chevron, star, hexagon, speech bubble), modern angled/slanted section dividers, and fluid text wrapping with `shape-outside: circle(50%)`.
9. **[Modern CSS](html/modernCss.html)**: Dynamic theming via CSS Custom Properties (`--var`), sibling hover dimming with `:has()`, native `aspect-ratio` (16/9, 1/1, 4/3), and pure CSS scroll snap carousels.
10. **[Responsive Design](html/responsive.html)**: Container Queries (`@container`) with an interactive resizable component, mobile-first breakpoints, fluid typography with `clamp()`, and modern mobile viewport units (`dvh`, `svh`, `lvh`).
11. **[Icons & OpenMoji](html/icons.html)**: SVG styling with CSS, `currentColor` inheritance, Tabler Icons specifications, and OpenMoji vector asset integration.

---

## 🚀 Running Locally

You can serve the project using any static file server:

```bash
# Python 3
python3 -m http.server 8000

# Node.js
npx serve
```

Visit `http://localhost:8000` in your web browser.

---

## 🎨 Asset Credits

- **Fonts**: [Cascadia Code](https://github.com/microsoft/cascadia-code)
- **Emoji Illustrations**: [OpenMoji](https://openmoji.org/) (CC BY-SA 4.0)
- **Vector Icons**: [Tabler Icons](https://tablericons.com/) (MIT)
