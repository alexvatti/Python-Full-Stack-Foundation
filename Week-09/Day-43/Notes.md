# 🗓️ DAY 3 — Display, Position, Z-Index & Flexbox Basics (Deep Dive)
### CSS IS ENOUGH | Week 09 | 1 Hour (Extended)
### ⬅️ Continues from `Day2-CSS.md`

### 🎯 Goal
Understand every common `display` value, all five `position` values with stacking context, and get comfortable with core Flexbox properties.

---

## 1. Display Property — Full Set

```css
.block-el   { display: block; }        /* full width, own line: div, p, h1, ul */
.inline-el  { display: inline; }        /* no width/height control: span, a, strong */
.inline-blk { display: inline-block; }  /* sits inline BUT respects width/height/margin */
.hidden-el  { display: none; }          /* removed from layout AND accessibility tree */
.invisible-el { visibility: hidden; }   /* hidden but STILL takes up space (different from none!) */
.flex-el    { display: flex; }          /* one-dimensional flexible layout (this week's focus) */
.grid-el    { display: grid; }          /* two-dimensional layout (Day 4) */
.table-el   { display: table; }         /* legacy — mimics HTML table behavior */
```

**`display: none` vs `visibility: hidden`:**
| | Takes up space? | In accessibility tree? |
|---|---|---|
| `display: none` | ❌ No | ❌ No |
| `visibility: hidden` | ✅ Yes | ❌ No |

---

## 2. Position Property — All Five Values

```css
.static-el   { position: static; }      /* default flow, top/left/right/bottom ignored */

.relative-el {
  position: relative;
  top: 10px;
  left: 10px;
  /* shifts from where it WOULD have been, but still reserves its original space */
}

.absolute-el {
  position: absolute;
  top: 0;
  right: 0;
  /* removed from normal flow; positioned relative to nearest ANCESTOR with position != static */
}

.fixed-el {
  position: fixed;
  bottom: 20px;
  right: 20px;
  /* positioned relative to the VIEWPORT; stays put on scroll — great for "back to top" buttons */
}

.sticky-el {
  position: sticky;
  top: 0;
  /* behaves like relative UNTIL it crosses the given threshold, then behaves like fixed */
}
```

**The classic pattern — absolute inside relative:**
```css
.parent {
  position: relative;   /* becomes the "anchor" */
}

.badge {
  position: absolute;
  top: -8px;
  right: -8px;
  /* .badge is now positioned relative to .parent, not the whole page */
}
```

### Z-Index & Stacking Context
```css
.modal-overlay { position: fixed; z-index: 100; }
.modal-box     { position: fixed; z-index: 101; } /* sits above the overlay */
.tooltip       { position: absolute; z-index: 10; }
```
`z-index` only works on positioned elements (`relative`, `absolute`, `fixed`, `sticky`) — it does nothing on `static` elements.

---

## 3. Flexbox — Container Properties (Full Basics)

```css
.flex-container {
  display: flex;
  flex-direction: row;             /* row | row-reverse | column | column-reverse */
  justify-content: space-between;  /* main-axis alignment */
  align-items: center;             /* cross-axis alignment */
  flex-wrap: nowrap;                /* nowrap | wrap | wrap-reverse */
  gap: 20px;                        /* space between items (row-gap column-gap also work) */
}
```

| `justify-content` value | Effect |
|---|---|
| `flex-start` | items packed at the start (default) |
| `center` | items centered |
| `flex-end` | items packed at the end |
| `space-between` | equal space BETWEEN items, none at edges |
| `space-around` | equal space around each item |
| `space-evenly` | perfectly equal space everywhere |

| `align-items` value | Effect |
|---|---|
| `stretch` | items fill the cross-axis (default) |
| `flex-start` | items align to top |
| `center` | items align to middle |
| `flex-end` | items align to bottom |
| `baseline` | items align by their text baseline |

## 4. Flexbox — Item Properties (Preview)
```css
.flex-item-special {
  order: -1;         /* moves this item before others, regardless of HTML order */
  align-self: flex-end; /* override align-items for THIS item only */
}
```

---

## 🟡 MINI PROJECT 2 (Start) — Responsive Navbar

**HTML — `navbar.html`** *(new file, new project)*
```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="navbar.css">
</head>
<body>
  <nav class="navbar">
    <div class="logo">Brand<span>.</span></div>
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
    <button class="cta-btn">Sign Up</button>
  </nav>

  <!-- a floating "back to top" button to practice position: fixed -->
  <button class="back-to-top">↑ Top</button>
</body>
</html>
```

**CSS — `navbar.css`** *(base file — Day 4 will extend this, do not delete)*
```css
* { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 40px;
  background-color: #1e1e2f;
  position: sticky;   /* sticks to top when scrolling */
  top: 0;
  z-index: 50;
}

.logo {
  color: white;
  font-size: 22px;
  font-weight: 700;
}

.logo span { color: #ff6b6b; }

.nav-links {
  display: flex;
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

---

## 🧪 Practice Exercises
1. Change `.navbar`'s `position` from `sticky` to `fixed` and observe the difference when scrolling.
2. Add a small red "notification dot" `<span>` inside `.logo` and position it absolutely in the top-right corner.
3. Change `justify-content` on `.navbar` to `center` and `flex-start` — note how the layout shifts.
4. Try `display: none` vs `visibility: hidden` on `.cta-btn` — check the DevTools layout to see the difference.

## ⚠️ Common Mistakes to Avoid
- Using `position: absolute` without setting `position: relative` on the intended parent — it'll jump to the nearest positioned ancestor (or the page itself).
- Forgetting that `z-index` needs a `position` value other than `static` to work at all.
- Confusing `justify-content` (main axis) with `align-items` (cross axis) — remember: in `flex-direction: row`, main axis = horizontal.

---

## ✅ Day 3 Checklist
- [ ] I understand every `display` value and when to use each
- [ ] I know when to use relative/absolute/fixed/sticky, and how stacking context works
- [ ] I built a horizontal, sticky navbar row with Flexbox
- [ ] Navbar structure works (not yet responsive)

**➡️ Continue in `Day4-CSS.md` — we extend `navbar.css` with flex-wrap and item properties, then start the Landing Page project with CSS Grid.**
