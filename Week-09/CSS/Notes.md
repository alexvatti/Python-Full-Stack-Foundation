# CSS — Position, Display, Forms, Flexbox, Grid & Navigation Bar

Since you already know the basic CSS properties, let's focus on **what each concept does, when to use it, and how to remember it**.

---

# 1. CSS `position`

### What does it do?

`position` controls **where an element is placed on the page**.

Think:

> **"How should this element be positioned?"**

### Main values

| Value      | Simple meaning                           |
| ---------- | ---------------------------------------- |
| `static`   | Normal/default position                  |
| `relative` | Stay in normal place, but can be moved   |
| `absolute` | Position relative to a positioned parent |
| `fixed`    | Stay fixed to the browser screen         |
| `sticky`   | Acts normal until scrolling, then sticks |

### `static`

```css
.box {
    position: static;
}
```

Normal HTML flow.

Usually you don't need to write this because it is the default.

---

### `relative`

```css
.box {
    position: relative;
    top: 20px;
    left: 30px;
}
```

The element moves **from its original position**.

Important:

> `relative` is also commonly used as a parent for an `absolute` element.

---

### `absolute`

```css
.box {
    position: absolute;
    top: 10px;
    right: 20px;
}
```

The element is taken **out of the normal page flow**.

Usually:

```css
.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 0;
    right: 0;
}
```

Think:

> **Parent = reference point**
> **Child = positioned inside parent**

---

### `fixed`

```css
button {
    position: fixed;
    bottom: 20px;
    right: 20px;
}
```

The element stays in the same place on the **browser screen**, even while scrolling.

Common uses:

* Chat button
* Back-to-top button
* Floating menu

---

### `sticky`

```css
header {
    position: sticky;
    top: 0;
}
```

It behaves normally until you scroll to it, then it **sticks to the top**.

Common use:

* Sticky navigation bar
* Sticky table header

---

### Easy memory

```text
static    → normal
relative  → move from normal position
absolute  → place exactly
fixed     → fixed to screen
sticky    → stick while scrolling
```

---

# 2. CSS `display`

### What does it do?

`display` controls **how an element behaves and how its children are arranged**.

Think:

> **"How should this element be displayed?"**

Important values:

```css
display: block;
display: inline;
display: inline-block;
display: flex;
display: grid;
display: none;
```

---

## `display: block`

A block takes the **full available width**.

Examples:

```html
<div>Hello</div>
<p>Hello</p>
<h1>Hello</h1>
```

```css
div {
    display: block;
}
```

Think:

```text
|-----------------------|
|       DIV             |
|-----------------------|
```

New block normally starts on a new line.

---

## `display: inline`

Only takes the width it needs.

```css
span {
    display: inline;
}
```

Example:

```text
Hello World
^^^^^ ^^^^^
inline elements
```

`span` is a common inline element.

---

## `display: inline-block`

Combination of:

```text
inline + block
```

It stays **next to other elements**, but you can control:

* width
* height
* padding
* margin

Example:

```css
.box {
    display: inline-block;
    width: 200px;
    height: 100px;
}
```

---

## `display: none`

Completely removes the element from the layout.

```css
.menu {
    display: none;
}
```

The element is not visible and **doesn't occupy space**.

---

# 3. Forms

HTML forms collect **user input**.

Example:

```html
<form>
    <label>Name</label>
    <input type="text">

    <label>Email</label>
    <input type="email">

    <button>Submit</button>
</form>
```

CSS makes the form look better.

---

## Basic form styling

```css
form {
    width: 300px;
}

label {
    display: block;
    margin-bottom: 5px;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 15px;
}

button {
    padding: 10px 20px;
}
```

### Important form elements

```html
<input>
<textarea>
<select>
<option>
<button>
<label>
```

---

## Input types

```html
<input type="text">

<input type="email">

<input type="password">

<input type="number">

<input type="date">

<input type="checkbox">

<input type="radio">

<input type="file">

<input type="submit">
```

### Easy understanding

```text
text       → normal text
email      → email
password   → hidden password
number     → numbers
date       → date picker
checkbox   → multiple choices
radio      → one choice
submit     → submit form
```

---

# 4. Flexbox

## What is Flexbox?

Flexbox is used to arrange elements in **one direction**.

Think:

> **Flexbox = Row OR Column**

For example:

```text
[Box 1] [Box 2] [Box 3]
```

or:

```text
[Box 1]
[Box 2]
[Box 3]
```

---

## Basic Flexbox

HTML:

```html
<div class="container">
    <div>Box 1</div>
    <div>Box 2</div>
    <div>Box 3</div>
</div>
```

CSS:

```css
.container {
    display: flex;
}
```

Now the boxes normally appear in a row.

---

# `flex-direction`

Controls the direction.

```css
.container {
    display: flex;
    flex-direction: row;
}
```

```text
Box 1 → Box 2 → Box 3
```

Or:

```css
.container {
    display: flex;
    flex-direction: column;
}
```

```text
Box 1
  ↓
Box 2
  ↓
Box 3
```

---

# `justify-content`

Controls alignment along the **main axis**.

```css
.container {
    display: flex;
    justify-content: center;
}
```

Common values:

```css
justify-content: flex-start;
justify-content: center;
justify-content: flex-end;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

Example:

```css
justify-content: space-between;
```

Result:

```text
[Box 1]          [Box 2]          [Box 3]
```

---

# `align-items`

Controls alignment along the **cross axis**.

```css
.container {
    display: flex;
    align-items: center;
}
```

Very commonly used for **vertical centering**.

Example:

```css
.container {
    display: flex;
    align-items: center;
    height: 200px;
}
```

---

# `gap`

Adds space between items.

```css
.container {
    display: flex;
    gap: 20px;
}
```

Result:

```text
[Box 1] 20px [Box 2] 20px [Box 3]
```

---

# Perfect Flexbox Example

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
```

Think:

```text
display:flex
      ↓
make flexible layout

justify-content
      ↓
horizontal/main-axis alignment

align-items
      ↓
vertical/cross-axis alignment

gap
      ↓
space between items
```

---

# 5. CSS Grid

## What is Grid?

Grid is used for **rows AND columns**.

Think:

> **Flexbox = 1D**
> **Grid = 2D**

Example:

```text
┌───────┬───────┬───────┐
│ Box 1 │ Box 2 │ Box 3 │
├───────┼───────┼───────┤
│ Box 4 │ Box 5 │ Box 6 │
└───────┴───────┴───────┘
```

---

## Basic Grid

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```

This creates **3 columns**.

```text
1fr    1fr    1fr
 ↓      ↓      ↓
 1/3    1/3    1/3
```

---

## Example

```html
<div class="container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
</div>
```

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 20px;
}
```

Result:

```text
1     2     3

4     5     6
```

---

## Two columns

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
}
```

Result:

```text
1       2

3       4

5       6
```

---

## Different column sizes

```css
grid-template-columns: 2fr 1fr;
```

Means:

```text
┌──────────────────┬─────────┐
│                  │         │
│      2 parts     │ 1 part  │
│                  │         │
└──────────────────┴─────────┘
```

---

## Grid rows

```css
.container {
    display: grid;
    grid-template-rows: 100px 200px;
}
```

Controls row sizes.

---

## Grid gap

```css
.container {
    display: grid;
    gap: 20px;
}
```

Adds spacing between rows and columns.

---

# Flexbox vs Grid

| Flexbox              | Grid                    |
| -------------------- | ----------------------- |
| 1-dimensional        | 2-dimensional           |
| Row OR column        | Rows AND columns        |
| Great for navigation | Great for page layouts  |
| Great for alignment  | Great for cards/layouts |
| `display: flex`      | `display: grid`         |

### Easy memory

```text
Flexbox → LINE

Grid → TABLE
```

---

# 6. Navigation Bar

A navigation bar allows users to move between pages.

Example:

```text
Home | About | Services | Contact | Login
```

HTML:

```html
<nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Services</a>
    <a href="#">Contact</a>
</nav>
```

CSS:

```css
nav {
    display: flex;
    gap: 20px;
}

nav a {
    text-decoration: none;
}
```

---

# Navigation Bar Using Flexbox

A common approach:

```css
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
}
```

Example:

```text
LOGO                         Home About Services Contact
```

HTML:

```html
<nav>
    <div class="logo">My Website</div>

    <div class="links">
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Services</a>
        <a href="#">Contact</a>
    </div>
</nav>
```

CSS:

```css
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.links {
    display: flex;
    gap: 20px;
}
```

### What is happening?

```text
nav
 ↓
display:flex
 ↓
Logo and links go into a row
 ↓
justify-content:space-between
 ↓
Logo goes left
Links go right
```

---

# 7. Position + Navigation

You can also make a navigation bar stay at the top.

```css
nav {
    position: sticky;
    top: 0;
}
```

Now:

```text
Scroll ↓

┌─────────────────────────────┐
│ Home About Services Contact │ ← stays at top
└─────────────────────────────┘
```

---

# 8. Putting Everything Together

A simple website layout could look like this:

```text
┌──────────────────────────────────┐
│          NAVIGATION              │
│ Logo    Home About Contact       │
├──────────────────────────────────┤
│                                  │
│          MAIN CONTENT            │
│                                  │
│    ┌──────┐ ┌──────┐ ┌──────┐   │
│    │ Card │ │ Card │ │ Card │   │
│    └──────┘ └──────┘ └──────┘   │
│                                  │
├──────────────────────────────────┤
│             FORM                 │
│ Name:   [____________]           │
│ Email:  [____________]           │
│         [ Submit ]               │
└──────────────────────────────────┘
```

Possible CSS:

```css
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: sticky;
    top: 0;
}

.cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
```

---

# ⭐ The Most Important Things to Remember

You don't need to memorize every CSS property. Understand the **job** of each.

```text
POSITION
↓
Where is the element?

DISPLAY
↓
How does the element behave?

FLEXBOX
↓
Arrange things in a row/column

GRID
↓
Arrange things in rows + columns

FORM
↓
Collect information from the user

NAVIGATION BAR
↓
Move between pages/sections
```

### Your CSS mental map

```text
                 CSS
                  │
       ┌──────────┼───────────┐
       │          │           │
    Position    Display     Forms
       │          │
       │      ┌───┴────┐
       │      │        │
       │    Flex      Grid
       │      │        │
       └──────┴────────┘
              │
       Navigation Bar
```

### If you remember only 10 things

```css
position: relative;
position: absolute;
position: fixed;
position: sticky;

display: flex;
display: grid;

justify-content: center;
align-items: center;

grid-template-columns: 1fr 1fr;
gap: 20px;
```

**These concepts are the bridge from basic CSS to building real websites.**
