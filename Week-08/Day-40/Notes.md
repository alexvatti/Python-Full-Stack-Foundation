# DAY 4 — DAY 39

# HTML FINAL REVISION + ADVANCED HTML + COMPLETE HTML MINI PROJECT

## Front-End Development — Day 39

**Duration:** 1 Hour
**Level:** Beginner → Intermediate
**Module:** Front-End Development
**Topic:** HTML — Final Revision, Advanced HTML & Complete Mini Project
**Focus:** **HTML Only**

> **Day 39 = Final HTML Day**
>
> Today we complete the **HTML Foundation** through revision, advanced HTML details, accessibility refinement, and one complete HTML-only mini project.
>
> **CSS is NOT covered today.**
>
> Colours, fonts, styling, layout design, responsive design and visual presentation will be covered in the **CSS sessions**.

---

# 1. DAY 39 OBJECTIVES

By the end of Day 39, you should be able to:

* Understand the complete HTML architecture
* Build a complete HTML document from scratch
* Use semantic HTML correctly
* Create navigation structures
* Create forms with appropriate input types
* Apply HTML validation
* Embed images, audio and video
* Use `iframe`
* Create tables and lists
* Use global attributes correctly
* Understand accessibility basics
* Use `figure` and `figcaption`
* Use `details` and `summary`
* Understand `data-*` attributes
* Understand `meta` information
* Create a complete multi-section webpage using HTML only
* Separate **content/structure** from **presentation**

---

# 2. DAY 39 — 1 HOUR PLAN

| Time      | Topic                               |
| --------- | ----------------------------------- |
| 0–10 min  | Complete HTML Revision              |
| 10–20 min | Advanced HTML                       |
| 20–30 min | Accessibility + HTML Best Practices |
| 30–45 min | Complete HTML Mini Project          |
| 45–55 min | Project Review                      |
| 55–60 min | Final HTML Checklist                |

---

# 3. COMPLETE HTML ARCHITECTURE

```text
HTML
│
├── DOCUMENT
│   ├── <!DOCTYPE html>
│   ├── html
│   ├── head
│   └── body
│
├── HEAD
│   ├── title
│   ├── meta
│   ├── link
│   └── base
│
├── CONTENT
│   ├── Headings
│   ├── Paragraphs
│   ├── Text
│   ├── Links
│   ├── Images
│   ├── Lists
│   └── Tables
│
├── STRUCTURE
│   ├── header
│   ├── nav
│   ├── main
│   ├── section
│   ├── article
│   ├── aside
│   └── footer
│
├── FORMS
│   ├── form
│   ├── label
│   ├── input
│   ├── select
│   ├── option
│   ├── textarea
│   ├── button
│   ├── fieldset
│   └── legend
│
├── HTML5
│   ├── Semantic Elements
│   ├── New Input Types
│   ├── Audio
│   ├── Video
│   ├── Validation
│   ├── Details
│   ├── Summary
│   ├── Figure
│   └── Figcaption
│
├── EMBEDDING
│   ├── iframe
│   ├── audio
│   └── video
│
└── ACCESSIBILITY
    ├── Labels
    ├── Alt Text
    ├── Headings
    ├── Semantic HTML
    ├── Captions
    └── Keyboard Access
```

---

# 4. HTML DOCUMENT — FINAL REVISION

Every normal HTML page starts with a document structure.

```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>My HTML Page</title>

</head>

<body>

    <h1>Hello HTML</h1>

    <p>This is my webpage.</p>

</body>

</html>
```

---

# 5. `<!DOCTYPE html>`

```html
<!DOCTYPE html>
```

This tells the browser that the document uses modern HTML.

It should normally be the **first line** of the HTML document.

---

# 6. `<html>`

```html
<html lang="en">
```

The `<html>` element is the root element of the document.

The `lang` attribute identifies the language.

```html
<html lang="en">
```

For example:

```html
<html lang="en">
```

---

# 7. `<head>`

The `<head>` contains information **about the webpage**.

```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>Student Portal</title>

</head>
```

The `<head>` is not the main visible page content.

---

# 8. `<body>`

The `<body>` contains the webpage content.

```html
<body>

    <h1>Student Portal</h1>

    <p>Welcome to the student portal.</p>

</body>
```

---

# 9. HEADINGS

HTML provides six heading levels.

```html
<h1>Main Heading</h1>

<h2>Section Heading</h2>

<h3>Subsection</h3>

<h4>Subsection</h4>

<h5>Subsection</h5>

<h6>Subsection</h6>
```

Recommended structure:

```text
h1
│
├── h2
│   ├── h3
│   └── h3
│
├── h2
│   ├── h3
│   └── h3
```

Do not choose headings simply because they look large.

**Headings represent structure.**

---

# 10. PARAGRAPHS

```html
<p>
    HTML is used to structure content on the web.
</p>
```

---

# 11. TEXT ELEMENTS

```html
<strong>Important</strong>

<em>Emphasis</em>

<mark>Highlighted</mark>

<small>Small text</small>

<del>Deleted text</del>

<ins>Inserted text</ins>

<sub>Subscript</sub>

<sup>Superscript</sup>
```

Example:

```html
<p>
    HTML is <strong>important</strong>
    for web development.
</p>
```

---

# 12. LINKS

```html
<a href="https://example.com">
    Visit Website
</a>
```

Open in a new browsing context:

```html
<a href="https://example.com" target="_blank">
    Visit Website
</a>
```

For external links opened with a new browsing context, a safer modern pattern is:

```html
<a href="https://example.com"
   target="_blank"
   rel="noopener noreferrer">
    Visit Website
</a>
```

---

# 13. INTERNAL LINKS

```html
<a href="#about">
    About
</a>

<section id="about">

    <h2>About Us</h2>

    <p>
        Information about our organization.
    </p>

</section>
```

This creates navigation within the same page.

---

# 14. IMAGES

```html
<img src="student.jpg"
     alt="Student studying at a desk">
```

Important attributes:

```text
src
alt
width
height
```

Example:

```html
<img src="student.jpg"
     alt="Student studying at a desk"
     width="300"
     height="200">
```

---

# 15. IMAGE ACCESSIBILITY

Always provide meaningful alternative text when an image conveys information.

Good:

```html
<img src="college.jpg"
     alt="Main building of ABC College">
```

Decorative image:

```html
<img src="decoration.png"
     alt="">
```

The `alt` value should describe the **purpose or meaning** of the image.

---

# 16. FIGURE + FIGCAPTION

HTML5 provides:

```html
<figure>

    <img src="college.jpg"
         alt="ABC College main building">

    <figcaption>
        ABC College Main Building
    </figcaption>

</figure>
```

Use `<figure>` when the content is a self-contained illustration, image, diagram, code example, or similar content with an optional caption.

---

# 17. LISTS

## Unordered List

```html
<ul>

    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>

</ul>
```

## Ordered List

```html
<ol>

    <li>Learn HTML</li>
    <li>Learn CSS</li>
    <li>Learn JavaScript</li>

</ol>
```

## Description List

```html
<dl>

    <dt>HTML</dt>

    <dd>
        Structure of a webpage.
    </dd>

    <dt>CSS</dt>

    <dd>
        Presentation of a webpage.
    </dd>

</dl>
```

---

# 18. TABLES

Basic table:

```html
<table>

    <thead>

        <tr>
            <th>Name</th>
            <th>Course</th>
            <th>Score</th>
        </tr>

    </thead>

    <tbody>

        <tr>
            <td>Alex</td>
            <td>Python</td>
            <td>90</td>
        </tr>

        <tr>
            <td>John</td>
            <td>HTML</td>
            <td>85</td>
        </tr>

    </tbody>

</table>
```

Remember:

```text
table
│
├── thead
│   └── tr
│       └── th
│
└── tbody
    └── tr
        └── td
```

---

# 19. TABLE CAPTION

```html
<table>

    <caption>
        Student Results
    </caption>

    <thead>

        <tr>
            <th>Name</th>
            <th>Score</th>
        </tr>

    </thead>

    <tbody>

        <tr>
            <td>Alex</td>
            <td>90</td>
        </tr>

    </tbody>

</table>
```

A caption gives the table a meaningful title.

---

# 20. SEMANTIC HTML

Semantic elements describe the meaning of content.

```html
<header>
</header>

<nav>
</nav>

<main>
</main>

<section>
</section>

<article>
</article>

<aside>
</aside>

<footer>
</footer>
```

A typical page:

```text
<body>

    <header>
    </header>

    <nav>
    </nav>

    <main>

        <section>
        </section>

        <section>
        </section>

        <article>
        </article>

        <aside>
        </aside>

    </main>

    <footer>
    </footer>

</body>
```

---

# 21. HEADER

```html
<header>

    <h1>Training Portal</h1>

    <p>
        Learn modern web development.
    </p>

</header>
```

A header can represent the introductory content of a page or section.

---

# 22. NAV

```html
<nav>

    <a href="#home">Home</a>

    <a href="#courses">Courses</a>

    <a href="#about">About</a>

    <a href="#contact">Contact</a>

</nav>
```

`nav` identifies a section containing navigation links.

---

# 23. MAIN

```html
<main>

    <h1>HTML Course</h1>

    <p>
        Learn HTML from beginner to intermediate level.
    </p>

</main>
```

A page should normally have one primary `<main>` element.

---

# 24. SECTION

```html
<section>

    <h2>HTML Course</h2>

    <p>
        Learn HTML fundamentals.
    </p>

</section>
```

A section represents a thematic grouping of content.

---

# 25. ARTICLE

```html
<article>

    <h2>What is HTML?</h2>

    <p>
        HTML is the standard markup language
        used to structure web content.
    </p>

</article>
```

An article represents self-contained content.

Examples:

```text
Blog post
News article
Forum post
Course lesson
Product article
```

---

# 26. ASIDE

```html
<aside>

    <h2>Related Topics</h2>

    <ul>

        <li>CSS</li>
        <li>JavaScript</li>
        <li>Bootstrap</li>

    </ul>

</aside>
```

`aside` represents related or complementary content.

---

# 27. FOOTER

```html
<footer>

    <p>
        © 2026 Training Portal
    </p>

</footer>
```

---

# 28. DIV

```html
<div>

    <p>
        Generic container.
    </p>

</div>
```

`div` has no semantic meaning.

Use semantic elements when a meaningful semantic element exists.

Use `<div>` when you need a generic container.

---

# 29. SPAN

```html
<p>

    This is
    <span>important</span>
    information.

</p>
```

`span` is an inline generic container.

---

# 30. FORMS — FINAL REVISION

Basic form:

```html
<form>

    <label for="name">
        Name
    </label>

    <input type="text"
           id="name"
           name="name">

    <button type="submit">
        Submit
    </button>

</form>
```

---

# 31. LABEL + INPUT

Correct:

```html
<label for="email">
    Email
</label>

<input type="email"
       id="email"
       name="email">
```

The `for` value should match the input's `id`.

```text
label for
     ↓
    email
     ↑
 input id
```

This improves usability and accessibility.

---

# 32. IMPORTANT INPUT TYPES

```html
<input type="text">

<input type="email">

<input type="password">

<input type="number">

<input type="date">

<input type="time">

<input type="tel">

<input type="url">

<input type="search">

<input type="file">

<input type="checkbox">

<input type="radio">

<input type="range">

<input type="color">

<input type="hidden">

<input type="submit">

<input type="reset">
```

---

# 33. REQUIRED

```html
<input type="text"
       name="username"
       required>
```

The user must provide a value before submission.

---

# 34. PLACEHOLDER

```html
<input type="text"
       placeholder="Enter your name">
```

A placeholder is a hint.

It should **not replace a label**.

Correct:

```html
<label for="username">
    Username
</label>

<input type="text"
       id="username"
       name="username"
       placeholder="Enter your username">
```

---

# 35. MINLENGTH + MAXLENGTH

```html
<input type="text"
       minlength="3"
       maxlength="20">
```

---

# 36. MIN + MAX

```html
<input type="number"
       min="18"
       max="60">
```

---

# 37. PATTERN

```html
<input type="text"
       pattern="[A-Za-z]+"
       required>
```

The pattern provides a validation rule.

---

# 38. SELECT

```html
<label for="course">
    Select Course
</label>

<select id="course"
        name="course">

    <option value="python">
        Python
    </option>

    <option value="html">
        HTML
    </option>

    <option value="javascript">
        JavaScript
    </option>

</select>
```

---

# 39. TEXTAREA

```html
<label for="message">
    Message
</label>

<textarea id="message"
          name="message"
          rows="5"
          cols="40">
</textarea>
```

---

# 40. FIELDSET + LEGEND

Use these to group related form controls.

```html
<fieldset>

    <legend>
        Personal Information
    </legend>

    <label for="name">
        Name
    </label>

    <input type="text"
           id="name"
           name="name">

</fieldset>
```

---

# 41. RADIO BUTTONS

```html
<fieldset>

    <legend>
        Gender
    </legend>

    <label>
        <input type="radio"
               name="gender"
               value="male">

        Male
    </label>

    <label>
        <input type="radio"
               name="gender"
               value="female">

        Female
    </label>

</fieldset>
```

The same `name` groups radio buttons together.

---

# 42. CHECKBOX

```html
<label>

    <input type="checkbox"
           name="terms"
           required>

    I agree to the terms.

</label>
```

---

# 43. BUTTON

```html
<button type="submit">
    Submit
</button>
```

Other types:

```html
<button type="button">
    Click
</button>

<button type="reset">
    Reset
</button>
```

---

# 44. FORM METHOD

Forms commonly use:

```html
<form method="get">
```

or:

```html
<form method="post">
```

Example:

```html
<form action="/register"
      method="post">

    ...

</form>
```

The details of server-side processing will be covered later with **Flask**.

---

# 45. AUDIO

```html
<audio controls>

    <source src="lesson.mp3"
            type="audio/mpeg">

    Your browser does not support audio.

</audio>
```

---

# 46. VIDEO

```html
<video controls
       width="600">

    <source src="lesson.mp4"
            type="video/mp4">

    Your browser does not support video.

</video>
```

---

# 47. VIDEO WITH CAPTIONS

Accessibility can be improved by providing captions.

```html
<video controls>

    <source src="lesson.mp4"
            type="video/mp4">

    <track src="captions.vtt"
           kind="captions"
           srclang="en"
           label="English">

</video>
```

---

# 48. IFRAME

An iframe embeds another document or external resource.

```html
<iframe
    src="https://example.com"
    title="Example Website">
</iframe>
```

The `title` attribute is important for accessibility.

---

# 49. DETAILS + SUMMARY

HTML provides a built-in expandable section.

```html
<details>

    <summary>
        What is HTML?
    </summary>

    <p>
        HTML is used to structure
        content on the web.
    </p>

</details>
```

The browser provides the interactive open/close behavior.

---

# 50. ADVANCED HTML — DIALOG

HTML provides the `<dialog>` element for dialog interfaces.

```html
<dialog open>

    <h2>Welcome</h2>

    <p>
        This is a dialog.
    </p>

</dialog>
```

JavaScript can later be used to control dialog behavior.

**JavaScript will be covered separately.**

---

# 51. DATA ATTRIBUTES

HTML allows custom data attributes beginning with:

```text
data-
```

Example:

```html
<button
    data-course="python"
    data-level="beginner">

    Python Course

</button>
```

These attributes can later be accessed using JavaScript.

For example:

```text
data-course
data-level
```

are custom data attributes.

---

# 52. GLOBAL ATTRIBUTES

Global attributes can be used on many HTML elements.

Important examples:

```text
id
class
title
lang
dir
hidden
data-*
tabindex
contenteditable
draggable
spellcheck
```

---

# 53. ID

```html
<section id="about">

    <h2>About</h2>

</section>
```

An `id` should identify a particular element.

A page should not normally contain multiple elements with the same `id`.

---

# 54. CLASS

```html
<p class="important">
    Important information.
</p>
```

Multiple elements can share the same class.

```html
<p class="important">
    First
</p>

<p class="important">
    Second
</p>
```

CSS will use classes heavily in the next stage.

---

# 55. TITLE

```html
<button title="Submit your application">
    Submit
</button>
```

The `title` attribute can provide supplementary information.

Do not use it as a replacement for visible labels or accessible names.

---

# 56. HIDDEN

```html
<p hidden>
    This content is hidden.
</p>
```

The `hidden` attribute indicates that the content is not currently relevant or intended to be presented.

---

# 57. TABINDEX

```html
<button tabindex="0">
    Continue
</button>
```

Keyboard navigation should generally follow a logical order.

Avoid using positive `tabindex` values unnecessarily.

---

# 58. ACCESSIBILITY — FINAL REVISION

Accessibility means making webpages usable by as many people as possible, including people using:

```text
Keyboard
Screen readers
Voice control
Magnification
Assistive technologies
```

---

# 59. ACCESSIBILITY RULE 1 — USE SEMANTIC HTML

Prefer:

```html
<button>
    Submit
</button>
```

instead of:

```html
<div>
    Submit
</div>
```

A button communicates its purpose to browsers and assistive technologies.

---

# 60. ACCESSIBILITY RULE 2 — LABEL FORM CONTROLS

Good:

```html
<label for="email">
    Email Address
</label>

<input type="email"
       id="email"
       name="email">
```

---

# 61. ACCESSIBILITY RULE 3 — ALT TEXT

Good:

```html
<img src="college.jpg"
     alt="ABC College main entrance">
```

Avoid:

```html
<img src="college.jpg">
```

when the image conveys meaningful information.

---

# 62. ACCESSIBILITY RULE 4 — HEADING STRUCTURE

Use headings logically.

```text
h1
│
├── h2
│   ├── h3
│   └── h3
│
└── h2
    ├── h3
    └── h3
```

Do not use headings merely to make text visually larger.

---

# 63. ACCESSIBILITY RULE 5 — KEYBOARD ACCESS

Interactive elements should be keyboard accessible.

Native HTML controls are generally the best starting point:

```html
<button>
    Submit
</button>

<a href="about.html">
    About
</a>

<input type="text">
```

Avoid creating fake controls with generic elements.

---

# 64. ACCESSIBILITY RULE 6 — VIDEO CAPTIONS

For video content containing speech:

```html
<track kind="captions">
```

can provide captions.

---

# 65. HTML BEST PRACTICES

## Practice 1

Use semantic elements.

```html
<header>
<nav>
<main>
<section>
<article>
<footer>
```

instead of using `<div>` for everything.

---

## Practice 2

Use meaningful names.

Good:

```html
id="student-registration"
```

Less meaningful:

```html
id="x1"
```

---

## Practice 3

Use lowercase HTML element names.

Preferred:

```html
<section>
```

---

## Practice 4

Indent your HTML.

Good:

```html
<section>

    <h2>Courses</h2>

    <p>
        Learn Python.
    </p>

</section>
```

---

## Practice 5

Use quotes around attribute values.

Preferred:

```html
<input type="text" name="username">
```

---

## Practice 6

Close elements correctly.

```html
<p>
    Hello
</p>
```

---

# 66. HTML IS NOT CSS

This distinction is extremely important.

HTML:

```text
Structure
Content
Meaning
Semantics
Accessibility
```

CSS:

```text
Colors
Fonts
Spacing
Borders
Layout
Responsive Design
Animation
Visual Design
```

Therefore, today:

```text
HTML
  ↓
Structure + Content
```

Next:

```text
CSS
  ↓
Presentation + Design
```

---

# 67. HTML VS CSS VS JAVASCRIPT

```text
WEB PAGE
   │
   ├── HTML
   │     ↓
   │   Structure
   │   Content
   │   Meaning
   │
   ├── CSS
   │     ↓
   │   Appearance
   │   Layout
   │   Responsive Design
   │
   └── JavaScript
         ↓
       Behavior
       Interaction
       DOM
       Events
```

Think:

```text
HTML       = Skeleton
CSS        = Appearance
JavaScript = Behavior
```

---

# 68. COMPLETE HTML MINI PROJECT

## Project: STUDENT TRAINING PORTAL

Today we will build a complete webpage using **HTML only**.

The project will contain:

```text
Student Training Portal
│
├── Header
├── Navigation
├── Main
│   ├── Welcome Section
│   ├── About Section
│   ├── Courses Section
│   ├── Course Table
│   ├── Learning Article
│   ├── FAQ
│   └── Registration Form
│
├── Aside
│
└── Footer
```

---

# 69. PROJECT REQUIREMENTS

The page should contain:

* Document structure
* Metadata
* Header
* Navigation
* Main content
* Sections
* Article
* Aside
* Footer
* Headings
* Paragraphs
* Links
* Lists
* Image
* Figure
* Table
* Form
* Validation
* Radio buttons
* Checkboxes
* Select
* Textarea
* Audio
* Video
* FAQ
* Semantic HTML
* Accessibility features

---

# 70. COMPLETE HTML PROJECT

```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <meta name="description"
          content="Student Training Portal for learning programming and web development">

    <meta name="author"
          content="Training and Placement">

    <title>Student Training Portal</title>

</head>

<body>

    <!-- ========================= -->
    <!-- HEADER -->
    <!-- ========================= -->

    <header id="home">

        <h1>Student Training Portal</h1>

        <p>
            Learn Programming, Web Development and Technology.
        </p>

    </header>


    <!-- ========================= -->
    <!-- NAVIGATION -->
    <!-- ========================= -->

    <nav aria-label="Main Navigation">

        <a href="#home">
            Home
        </a>

        <a href="#about">
            About
        </a>

        <a href="#courses">
            Courses
        </a>

        <a href="#learning">
            Learning
        </a>

        <a href="#register">
            Register
        </a>

        <a href="#contact">
            Contact
        </a>

    </nav>


    <!-- ========================= -->
    <!-- MAIN -->
    <!-- ========================= -->

    <main>


        <!-- ========================= -->
        <!-- WELCOME -->
        <!-- ========================= -->

        <section>

            <h2>
                Welcome to the Training Portal
            </h2>

            <p>
                This portal helps students learn
                programming and modern technology.
            </p>

            <p>
                Our learning path starts with
                fundamentals and gradually moves
                toward real-world development.
            </p>

        </section>


        <!-- ========================= -->
        <!-- ABOUT -->
        <!-- ========================= -->

        <section id="about">

            <h2>
                About the Portal
            </h2>

            <p>
                The Student Training Portal provides
                structured learning resources for
                students and beginners.
            </p>

            <h3>
                Our Learning Approach
            </h3>

            <ol>

                <li>
                    Learn the fundamentals
                </li>

                <li>
                    Practice concepts
                </li>

                <li>
                    Solve problems
                </li>

                <li>
                    Build projects
                </li>

                <li>
                    Prepare for careers
                </li>

            </ol>

        </section>


        <!-- ========================= -->
        <!-- IMAGE / FIGURE -->
        <!-- ========================= -->

        <section>

            <h2>
                Learning Environment
            </h2>

            <figure>

                <img src="training.jpg"
                     alt="Students learning programming in a classroom"
                     width="500"
                     height="300">

                <figcaption>
                    Students learning programming
                    and technology.
                </figcaption>

            </figure>

        </section>


        <!-- ========================= -->
        <!-- COURSES -->
        <!-- ========================= -->

        <section id="courses">

            <h2>
                Our Courses
            </h2>

            <ul>

                <li>
                    HTML
                </li>

                <li>
                    CSS
                </li>

                <li>
                    JavaScript
                </li>

                <li>
                    Python
                </li>

                <li>
                    Flask
                </li>

                <li>
                    Database
                </li>

            </ul>

        </section>


        <!-- ========================= -->
        <!-- COURSE TABLE -->
        <!-- ========================= -->

        <section>

            <h2>
                Course Schedule
            </h2>

            <table>

                <caption>
                    Student Training Schedule
                </caption>

                <thead>

                    <tr>

                        <th scope="col">
                            Course
                        </th>

                        <th scope="col">
                            Duration
                        </th>

                        <th scope="col">
                            Level
                        </th>

                    </tr>

                </thead>

                <tbody>

                    <tr>

                        <td>
                            HTML
                        </td>

                        <td>
                            4 Days
                        </td>

                        <td>
                            Beginner
                        </td>

                    </tr>

                    <tr>

                        <td>
                            CSS
                        </td>

                        <td>
                            5 Days
                        </td>

                        <td>
                            Beginner
                        </td>

                    </tr>

                    <tr>

                        <td>
                            JavaScript
                        </td>

                        <td>
                            10 Days
                        </td>

                        <td>
                            Beginner → Intermediate
                        </td>

                    </tr>

                    <tr>

                        <td>
                            Python
                        </td>

                        <td>
                            15 Days
                        </td>

                        <td>
                            Beginner → Intermediate
                        </td>

                    </tr>

                </tbody>

            </table>

        </section>


        <!-- ========================= -->
        <!-- ARTICLE -->
        <!-- ========================= -->

        <article id="learning">

            <h2>
                Why Learn HTML?
            </h2>

            <p>
                HTML is the foundation of web development.
                It defines the structure and meaning of
                content displayed by web browsers.
            </p>

            <p>
                HTML is used together with CSS and
                JavaScript to create modern web applications.
            </p>

            <h3>
                HTML Learning Path
            </h3>

            <ul>

                <li>
                    Document Structure
                </li>

                <li>
                    Text and Content
                </li>

                <li>
                    Links and Images
                </li>

                <li>
                    Lists and Tables
                </li>

                <li>
                    Forms
                </li>

                <li>
                    Semantic HTML
                </li>

                <li>
                    Accessibility
                </li>

            </ul>

        </article>


        <!-- ========================= -->
        <!-- MULTIMEDIA -->
        <!-- ========================= -->

        <section>

            <h2>
                Learning Resources
            </h2>

            <h3>
                Audio Lesson
            </h3>

            <audio controls>

                <source src="lesson.mp3"
                        type="audio/mpeg">

                Your browser does not support audio.

            </audio>


            <h3>
                Video Lesson
            </h3>

            <video controls
                   width="500">

                <source src="lesson.mp4"
                        type="video/mp4">

                <track src="captions.vtt"
                       kind="captions"
                       srclang="en"
                       label="English">

                Your browser does not support video.

            </video>

        </section>


        <!-- ========================= -->
        <!-- FAQ -->
        <!-- ========================= -->

        <section>

            <h2>
                Frequently Asked Questions
            </h2>

            <details>

                <summary>
                    What is HTML?
                </summary>

                <p>
                    HTML is the markup language
                    used to structure content on the web.
                </p>

            </details>


            <details>

                <summary>
                    Do I need CSS to learn HTML?
                </summary>

                <p>
                    No. HTML can be learned independently
                    as the foundation of web development.
                </p>

            </details>


            <details>

                <summary>
                    What comes after HTML?
                </summary>

                <p>
                    CSS is the next major frontend
                    technology for styling and layout.
                </p>

            </details>

        </section>


        <!-- ========================= -->
        <!-- REGISTRATION FORM -->
        <!-- ========================= -->

        <section id="register">

            <h2>
                Student Registration
            </h2>

            <form action="/register"
                  method="post">


                <!-- PERSONAL INFORMATION -->

                <fieldset>

                    <legend>
                        Personal Information
                    </legend>


                    <p>

                        <label for="name">
                            Full Name
                        </label>

                        <br>

                        <input type="text"
                               id="name"
                               name="name"
                               placeholder="Enter your full name"
                               required
                               minlength="3"
                               maxlength="50">

                    </p>


                    <p>

                        <label for="email">
                            Email Address
                        </label>

                        <br>

                        <input type="email"
                               id="email"
                               name="email"
                               placeholder="Enter your email"
                               required>

                    </p>


                    <p>

                        <label for="phone">
                            Phone Number
                        </label>

                        <br>

                        <input type="tel"
                               id="phone"
                               name="phone"
                               placeholder="Enter phone number"
                               required>

                    </p>


                    <p>

                        <label for="birthdate">
                            Date of Birth
                        </label>

                        <br>

                        <input type="date"
                               id="birthdate"
                               name="birthdate">

                    </p>

                </fieldset>


                <!-- COURSE INFORMATION -->

                <fieldset>

                    <legend>
                        Course Information
                    </legend>


                    <p>

                        <label for="course">
                            Select Course
                        </label>

                        <br>

                        <select id="course"
                                name="course"
                                required>

                            <option value="">
                                Select a course
                            </option>

                            <option value="html">
                                HTML
                            </option>

                            <option value="css">
                                CSS
                            </option>

                            <option value="javascript">
                                JavaScript
                            </option>

                            <option value="python">
                                Python
                            </option>

                            <option value="flask">
                                Flask
                            </option>

                        </select>

                    </p>


                    <p>

                        <strong>
                            Learning Mode
                        </strong>

                    </p>


                    <label>

                        <input type="radio"
                               name="mode"
                               value="online"
                               required>

                        Online

                    </label>


                    <label>

                        <input type="radio"
                               name="mode"
                               value="offline">

                        Offline

                    </label>

                </fieldset>


                <!-- SKILLS -->

                <fieldset>

                    <legend>
                        Existing Skills
                    </legend>


                    <label>

                        <input type="checkbox"
                               name="skills"
                               value="html">

                        HTML

                    </label>


                    <label>

                        <input type="checkbox"
                               name="skills"
                               value="python">

                        Python

                    </label>


                    <label>

                        <input type="checkbox"
                               name="skills"
                               value="database">

                        Database

                    </label>

                </fieldset>


                <!-- MESSAGE -->

                <fieldset>

                    <legend>
                        Additional Information
                    </legend>


                    <p>

                        <label for="message">
                            Tell us about your goals
                        </label>

                        <br>

                        <textarea id="message"
                                  name="message"
                                  rows="6"
                                  cols="50"
                                  placeholder="Enter your learning goals">
                        </textarea>

                    </p>

                </fieldset>


                <!-- TERMS -->

                <p>

                    <label>

                        <input type="checkbox"
                               name="terms"
                               required>

                        I agree to the terms
                        and conditions.

                    </label>

                </p>


                <!-- BUTTONS -->

                <button type="submit">
                    Register
                </button>


                <button type="reset">
                    Reset
                </button>


            </form>

        </section>


        <!-- ========================= -->
        <!-- ASIDE -->
        <!-- ========================= -->

        <aside>

            <h2>
                Recommended Skills
            </h2>

            <ul>

                <li>
                    Problem Solving
                </li>

                <li>
                    Programming
                </li>

                <li>
                    Communication
                </li>

                <li>
                    Database
                </li>

                <li>
                    Git
                </li>

            </ul>

        </aside>


    </main>


    <!-- ========================= -->
    <!-- FOOTER -->
    <!-- ========================= -->

    <footer id="contact">

        <h2>
            Contact
        </h2>

        <p>
            Email:
            <a href="mailto:training@example.com">
                training@example.com
            </a>
        </p>

        <p>
            © 2026 Student Training Portal
        </p>

    </footer>


</body>

</html>
```

---

# 71. PROJECT ARCHITECTURE

The complete project now looks like:

```text
Student Training Portal
│
├── DOCTYPE
│
├── HTML
│   │
│   ├── HEAD
│   │   ├── charset
│   │   ├── viewport
│   │   ├── description
│   │   ├── author
│   │   └── title
│   │
│   └── BODY
│       │
│       ├── HEADER
│       │
│       ├── NAV
│       │
│       ├── MAIN
│       │   │
│       │   ├── Welcome Section
│       │   ├── About Section
│       │   ├── Figure
│       │   ├── Courses
│       │   ├── Table
│       │   ├── Article
│       │   ├── Multimedia
│       │   ├── FAQ
│       │   ├── Registration Form
│       │   └── Aside
│       │
│       └── FOOTER
│
└── END
```

---

# 72. WHAT HAVE WE USED?

| HTML Area          | Used |
| ------------------ | ---: |
| Document Structure |    ✅ |
| `doctype`          |    ✅ |
| `html`             |    ✅ |
| `head`             |    ✅ |
| `meta`             |    ✅ |
| `title`            |    ✅ |
| Headings           |    ✅ |
| Paragraphs         |    ✅ |
| Links              |    ✅ |
| Images             |    ✅ |
| Figure             |    ✅ |
| Figcaption         |    ✅ |
| Lists              |    ✅ |
| Tables             |    ✅ |
| Header             |    ✅ |
| Nav                |    ✅ |
| Main               |    ✅ |
| Section            |    ✅ |
| Article            |    ✅ |
| Aside              |    ✅ |
| Footer             |    ✅ |
| Forms              |    ✅ |
| Labels             |    ✅ |
| Text Inputs        |    ✅ |
| Email              |    ✅ |
| Telephone          |    ✅ |
| Date               |    ✅ |
| Select             |    ✅ |
| Option             |    ✅ |
| Textarea           |    ✅ |
| Radio              |    ✅ |
| Checkbox           |    ✅ |
| Fieldset           |    ✅ |
| Legend             |    ✅ |
| Validation         |    ✅ |
| Audio              |    ✅ |
| Video              |    ✅ |
| Track/Captions     |    ✅ |
| Details            |    ✅ |
| Summary            |    ✅ |
| Global Attributes  |    ✅ |
| Accessibility      |    ✅ |

---

# 73. HTML VALIDATION CHECK

Before considering your HTML complete, check:

```text
[ ] <!DOCTYPE html>
[ ] <html lang="en">
[ ] <head>
[ ] charset
[ ] viewport
[ ] title
[ ] <body>
[ ] Logical heading structure
[ ] Semantic elements
[ ] Meaningful links
[ ] Alt text
[ ] Form labels
[ ] Form validation
[ ] Accessible buttons
[ ] Table headings
[ ] Table caption
[ ] Video captions where applicable
[ ] Keyboard-accessible controls
[ ] No unnecessary div elements
[ ] Proper nesting
[ ] Proper closing tags
```

---

# 74. HTML REVISION — ONE VIEW

```text
HTML
│
├── DOCUMENT
│   ├── doctype
│   ├── html
│   ├── head
│   └── body
│
├── HEAD
│   ├── meta
│   ├── title
│   └── link
│
├── CONTENT
│   ├── h1-h6
│   ├── p
│   ├── strong
│   ├── em
│   ├── mark
│   ├── a
│   ├── img
│   ├── ul
│   ├── ol
│   ├── dl
│   └── table
│
├── SEMANTIC
│   ├── header
│   ├── nav
│   ├── main
│   ├── section
│   ├── article
│   ├── aside
│   └── footer
│
├── FORMS
│   ├── form
│   ├── label
│   ├── input
│   ├── select
│   ├── option
│   ├── textarea
│   ├── button
│   ├── fieldset
│   └── legend
│
├── MULTIMEDIA
│   ├── audio
│   ├── video
│   ├── track
│   └── iframe
│
├── ADVANCED
│   ├── figure
│   ├── figcaption
│   ├── details
│   ├── summary
│   ├── dialog
│   └── data-*
│
└── ACCESSIBILITY
    ├── semantic HTML
    ├── labels
    ├── alt
    ├── headings
    ├── captions
    └── keyboard access
```

---

# 75. HTML → CSS → JAVASCRIPT → FLASK

Your frontend learning architecture is now:

```text
                    FRONT END
                       │
                       ▼
                    HTML
                       │
              Structure + Meaning
                       │
                       ▼
                     CSS
                       │
              Design + Layout
                       │
                       ▼
                 JavaScript
                       │
              Behavior + Events
                       │
                       ▼
                    Flask
                       │
          Backend + Routes + Templates
                       │
                       ▼
                   Database
```

---

# 76. IMPORTANT — DO NOT MIX THE LAYERS

For this HTML stage, concentrate on:

```text
What content exists?
        ↓
How is it structured?
        ↓
What does the content mean?
        ↓
How can users access it?
```

Do **not** worry yet about:

```text
Colors
Fonts
Backgrounds
Borders
Margins
Padding
Flexbox
Grid
Responsive layouts
Animations
```

Those belong primarily to **CSS**.

---

# 77. DAY 39 PRACTICE TASK

Create your own HTML-only page:

## **"My Learning Portfolio"**

It must contain:

```text
1. Header
2. Navigation
3. About Me
4. Skills
5. Education
6. Projects
7. Project Table
8. Learning Article
9. FAQ
10. Registration/Contact Form
11. Footer
```

Use at least:

```text
3 semantic elements
2 lists
1 table
1 image
1 figure
1 article
1 aside
1 form
3 different input types
1 select
1 textarea
1 fieldset
1 details/summary
```

---

# 78. DAY 39 CHALLENGE

Build the page **without looking at the complete project above**.

Start with:

```html
<!DOCTYPE html>
<html lang="en">

<head>

</head>

<body>

</body>

</html>
```

Then build the page yourself.

The goal is not memorization.

The goal is:

> **Can I design and structure a complete webpage using HTML from scratch?**

---

# 79. FINAL HTML TEST

Answer these without looking at your notes:

### Q1

What is the purpose of HTML?

### Q2

What is the difference between:

```html
<div>
```

and:

```html
<section>
```

### Q3

Why is `alt` important?

### Q4

Why should form controls have labels?

### Q5

What is the difference between:

```html
id
```

and:

```html
class
```

### Q6

What is the purpose of:

```html
<header>
<nav>
<main>
<footer>
```

### Q7

What is the purpose of:

```html
<fieldset>
<legend>
```

### Q8

What is the difference between:

```html
GET
```

and:

```html
POST
```

at a high level?

### Q9

What does `required` do?

### Q10

Why should HTML structure be separated from CSS presentation?

---

# 80. DAY 39 FINAL CHECKPOINT

After completing Day 39:

```text
HTML FOUNDATION              ✅
HTML DOCUMENT                ✅
HTML CONTENT                 ✅
HTML TEXT                    ✅
HTML LINKS                   ✅
HTML IMAGES                  ✅
HTML FIGURES                 ✅
HTML LISTS                   ✅
HTML TABLES                  ✅
HTML PATHS                   ✅
HTML SEMANTIC                ✅
HTML FORMS                   ✅
HTML INPUTS                  ✅
HTML VALIDATION              ✅
HTML MULTIMEDIA              ✅
HTML AUDIO                   ✅
HTML VIDEO                   ✅
HTML IFRAME                  ✅
HTML5 FEATURES               ✅
HTML GLOBAL ATTRIBUTES       ✅
HTML ACCESSIBILITY           ✅
HTML BEST PRACTICES          ✅
HTML MINI PROJECT            ✅
HTML REVISION                ✅
```

---

# 81. HTML COMPLETION STATUS

```text
             HTML
              │
              ▼
       ┌───────────────┐
       │   FOUNDATION  │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │    CONTENT    │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │   STRUCTURE   │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │     FORMS     │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │    HTML5      │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │ ACCESSIBILITY │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │ MINI PROJECT  │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │ HTML COMPLETE │
       └───────────────┘
```

---

# 82. FINAL ARCHITECTURE

```text
FRONT END DEVELOPMENT
│
├── HTML
│   │
│   ├── Structure
│   ├── Content
│   ├── Links
│   ├── Images
│   ├── Lists
│   ├── Tables
│   ├── Forms
│   ├── Multimedia
│   ├── Semantic HTML
│   ├── HTML5
│   └── Accessibility
│
├── CSS
│   ↓
│   Presentation
│   Colors
│   Fonts
│   Layout
│   Responsive Design
│
├── JavaScript
│   ↓
│   Behavior
│   Events
│   DOM
│   API
│
└── Flask
    ↓
    Backend
    Routes
    Templates
    Forms
    Database
```

---

# DAY 39 — HTML COMPLETE

> **HTML is now complete as the first layer of Front-End Development.**

```text
DAY 36
HTML Fundamentals
        ↓
DAY 37
HTML Content + Structure
        ↓
DAY 38
Forms + HTML5 + Multimedia
        ↓
DAY 39
Final Revision
+ Advanced HTML
+ Accessibility
+ Mini Project
        ↓
     HTML ✅
        ↓
      CSS 🚀
```

---

# NEXT MODULE

# CSS — FRONT-END PRESENTATION

The next sessions will move from:

```text
HTML
Structure
Content
Meaning
```

to:

```text
CSS
│
├── Selectors
├── Properties
├── Values
├── Colors
├── Text
├── Fonts
├── Backgrounds
├── Borders
├── Box Model
├── Margin
├── Padding
├── Width / Height
├── Display
├── Position
├── Flexbox
├── Grid
├── Responsive Design
└── Complete CSS Project
```

**Day 39 = Final HTML Day. HTML is complete. Next stage: CSS.**
