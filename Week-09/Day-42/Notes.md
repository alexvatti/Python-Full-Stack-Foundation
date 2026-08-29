# 🗓️ DAY 2 — Typography, Backgrounds, Borders & Shadows (Deep Dive)
### CSS IS ENOUGH | Week 09 | 1 Hour (Extended)
### ⬅️ Continues from `Day1-CSS.md`

### 🎯 Goal
Go beyond basic text styling — cover font shorthand, web fonts, multiple backgrounds, gradients, border tricks, and layered shadows.

---

## 1. Typography — Full Toolkit

```css
body {
  font-family: 'Segoe UI', Arial, sans-serif;
  font-size: 16px;
  line-height: 1.6;      /* readability sweet spot: 1.4–1.8 */
  color: #2b2b2b;
}

h1 {
  font-size: 2rem;
  font-weight: 700;      /* 100(thin) - 900(black); 400 = normal, 700 = bold */
  letter-spacing: 0.5px; /* space between letters */
  word-spacing: 2px;     /* space between words */
}

.subtitle {
  font-style: italic;
  text-transform: uppercase;  /* lowercase | capitalize | none */
  text-align: center;         /* left | right | justify */
  text-decoration: none;
}

/* Font shorthand: style weight size/line-height family */
.shorthand-example {
  font: italic 700 18px/1.5 'Segoe UI', sans-serif;
}

/* Importing a web font (Google Fonts style) */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');

.branded-heading {
  font-family: 'Poppins', sans-serif;
}

/* Text overflow — for cutting off long text cleanly */
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;  /* shows "…" */
}

/* Multi-line clamp (modern browsers) */
.clamp-3-lines {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Text shadow */
.glow-text {
  text-shadow: 0 0 8px rgba(255, 107, 107, 0.8);
}
```

---

## 2. Backgrounds — Full Toolkit

```css
.section-1 { background-color: #f4f4f4; }

.section-2 {
  background-image: url('bg.jpg');
  background-size: cover;       /* fill container, may crop */
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed; /* parallax-style fixed background */
}

/* Linear gradient */
.section-3 {
  background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
}

/* Radial gradient */
.section-4 {
  background: radial-gradient(circle, #ff6b6b, #1e1e2f);
}

/* Multiple backgrounds layered (first listed = top layer) */
.section-5 {
  background:
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),  /* dark overlay */
    url('bg.jpg');
  background-size: cover;
}

/* background shorthand order: color image repeat attachment position/size */
.section-6 {
  background: #222 url('pattern.png') repeat-x fixed top center;
}
```

---

## 3. Borders, Radius & Shadows — Full Toolkit

```css
.rounded-box {
  border: 2px solid #ccc;
  border-radius: 12px;          /* soft corners */
}

/* Individual corners */
.custom-radius {
  border-top-left-radius: 20px;
  border-bottom-right-radius: 20px;
}

/* Individual sides */
.left-accent {
  border-left: 4px solid #ff6b6b;
}

.circle-avatar {
  border-radius: 50%;           /* perfect circle on a square image */
}

/* Dashed / dotted / double styles */
.ticket-style {
  border: 2px dashed #999;
}

/* box-shadow: offset-x offset-y blur spread color */
.elevated-card {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.inner-shadow {
  box-shadow: inset 0 0 8px rgba(0,0,0,0.2);
}

/* MULTIPLE shadows, comma-separated, for realistic depth */
.deep-shadow {
  box-shadow:
    0 1px 2px rgba(0,0,0,0.07),
    0 2px 4px rgba(0,0,0,0.07),
    0 4px 8px rgba(0,0,0,0.07);
}

/* border-image (advanced, decorative borders using an image slice) */
.fancy-border {
  border: 12px solid transparent;
  border-image: url('border-pattern.png') 30 round;
}
```

---

## 🟢 MINI PROJECT 1 (Finish) — Profile Card, Fully Styled

Same `profile.html` from Day 1 — add nothing new, just style what's there (including the `.tags`).

**CSS — `profile.css`** *(this REPLACES the Day 1 version — same file, extended)*
```css
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card {
  width: 300px;
  padding: 32px 24px;
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  text-align: center;
}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 3px solid #764ba2;
  display: block;
  margin: 0 auto 16px auto;
  box-shadow: 0 4px 10px rgba(0,0,0,0.15);
}

.name {
  font-size: 22px;
  font-weight: 700;
  color: #222;
  margin-bottom: 4px;
}

.role {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #764ba2;
  margin-bottom: 16px;
}

.bio {
  font-size: 14px;
  line-height: 1.6;
  color: #555;
}

.tags { margin-top: 16px; }

.tag {
  display: inline-block;
  padding: 4px 12px;
  margin: 2px;
  border-radius: 20px;
  background-color: #f0eaf9;
  color: #764ba2;
  font-size: 12px;
  font-weight: 600;
}
```

---

## 🧪 Practice Exercises
1. Add a `text-shadow` to `.name` for a subtle glow effect.
2. Change `.card`'s background to a radial gradient instead of the page's linear one.
3. Add a fourth `.tag` and give the tags a hover effect using `:hover` (preview of Day 3/5 material — try it with `background-color` change only).
4. Try `background-attachment: fixed` on the `body` and scroll — observe the parallax effect.

## ⚠️ Common Mistakes to Avoid
- Forgetting `no-repeat` on background images — they'll tile unexpectedly.
- Overusing heavy box-shadows — layered *soft* shadows look more realistic than one dark one.
- Using `%` for `border-radius` on non-square elements — you'll get an oval, not a circle.

---

## ✅ Day 2 Checklist
- [ ] I can use font shorthand and import web fonts
- [ ] I can apply gradients, multiple backgrounds, and background-attachment
- [ ] I know how to layer multiple box-shadows for depth
- [ ] Profile card is fully polished ✅ **Mini Project 1 complete**

**➡️ Continue in `Day3-CSS.md` — we start a brand-new project: the Navbar, using Flexbox.**
