# 🗓️ DAY 1 — CSS Fundamentals (Selectors, Box Model, Units, Specificity)
### CSS IS ENOUGH | Week 09 | 1 Hour (Extended)

### 🎯 Goal
Understand how CSS attaches to HTML, master every common selector type, understand specificity, and fully internalize the box model.

---

## 1. Three Ways to Add CSS

```html
<!DOCTYPE html>
<html>
<head>
  <title>Day 1</title>
  <!-- 3. External CSS (BEST practice — cacheable, reusable, separates concerns) -->
  <link rel="stylesheet" href="style.css">
  <style>
    /* 2. Internal CSS — fine for single-page demos */
    h1 { color: navy; }
  </style>
</head>
<body>
  <!-- 1. Inline CSS (avoid in real projects — highest specificity, hard to maintain) -->
  <p style="color: red;">Inline styled text</p>
  <h1>Internal styled heading</h1>
</body>
</html>
```

**Why external wins:** one `.css` file can style hundreds of HTML pages, the browser caches it, and your HTML stays clean.

---

## 2. Selectors — The Full Targeting Toolkit

```css
/* Universal selector */
* { margin: 0; padding: 0; box-sizing: border-box; }

/* Element (type) selector */
p { color: #333; }

/* Class selector (reusable, most common) */
.highlight { background-color: yellow; }

/* ID selector (unique, one per page) */
#main-title { font-size: 32px; }

/* Grouping selector */
h1, h2, h3 { font-family: Arial, sans-serif; }

/* Descendant selector — targets ANY <p> inside .card, at any depth */
.card p { font-size: 14px; }

/* Child selector — targets ONLY direct children */
.card > p { margin-bottom: 8px; }

/* Adjacent sibling — the <p> immediately after an <h2> */
h2 + p { font-weight: bold; }

/* General sibling — every <p> that comes after an <h2> */
h2 ~ p { color: gray; }

/* Attribute selectors */
input[type="text"] { border: 1px solid #ccc; }
a[href^="https"] { color: green; }   /* starts with */
a[href$=".pdf"]  { color: red; }     /* ends with */

/* Pseudo-classes — style based on STATE */
a:hover      { text-decoration: underline; }
input:focus  { outline: 2px solid blue; }
li:first-child { font-weight: bold; }
li:last-child  { margin-bottom: 0; }
li:nth-child(2) { color: teal; }
li:nth-child(odd)  { background: #f4f4f4; }
li:nth-child(even) { background: #fff; }

/* Pseudo-elements — style a PART of an element */
p::first-line { font-weight: bold; }
p::first-letter { font-size: 200%; }
```

### 📊 Selector Cheat Sheet

| Selector | Example | Matches |
|---|---|---|
| Type | `p` | every `<p>` |
| Class | `.card` | every element with `class="card"` |
| ID | `#header` | the one element with `id="header"` |
| Descendant | `.card p` | any `<p>` inside `.card` |
| Child | `.card > p` | only direct `<p>` children |
| Attribute | `[type="text"]` | elements with that attribute value |
| Pseudo-class | `:hover`, `:nth-child()` | state or position |
| Pseudo-element | `::before`, `::first-line` | a sub-part of the element |

---

## 3. CSS Specificity — Who Wins When Rules Conflict

Specificity is calculated like a 4-digit score: **(inline, IDs, classes/attributes/pseudo-classes, elements)**

```css
p                { color: black; }   /* specificity: 0,0,0,1 */
.text             { color: blue;  }   /* specificity: 0,0,1,0 — WINS over p */
#main             { color: green; }   /* specificity: 0,1,0,0 — WINS over .text */
p style="color: red" /* inline    */  /* specificity: 1,0,0,0 — ALWAYS wins (except !important) */
```

**Rule of thumb:** IDs beat classes, classes beat elements, inline beats everything, and `!important` beats inline (but avoid it — it's a last resort, not a habit).

---

## 4. Units That Matter

| Unit | Meaning | When to use |
|---|---|---|
| `px` | Fixed pixels | Borders, precise control |
| `%` | Relative to parent | Fluid widths |
| `em` | Relative to parent font-size | Component-level scaling |
| `rem` | Relative to root (`html`) font-size | Global, consistent scaling |
| `vh` / `vw` | % of viewport height/width | Full-screen sections |
| `vmin` / `vmax` | % of the smaller/larger viewport dimension | Responsive squares, hero text |

```css
html { font-size: 16px; }          /* 1rem = 16px everywhere */
.title { font-size: 2rem; }        /* = 32px, no matter what */
.child-text { font-size: 1.2em; }  /* = 1.2x the PARENT's font-size */
.hero { height: 100vh; }           /* full screen height */
```

---

## 5. The Box Model (In Depth)

```
┌─────────────────────────────┐
│          margin             │
│  ┌─────────────────────     │
│  │       border        │    │
│  │  ┌───────────────┐  │    │
│  │  │   padding        │    │
│  │  │  ┌─────────┐  │  │    │
│  │  │  │ content │  │  │    │
│  │  │  └─────────┘  │  │    │
│  │  └───────────────┘  │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
```

```css
.box {
  width: 200px;
  padding: 20px;
  border: 2px solid #444;
  margin: 10px;
  box-sizing: border-box; /* width INCLUDES padding+border → total stays 200px */
}

.box-alt {
  box-sizing: content-box; /* DEFAULT — width is content ONLY, box grows bigger */
}
```

**Shorthand order matters — always clockwise from top:**
```css
.box {
  margin: 10px 20px 15px 5px; /* top right bottom left */
  padding: 10px 20px;         /* top/bottom = 10px, left/right = 20px */
  margin: 0 auto;             /* 0 top/bottom, auto left/right → centers a block element */
}
```

**Margin collapsing (a common gotcha):** vertically adjacent margins between block elements collapse into the *larger* one, not the sum. Padding never collapses.

---

## 🟢 MINI PROJECT 1 (Start) — Profile Card

**HTML — `profile.html`**
```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="profile.css">
</head>
<body>
  <div class="card">
    <img src="https://via.placeholder.com/100" alt="avatar" class="avatar">
    <h2 class="name">Alex Sharma</h2>
    <p class="role">Frontend Developer</p>
    <p class="bio">Loves building clean UIs and learning CSS one day at a time.</p>
    <div class="tags">
      <span class="tag">HTML</span>
      <span class="tag">CSS</span>
      <span class="tag">JS</span>
    </div>
  </div>
</body>
</html>
```

**CSS — `profile.css`** *(base file — Day 2 will extend this, do not delete)*
```css
* { box-sizing: border-box; margin: 0; padding: 0; }

.card {
  width: 300px;
  padding: 24px;
  margin: 40px auto;
  border: 1px solid #ddd;
}

.avatar {
  width: 100px;
  height: 100px;
  display: block;
  margin: 0 auto 16px auto;
}

.name { text-align: center; margin-bottom: 4px; }
.role { text-align: center; margin-bottom: 12px; }
.bio { text-align: center; }

.tags { text-align: center; margin-top: 16px; }

.tag {
  display: inline-block;
  padding: 4px 10px;
  margin: 2px;
  border: 1px solid #ccc;
}
```

---

## 🧪 Practice Exercises (do these before moving on)
1. Write a selector that targets only `<li>` items that are even-numbered.
2. Write a selector that targets a `<p>` directly inside a `<div class="box">` (not nested deeper).
3. Between `#nav .link` and `.container p`, which wins if both apply to the same element? Why?
4. Change `.card` above to use `box-sizing: content-box` and predict what happens to its rendered width. Test it.

## ⚠️ Common Mistakes to Avoid
- Forgetting `box-sizing: border-box` — leads to layout math that never quite fits.
- Overusing IDs for styling — they make specificity conflicts painful later. Prefer classes.
- Confusing `margin` (space outside the border) with `padding` (space inside the border).

---

## ✅ Day 1 Checklist
- [ ] I understand the 3 ways to write CSS
- [ ] I can write class, ID, descendant, child, attribute, and pseudo-class selectors
- [ ] I can predict which rule wins in a specificity conflict
- [ ] I can explain content → padding → border → margin, and margin collapsing
- [ ] Profile card HTML + basic structure done

**➡️ Continue in `Day2-CSS.md` — we extend `profile.css` with typography, backgrounds, gradients, and shadows.**
