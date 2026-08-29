# 🗓️ DAY 4 — Flexbox Deep Dive + CSS Grid (Full Basics)
### CSS IS ENOUGH | Week 09 | 1 Hour (Extended)
### ⬅️ Continues from `Day3-CSS.md`

### 🎯 Goal
Master every remaining Flexbox item property, then go deep on CSS Grid — template areas, `minmax()`, and `auto-fit`/`auto-fill` for truly responsive grids without media queries.

---

## 1. Flexbox — The Complete Item Toolkit

```css
.flex-row {
  display: flex;
  flex-direction: row;     /* row | column | row-reverse | column-reverse */
  flex-wrap: wrap;         /* allows items to wrap to next line */
}

.flex-item {
  flex-grow: 1;      /* how much it grows to fill leftover space, relative to siblings */
  flex-shrink: 1;    /* how much it shrinks if space is tight */
  flex-basis: 200px; /* starting size before grow/shrink kicks in */
  /* shorthand: flex: 1 1 200px; */
}

.flex-item-fixed {
  flex: 0 0 150px;  /* grow:0 shrink:0 basis:150px → NEVER resizes, always 150px */
}

.flex-item-fluid {
  flex: 1;          /* shorthand for flex: 1 1 0 → grows/shrinks equally with siblings */
}

.flex-item-priority {
  order: -1;            /* moves before all default (order:0) items */
  align-self: flex-end; /* overrides the container's align-items, just for this item */
}
```

**Common flex patterns:**
```css
/* Equal-width columns, no matter how many items */
.equal-columns > * { flex: 1; }

/* One fixed sidebar + one fluid main content */
.layout { display: flex; }
.sidebar { flex: 0 0 250px; }
.main    { flex: 1; }

/* Sticky footer using flex on the whole page */
body { display: flex; flex-direction: column; min-height: 100vh; }
main { flex: 1; } /* pushes footer down even with little content */
```

---

## 2. CSS Grid — Full Basics

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 equal, flexible columns */
  grid-template-rows: auto auto;
  gap: 20px;                              /* row-gap + column-gap shorthand */
}

.grid-item-wide {
  grid-column: span 2; /* takes up 2 columns */
}

.grid-item-tall {
  grid-row: span 2; /* takes up 2 rows */
}
```

### `fr` unit and `minmax()`
```css
.grid-flexible {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* middle column is twice as wide */
}

.grid-safe {
  display: grid;
  grid-template-columns: repeat(3, minmax(150px, 1fr));
  /* each column is AT LEAST 150px, but grows equally beyond that */
}
```

### The Magic Combo: `auto-fit` + `minmax()` (Responsive WITHOUT media queries!)
```css
.responsive-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 20px;
  /* browser automatically fits as many 220px+ columns as will fit,
     and stretches them to fill remaining space */
}
```
`auto-fit` collapses empty tracks; `auto-fill` keeps them as empty placeholder columns. For card grids, `auto-fit` is almost always what you want.

### Named Template Areas (great for full page layouts)
```css
.page-layout {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  min-height: 100vh;
  gap: 16px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

### Grid Alignment
```css
.grid-container {
  justify-items: center;  /* aligns items horizontally WITHIN their cell */
  align-items: center;    /* aligns items vertically WITHIN their cell */
  justify-content: center; /* aligns the WHOLE grid within the container, if smaller */
}
```

**Flexbox vs Grid — quick rule of thumb:**

| Use Flexbox for... | Use Grid for... |
|---|---|
| Navbars, single rows/columns | Full page layouts |
| Aligning a group of items | Card grids, dashboards |
| One-dimensional flow | Two-dimensional (rows AND columns) |
| Content-driven sizing | Layout-driven sizing |

---

## 🟡 MINI PROJECT 2 (Finish) — Responsive Navbar

Same `navbar.html` from Day 3 — no HTML changes needed today.

**CSS — `navbar.css`** *(this REPLACES the Day 3 version — same file, extended with wrap + item properties)*
```css
* { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  padding: 16px 40px;
  background-color: #1e1e2f;
  position: sticky;
  top: 0;
  z-index: 50;
}

.logo {
  color: white;
  font-size: 22px;
  font-weight: 700;
  order: -1; /* always first, even if HTML order changes */
}

.logo span { color: #ff6b6b; }

.nav-links {
  display: flex;
  flex-wrap: wrap;
  flex: 1 1 auto;      /* takes up available space and can grow */
  justify-content: center;
  list-style: none;
  gap: 28px;
}

.nav-links a {
  color: #ccc;
  text-decoration: none;
  font-size: 15px;
}

.nav-links a:hover { color: white; }

.cta-btn {
  flex: 0 0 auto; /* never shrinks or grows */
  padding: 8px 18px;
  border: none;
  border-radius: 6px;
  background-color: #ff6b6b;
  color: white;
  cursor: pointer;
}

.back-to-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  background-color: #1e1e2f;
  color: white;
  cursor: pointer;
  z-index: 100;
}
```
✅ **Mini Project 2 complete**

---

## 🔵 MINI PROJECT 3 (Start) — Simple Landing Page (Grid Layout)

**HTML — `landing.html`** *(new file, new project)*
```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="landing.css">
</head>
<body>
  <header class="hero">
    <h1>Build Better with CSS</h1>
    <p>A landing page built entirely with Grid + Flexbox.</p>
    <button class="cta-btn">Get Started</button>
  </header>

  <section class="features">
    <div class="feature-card">
      <h3>Fast</h3>
      <p>Lightweight and quick to load.</p>
    </div>
    <div class="feature-card">
      <h3>Flexible</h3>
      <p>Adapts to any screen size.</p>
    </div>
    <div class="feature-card">
      <h3>Modern</h3>
      <p>Clean, minimal design language.</p>
    </div>
    <div class="feature-card">
      <h3>Accessible</h3>
      <p>Built with semantic, readable markup.</p>
    </div>
  </section>
</body>
</html>
```

**CSS — `landing.css`** *(base file — Day 5 will extend this, do not delete)*
```css
* { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }

.hero {
  text-align: center;
  padding: 80px 20px;
  background-color: #1e1e2f;
  color: white;
}

.hero h1 { font-size: 36px; margin-bottom: 12px; }
.hero p { font-size: 16px; color: #ccc; margin-bottom: 24px; }

.cta-btn {
  padding: 12px 28px;
  border: none;
  border-radius: 6px;
  background-color: #ff6b6b;
  color: white;
  font-size: 15px;
  cursor: pointer;
}

/* Using auto-fit + minmax — this is ALREADY responsive, no media query needed yet! */
.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 24px;
  padding: 60px 40px;
}

.feature-card {
  background-color: #f7f7fb;
  border-radius: 10px;
  padding: 24px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0,0,0,0.06);
}
```

---

## 🧪 Practice Exercises
1. Change `.features` back to `repeat(3, 1fr)` and resize the browser — compare to `auto-fit, minmax()`.
2. In `.navbar`, try `order: 1` on `.cta-btn` and `order: -1` on `.nav-links` — what changes visually?
3. Build a 2-row, 2-column grid using `grid-template-areas` for a simple header/sidebar/main/footer layout.
4. Add a 5th `.feature-card` and watch the grid reflow automatically.

## ⚠️ Common Mistakes to Avoid
- Forgetting `fr` units and using `%` instead — `fr` distributes LEFTOVER space, `%` is relative to the container's total width; they behave differently with `gap`.
- Mixing up `auto-fit` and `auto-fill` — `auto-fill` leaves invisible empty tracks that can affect centering.
- Setting `flex: 1` on every item AND expecting fixed widths — `flex-grow` will override your `width`.

---

## ✅ Day 4 Checklist
- [ ] I understand flex-grow/shrink/basis and the `flex` shorthand
- [ ] I can build a responsive Grid using `auto-fit` + `minmax()` — no media query needed
- [ ] I can lay out a page using `grid-template-areas`
- [ ] Navbar is wrap-friendly ✅ **Mini Project 2 complete**
- [ ] Landing page hero + responsive feature grid built

**➡️ Continue in `Day5-CSS.md` — we extend `landing.css` with media queries, CSS variables, `clamp()`, keyframe animations, and transitions to finish the week.**
