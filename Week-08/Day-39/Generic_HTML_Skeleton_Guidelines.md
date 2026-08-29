# Generic HTML Page Skeleton — Design Guidelines (HTML Only)

This is the common structural template used across all three mini
projects (Portfolio / Student-Course Info / Gym-Nutrition Coaching).
Use this as a starting skeleton for **any** new webpage — HTML only,
no CSS, no JavaScript.

---

## 1. Base Document Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Short description of the page">
    <title>Page Title</title>
</head>
<body>

</body>
</html>
```

**Rules:**
- `<!DOCTYPE html>` is always the first line.
- `<html lang="en">` declares the language.
- `<head>` never contains visible content — only metadata.
- Always include `charset` and `viewport` meta tags.

---

## 2. Generic Page Structure (used in all 3 projects)

```text
<body>
│
├── <header>              → site/page title + tagline
│
├── <nav>                 → in-page or site navigation links
│
├── <main>                → ONE per page, holds everything below
│   │
│   ├── <section id="...">      → Section 1 (e.g. About / Directory / About Program)
│   ├── <section id="...">      → Section 2 (e.g. Skills / Courses / Programs)
│   ├── <section id="...">      → Section 3 (table: schedule/scores/timetable)
│   ├── <article id="...">      → Long-form standalone content (notice/essay)
│   ├── <section id="...">      → Multimedia (image/figure/audio/video)
│   ├── <section id="faq">      → FAQ using <details>/<summary>
│   ├── <aside>                 → related/side content
│   └── <section id="...">      → Form (contact/enroll/join)
│
└── <footer id="contact"> → contact info + copyright
```

**Rules:**
- Every section that's a nav target gets an `id` (`id="about"`, `id="courses"`, etc.) matching the `<nav>` links (`href="#about"`).
- Use `<section>` for a themed block of content, `<article>` for something that could stand alone (a notice, blog-style write-up), `<aside>` for supplementary/related info.
- Only one `<main>` per page.

---

## 3. Header Block

```html
<header id="home">
    <h1>Page/Brand Name</h1>
    <p>One-line tagline or purpose</p>
</header>
```

---

## 4. Navigation Block

```html
<nav aria-label="Main Navigation">
    <a href="#section-1">Label</a>
    <a href="#section-2">Label</a>
    <a href="#section-3">Label</a>
    <a href="#contact">Contact</a>
</nav>
```

**Rule:** Every `href="#x"` must match a real `id="x"` somewhere on the page.

---

## 5. Content Section Pattern

```html
<section id="section-id">
    <h2>Section Heading</h2>
    <p>Explanatory paragraph.</p>
    <ul>
        <li>Item</li>
        <li>Item</li>
    </ul>
</section>
```

Swap `<ul>` for `<ol>` (steps/sequence) or `<dl>` (term/definition pairs) as needed.

---

## 6. Table Pattern (data display)

```html
<section id="table-section">
    <h2>Heading</h2>
    <table>
        <caption>Table Title</caption>
        <thead>
            <tr>
                <th scope="col">Column 1</th>
                <th scope="col">Column 2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Value</td>
                <td>Value</td>
            </tr>
        </tbody>
    </table>
</section>
```

---

## 7. Image / Figure Pattern

```html
<figure>
    <img src="image.jpg" alt="Describe what the image shows" width="500" height="300">
    <figcaption>Caption describing the image.</figcaption>
</figure>
```

**Rule:** `alt` describes meaning/purpose; use `alt=""` only for purely decorative images.

---

## 8. Article Pattern (standalone content)

```html
<article id="article-id">
    <h2>Heading</h2>
    <p>Self-contained content — notice, write-up, explanation.</p>
</article>
```

---

## 9. Multimedia Pattern

```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    Your browser does not support audio.
</audio>

<video controls width="500">
    <source src="video.mp4" type="video/mp4">
    <track src="captions.vtt" kind="captions" srclang="en" label="English">
    Your browser does not support video.
</video>
```

---

## 10. FAQ Pattern

```html
<section id="faq">
    <h2>Frequently Asked Questions</h2>
    <details>
        <summary>Question?</summary>
        <p>Answer.</p>
    </details>
    <details>
        <summary>Question?</summary>
        <p>Answer.</p>
    </details>
</section>
```

---

## 11. Aside Pattern

```html
<aside>
    <h2>Related / Side Content</h2>
    <ul>
        <li>Related item</li>
        <li>Related item</li>
    </ul>
</aside>
```

---

## 12. Form Pattern (contact / enroll / join)

```html
<section id="form-id">
    <h2>Form Heading</h2>
    <form action="/endpoint" method="post">

        <fieldset>
            <legend>Group 1 — Personal Info</legend>

            <p>
                <label for="name">Full Name</label><br>
                <input type="text" id="name" name="name" required minlength="3" maxlength="50">
            </p>

            <p>
                <label for="email">Email</label><br>
                <input type="email" id="email" name="email" required>
            </p>
        </fieldset>

        <fieldset>
            <legend>Group 2 — Choices</legend>

            <p>
                <label for="option">Select</label><br>
                <select id="option" name="option" required>
                    <option value="">Choose one</option>
                    <option value="a">Option A</option>
                    <option value="b">Option B</option>
                </select>
            </p>

            <label><input type="radio" name="mode" value="x" required> Choice X</label>
            <label><input type="radio" name="mode" value="y"> Choice Y</label>
        </fieldset>

        <fieldset>
            <legend>Group 3 — Extra</legend>
            <label><input type="checkbox" name="pref" value="a"> Preference A</label>
            <p>
                <label for="notes">Notes</label><br>
                <textarea id="notes" name="notes" rows="5" cols="40"></textarea>
            </p>
        </fieldset>

        <p>
            <label><input type="checkbox" name="terms" required> I agree to the terms and conditions.</label>
        </p>

        <button type="submit">Submit</button>
        <button type="reset">Reset</button>
    </form>
</section>
```

**Rules:**
- Every `<input>`/`<select>`/`<textarea>` has a matching `<label for="id">`.
- Group related fields with `<fieldset>` + `<legend>`.
- Use `required`, `minlength`, `maxlength`, `min`, `max`, `pattern` for validation — never rely on `placeholder` alone.
- Radios sharing a decision use the same `name`; checkboxes are independent.

---

## 13. Footer Block

```html
<footer id="contact">
    <h2>Contact</h2>
    <p>Email: <a href="mailto:someone@example.com">someone@example.com</a></p>
    <p>&copy; 2026 Site/Brand Name</p>
</footer>
```

---

## 14. Design Guidelines Summary (HTML-only stage)

1. **One skeleton, many pages** — header → nav → main (sections/article/aside) → footer works for a portfolio, an information portal, or a coaching site alike; only the content changes.
2. **IDs drive navigation** — every nav link must resolve to a real section `id`.
3. **Semantic first, `div` last** — reach for `section`/`article`/`aside`/`header`/`footer`/`nav` before a generic `div`.
4. **Every input needs a label** — no exceptions, even inside a `<fieldset>`.
5. **Every image needs alt text** — describe meaning, not decoration, unless purely decorative (`alt=""`).
6. **Tables need a caption + `th scope`** — for accessibility and clarity.
7. **Group form fields with `fieldset`/`legend`** — improves both structure and screen-reader experience.
8. **No styling decisions at this stage** — no colors, fonts, spacing, or layout; that is CSS's job, not HTML's.
9. **Validate structure, not appearance** — check nesting, closing tags, heading order, and semantic correctness before moving to CSS.

---

**Use this skeleton as the starting point for any new HTML-only page — copy Section 1 (Base Document Shell) first, then plug in the section patterns (2–13) as needed.**
