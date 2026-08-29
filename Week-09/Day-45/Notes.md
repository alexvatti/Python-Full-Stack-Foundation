# 🗓️ DAY 5 — Responsive Design, Media Queries, Variables & Animation (Deep Dive)
### CSS IS ENOUGH | Week 09 | 1 Hour (Extended)
### ⬅️ Continues from `Day4-CSS.md`

### 🎯 Goal
Make everything you built truly responsive, learn fluid sizing with `clamp()`, master CSS variables, and add real motion with `@keyframes` and pseudo-elements.

---

## 1. Media Queries — Mobile-First Approach

```css
/* Base styles = mobile first */
.features {
  display: grid;
  grid-template-columns: 1fr; /* 1 column by default */
  gap: 20px;
}

/* Tablet and up */
@media (min-width: 600px) {
  .features {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .features {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* You can also target MAX width (desktop-first approach) */
@media (max-width: 599px) {
  .hero h1 { font-size: 24px; }
}

/* Combine conditions */
@media (min-width: 600px) and (max-width: 1023px) {
  .hero { padding: 60px 30px; } /* tablet-only tweak */
}

/* Orientation-based */
@media (orientation: landscape) {
  .hero { padding: 40px 20px; }
}
```

**Common breakpoints (a widely used convention, not a hard rule):**
| Breakpoint | Typical device |
|---|---|
| `< 600px` | Mobile |
| `600px – 1023px` | Tablet |
| `≥ 1024px` | Desktop |
| `≥ 1440px` | Large desktop |

---

## 2. CSS Variables (Custom Properties) — In Depth

```css
:root {
  --primary-color: #ff6b6b;
  --dark-bg: #1e1e2f;
  --radius: 10px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 32px;
}

.cta-btn {
  background-color: var(--primary-color);
  border-radius: var(--radius);
  padding: var(--spacing-sm) var(--spacing-md);
}

/* Variables can be redefined inside a scope — great for theming */
.dark-theme {
  --primary-color: #ffb86b;
  --dark-bg: #0d0d14;
}

/* Fallback value if the variable isn't defined */
.safe-box {
  color: var(--text-color, #333);
}
```
Variables cascade like any other CSS property — redefine them inside a media query to adjust spacing responsively without duplicating whole rule blocks.

```css
:root { --gap: 16px; }
@media (min-width: 1024px) {
  :root { --gap: 32px; }
}
.features { gap: var(--gap); }
```

---

## 3. Fluid Sizing with `clamp()` (Modern Responsive Typography)

```css
.hero h1 {
  /* clamp(MIN, PREFERRED, MAX) */
  font-size: clamp(24px, 5vw, 48px);
  /* never smaller than 24px, never bigger than 48px,
     scales smoothly with viewport width in between */
}

.container {
  width: clamp(300px, 90%, 1200px);
  margin: 0 auto;
}
```
This one line often replaces 2–3 media queries for font sizing.

---

## 4. Transitions & Hover Animation

```css
.cta-btn {
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.cta-btn:hover {
  background-color: #e64c4c;
  transform: translateY(-2px);
}

.feature-card {
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.feature-card:hover {
  box-shadow: 0 8px 20px rgba(0,0,0,0.12);
  transform: translateY(-4px);
}
```

## 5. `@keyframes` — Real Animation (Beyond Hover)

```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero h1 {
  animation: fadeInUp 0.8s ease-out;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%      { transform: scale(1.05); }
}

.cta-btn {
  animation: pulse 2s infinite;
}
```

## 6. Pseudo-Elements for Decoration (`::before` / `::after`)

```css
.feature-card {
  position: relative;
}

.feature-card::before {
  content: "★";
  position: absolute;
  top: -10px;
  left: -10px;
  font-size: 20px;
  color: var(--primary-color);
}

/* A classic use: decorative quote marks, tooltips, or a colored bar */
.section-title::after {
  content: "";
  display: block;
  width: 40px;
  height: 3px;
  background: var(--primary-color);
  margin: 8px auto 0;
}
```

---

## 🔵 MINI PROJECT 3 (Finish) — Landing Page, Fully Responsive + Animated

Same `landing.html` from Day 4 — no HTML changes needed today.

**CSS — `landing.css`** *(this REPLACES the Day 4 version — final, complete file)*
```css
:root {
  --primary-color: #ff6b6b;
  --dark-bg: #1e1e2f;
  --radius: 10px;
  --gap: 20px;
}

* { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero {
  text-align: center;
  padding: 80px 20px;
  background-color: var(--dark-bg);
  color: white;
  animation: fadeInUp 0.8s ease-out;
}

.hero h1 {
  font-size: clamp(24px, 5vw, 40px);
  margin-bottom: 12px;
}

.hero p { font-size: 16px; color: #ccc; margin-bottom: 24px; }

.cta-btn {
  padding: 12px 28px;
  border: none;
  border-radius: var(--radius);
  background-color: var(--primary-color);
  color: white;
  font-size: 15px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.cta-btn:hover {
  background-color: #e64c4c;
  transform: translateY(-2px);
}

.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: var(--gap);
  padding: 50px clamp(20px, 5vw, 40px);
}

.feature-card {
  position: relative;
  background-color: #f7f7fb;
  border-radius: var(--radius);
  padding: 24px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0,0,0,0.06);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.feature-card::before {
  content: "★";
  position: absolute;
  top: -10px;
  left: -10px;
  font-size: 18px;
  color: var(--primary-color);
}

.feature-card:hover {
  box-shadow: 0 8px 20px rgba(0,0,0,0.12);
  transform: translateY(-4px);
}

/* Dark theme variant — toggle by adding class="dark-theme" to <body> */
.dark-theme {
  --primary-color: #ffb86b;
  --dark-bg: #0d0d14;
}

/* Tablet */
@media (min-width: 600px) {
  :root { --gap: 24px; }
}

/* Desktop */
@media (min-width: 1024px) {
  :root { --gap: 32px; }
  .features { padding: 60px 40px; }
}
```

---

## 🧪 Practice Exercises
1. Toggle `class="dark-theme"` on `<body>` in `landing.html` and confirm the color scheme swaps via variables.
2. Change `clamp(24px, 5vw, 40px)` values and resize the browser to see the scaling behavior.
3. Add a `@keyframes` bounce animation to `.cta-btn` that triggers once on page load.
4. Add a `::after` underline accent below `.hero h1` using the pattern shown above.

## ⚠️ Common Mistakes to Avoid
- Writing `max-width` media queries AND `min-width` ones inconsistently — pick ONE approach (mobile-first `min-width` is recommended) and stick to it.
- Forgetting `content: ""` on `::before`/`::after` — without it, the pseudo-element won't render at all.
- Overusing `@keyframes` with `infinite` — constant motion is distracting; reserve it for subtle accents (like the `pulse` example) or one-time entrance effects.

---

## ✅ Day 5 Checklist
- [ ] I understand mobile-first media queries and common breakpoints
- [ ] I can define, scope, and reuse CSS variables — including a theme swap
- [ ] I can use `clamp()` for fluid font sizing
- [ ] I can write `@keyframes` animations and use `::before`/`::after`
- [ ] Landing page is responsive, animated, and theme-ready ✅ **Mini Project 3 complete**

---

## 🏆 WEEK 09 COMPLETE

You shipped **3 real mini projects** across Day 1–5, each one deeper than the last:
1. **Profile Card** (Day 1–2) — selectors, specificity, box model, typography, gradients, layered shadows
2. **Navbar** (Day 3–4) — position/z-index, sticky headers, full Flexbox item toolkit
3. **Landing Page** (Day 4–5) — responsive Grid with `auto-fit`, `clamp()`, variables/theming, keyframe animation, pseudo-elements

### 🔜 Natural Next Step (Week 10 idea)
CSS transforms in 3D (`perspective`, `rotateX/Y`), advanced `@keyframes` sequencing, container queries (`@container`), and accessibility-focused CSS (`prefers-reduced-motion`, `prefers-color-scheme`).
