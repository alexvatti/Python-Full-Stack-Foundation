# DAY 2 — HTML CONTENT, LINKS, IMAGES, LISTS, TABLES, PATHS, DIV, SPAN & SEMANTIC HTML

## Front-End Development — Day 37

**Duration:** 1 Hour  
**Level:** Beginner → Intermediate  
**Module:** Front-End Development  
**Topic:** HTML — Content & Structure  
**Focus:** HTML Only

> **Day 37 = HTML Content**
>
> CSS, JavaScript and Flask are intentionally not covered today.

---

# 1. Day 2 Objective

By the end of Day 2, you should be able to create a meaningful multi-page HTML website using:

```text
Links
Images
Lists
Tables
File Paths
div
span
Semantic HTML
Navigation
Sections
Articles
Headers
Footers
```

The goal is to move from:

```text
Basic HTML Page
```

to:

```text
Structured HTML Website
```

---

# 2. Day 1 → Day 2 Connection

In Day 1 we learned:

```text
HTML
↓
Document Structure
↓
html
head
body
↓
Tags
Elements
Attributes
Nesting
↓
Headings
Paragraphs
Text
```

Today we build actual website content:

```text
HTML
│
├── Links
├── Images
├── Lists
├── Tables
├── Paths
├── div
├── span
│
└── Semantic HTML
    ├── header
    ├── nav
    ├── main
    ├── section
    ├── article
    ├── aside
    └── footer
```

---

# 3. Why Do We Need More HTML Elements?

A real website contains more than:

```html
<h1>
<p>
<h2>
```

For example:

```text
College Website
│
├── Home
├── About
├── Courses
├── Students
├── Contact
│
├── Course Information
├── Student Information
├── Images
├── Tables
└── Footer
```

HTML provides elements to represent these different types of content.

---

# 4. HTML Links

The HTML link element is:

```html
<a>
```

`a` represents an anchor.

Example:

```html
<a href="about.html">
    About Us
</a>
```

The user can click the link.

---

# 5. The `href` Attribute

The most important attribute of an anchor is:

```html
href
```

Example:

```html
<a href="about.html">
    About
</a>
```

Here:

```text
a
│
├── href
│   └── about.html
│
└── About
```

---

# 6. Link to Another HTML Page

Suppose the folder contains:

```text
website/
│
├── index.html
├── about.html
└── contact.html
```

From `index.html`:

```html
<a href="about.html">
    About
</a>

<a href="contact.html">
    Contact
</a>
```

---

# 7. Navigation Using Links

Example:

```html
<nav>

    <a href="index.html">Home</a>

    <a href="about.html">About</a>

    <a href="courses.html">Courses</a>

    <a href="contact.html">Contact</a>

</nav>
```

This creates the structural navigation of a website.

CSS will later control its appearance.

---

# 8. Absolute URLs

A link can point to another website.

Example:

```html
<a href="https://www.example.com">
    Example
</a>
```

This is an external or absolute URL.

The complete address is specified.

---

# 9. Relative URLs

A relative URL points to a resource relative to the current page.

Example:

```html
<a href="about.html">
    About
</a>
```

If:

```text
index.html
about.html
```

are in the same folder, this works as a relative path.

---

# 10. Opening a Link in a New Browsing Context

Example:

```html
<a
    href="https://www.example.com"
    target="_blank">
    Visit Example
</a>
```

The `target` attribute controls where the linked document is opened.

Common value:

```html
target="_blank"
```

---

# 11. `rel` Attribute with External New-Tab Links

When using:

```html
target="_blank"
```

it is good practice to use:

```html
rel="noopener"
```

Example:

```html
<a
    href="https://www.example.com"
    target="_blank"
    rel="noopener">
    Example
</a>
```

This is especially useful for security and browsing-context isolation.

---

# 12. Email Links

HTML can create a link that opens the user's email application.

Example:

```html
<a href="mailto:admin@example.com">
    Email Admin
</a>
```

The scheme is:

```text
mailto:
```

---

# 13. Telephone Links

A telephone link can be written as:

```html
<a href="tel:+911234567890">
    Call Us
</a>
```

The scheme is:

```text
tel:
```

This is particularly useful on mobile devices.

---

# 14. Link to a Section on the Same Page

Suppose:

```html
<h2 id="courses">
    Courses
</h2>
```

A link can point to it:

```html
<a href="#courses">
    Go to Courses
</a>
```

The `#` refers to an element ID on the current page.

---

# 15. The `id` Attribute

Example:

```html
<h2 id="courses">
    Courses
</h2>
```

The value is:

```text
courses
```

A link can reference it:

```html
<a href="#courses">
    Courses
</a>
```

Conceptually:

```text
<a href="#courses">
        |
        v
<h2 id="courses">
```

---

# 16. ID Values

An `id` identifies an element within a document.

Example:

```html
<section id="about">
```

Another:

```html
<section id="courses">
```

Another:

```html
<section id="contact">
```

IDs should be meaningful and unique within the document.

---

# 17. Image Element

The image element is:

```html
<img>
```

Example:

```html
<img
    src="student.jpg"
    alt="Student">
```

---

# 18. The `src` Attribute

`src` specifies the image resource.

Example:

```html
<img src="student.jpg">
```

Here:

```text
src
↓
student.jpg
```

---

# 19. The `alt` Attribute

`alt` provides alternative text for an image.

Example:

```html
<img
    src="student.jpg"
    alt="Student profile photo">
```

The alternative text is useful when:

- The image cannot be loaded.
- A screen reader is interpreting the page.
- The image conveys important information.

---

# 20. Decorative Images

If an image is purely decorative and conveys no information, the alternative text can be empty:

```html
<img
    src="decoration.png"
    alt="">
```

Do not use meaningless text such as:

```html
alt="image"
```

when the image has no informational value.

---

# 21. Image Width and Height Attributes

HTML can specify intrinsic display dimensions:

```html
<img
    src="student.jpg"
    alt="Student"
    width="300"
    height="200">
```

These attributes describe the image's displayed dimensions.

Later, CSS will provide more flexible responsive control.

---

# 22. Image Is a Void Element

The `<img>` element does not have normal content or a closing tag.

Correct:

```html
<img src="photo.jpg" alt="Photo">
```

Do not write:

```html
<img>
    ...
</img>
```

---

# 23. Image File Structure

Suppose:

```text
website/
│
├── index.html
│
└── images/
    ├── student.jpg
    ├── college.jpg
    └── logo.png
```

From `index.html`:

```html
<img
    src="images/student.jpg"
    alt="Student">
```

---

# 24. Image in the Same Folder

If:

```text
website/
│
├── index.html
└── student.jpg
```

Use:

```html
<img
    src="student.jpg"
    alt="Student">
```

---

# 25. Parent Folder Path

Suppose:

```text
website/
│
├── index.html
│
└── pages/
    └── about.html
```

From:

```text
pages/about.html
```

to:

```text
index.html
```

use:

```html
<a href="../index.html">
    Home
</a>
```

`..` means:

```text
Parent directory
```

---

# 26. Nested Folder Path

Suppose:

```text
website/
│
├── index.html
│
└── images/
    └── students/
        └── student.jpg
```

From `index.html`:

```html
<img
    src="images/students/student.jpg"
    alt="Student">
```

---

# 27. Understanding `./`

`./` refers to the current directory.

Example:

```html
<a href="./about.html">
    About
</a>
```

This points to:

```text
about.html
```

in the current directory.

In many simple cases:

```html
<a href="about.html">
```

is equivalent.

---

# 28. Understanding `../`

`../` means:

```text
Go up one directory.
```

Example:

```html
<a href="../index.html">
    Home
</a>
```

If the current file is inside:

```text
pages/
```

then:

```text
../
```

moves to the parent directory.

---

# 29. Path Mental Model

Remember:

```text
./
↓
Current folder

../
↓
Parent folder

folder/
↓
Child folder
```

Example:

```text
website/
│
├── index.html
│
├── pages/
│   └── about.html
│
└── images/
    └── logo.png
```

From `about.html`:

```html
<a href="../index.html">
    Home
</a>
```

From `about.html`:

```html
<img
    src="../images/logo.png"
    alt="Logo">
```

---

# 30. HTML Lists

HTML provides lists for grouped information.

Main types:

```text
Unordered List
Ordered List
Description List
```

---

# 31. Unordered List

Use:

```html
<ul>
```

Each item uses:

```html
<li>
```

Example:

```html
<ul>

    <li>HTML</li>

    <li>CSS</li>

    <li>JavaScript</li>

</ul>
```

---

# 32. `<ul>` Meaning

`ul` means:

```text
Unordered List
```

The order of items is not the primary meaning.

Example:

```html
<ul>
    <li>Python</li>
    <li>Java</li>
    <li>C++</li>
</ul>
```

---

# 33. `<li>` Meaning

`li` means:

```text
List Item
```

Example:

```html
<li>HTML</li>
```

A list item normally belongs inside a list.

---

# 34. Ordered List

Use:

```html
<ol>
```

Example:

```html
<ol>

    <li>Learn HTML</li>

    <li>Learn CSS</li>

    <li>Learn JavaScript</li>

</ol>
```

`ol` means:

```text
Ordered List
```

---

# 35. Ordered List Meaning

An ordered list represents items where sequence or order matters.

Example:

```html
<ol>

    <li>Open the application.</li>

    <li>Login.</li>

    <li>Select the course.</li>

    <li>Submit the form.</li>

</ol>
```

---

# 36. Description List

HTML also supports description lists.

Elements:

```html
<dl>
<dt>
<dd>
```

Example:

```html
<dl>

    <dt>HTML</dt>

    <dd>
        HyperText Markup Language.
    </dd>

    <dt>CSS</dt>

    <dd>
        Cascading Style Sheets.
    </dd>

</dl>
```

---

# 37. Description List Structure

Think:

```text
dl
│
├── dt
│   └── Term
│
├── dd
│   └── Description
│
├── dt
│   └── Term
│
└── dd
    └── Description
```

---

# 38. Nested Lists

Lists can contain other lists.

Example:

```html
<ul>

    <li>
        Frontend

        <ul>

            <li>HTML</li>

            <li>CSS</li>

            <li>JavaScript</li>

        </ul>

    </li>

    <li>
        Backend

        <ul>

            <li>Python</li>

            <li>Flask</li>

        </ul>

    </li>

</ul>
```

Structure:

```text
Frontend
├── HTML
├── CSS
└── JavaScript

Backend
├── Python
└── Flask
```

---

# 39. Lists Are Structural

Use lists when information is logically a list.

Do not use:

```html
<ul>
```

just to create a visual layout.

HTML describes meaning.

CSS will later handle layout.

---

# 40. HTML Tables

Tables represent tabular data.

Examples:

```text
Student Records
Course Results
Product Data
Employee Records
Attendance
Marks
```

Main table elements:

```text
table
tr
th
td
```

---

# 41. Basic Table

Example:

```html
<table>

    <tr>
        <th>Name</th>
        <th>Age</th>
    </tr>

    <tr>
        <td>Alex</td>
        <td>45</td>
    </tr>

</table>
```

---

# 42. `<table>`

The `<table>` element represents tabular data.

Example:

```html
<table>

    ...

</table>
```

---

# 43. `<tr>`

`tr` means:

```text
Table Row
```

Example:

```html
<tr>
    <td>Alex</td>
    <td>45</td>
</tr>
```

---

# 44. `<th>`

`th` means:

```text
Table Header Cell
```

Example:

```html
<th>Name</th>
<th>Age</th>
```

It identifies header information.

---

# 45. `<td>`

`td` means:

```text
Table Data Cell
```

Example:

```html
<td>Alex</td>
<td>45</td>
```

---

# 46. Table Structure

Think:

```text
table
│
├── tr
│   ├── th
│   └── th
│
├── tr
│   ├── td
│   └── td
│
└── tr
    ├── td
    └── td
```

---

# 47. Table with Student Data

```html
<table>

    <tr>

        <th>Student ID</th>
        <th>Name</th>
        <th>Course</th>

    </tr>

    <tr>

        <td>101</td>
        <td>Alex</td>
        <td>Python</td>

    </tr>

    <tr>

        <td>102</td>
        <td>John</td>
        <td>Java</td>

    </tr>

</table>
```

---

# 48. Table Caption

Use:

```html
<caption>
```

Example:

```html
<table>

    <caption>
        Student Details
    </caption>

    <tr>
        <th>ID</th>
        <th>Name</th>
    </tr>

    <tr>
        <td>101</td>
        <td>Alex</td>
    </tr>

</table>
```

A caption describes the table.

---

# 49. Table Head, Body and Foot

HTML provides:

```text
thead
tbody
tfoot
```

Example:

```html
<table>

    <caption>Student Marks</caption>

    <thead>

        <tr>
            <th>Name</th>
            <th>Marks</th>
        </tr>

    </thead>

    <tbody>

        <tr>
            <td>Alex</td>
            <td>90</td>
        </tr>

        <tr>
            <td>John</td>
            <td>85</td>
        </tr>

    </tbody>

    <tfoot>

        <tr>
            <td>Total</td>
            <td>175</td>
        </tr>

    </tfoot>

</table>
```

---

# 50. Table Sections

The structure becomes:

```text
table
│
├── caption
│
├── thead
│   └── tr
│       ├── th
│       └── th
│
├── tbody
│   ├── tr
│   └── tr
│
└── tfoot
    └── tr
```

---

# 51. `colspan`

`colspan` allows a cell to span multiple columns.

Example:

```html
<table>

    <tr>

        <th colspan="2">
            Student Details
        </th>

    </tr>

    <tr>

        <td>Name</td>
        <td>Alex</td>

    </tr>

</table>
```

Here:

```text
colspan="2"
```

means the cell spans two columns.

---

# 52. `rowspan`

`rowspan` allows a cell to span multiple rows.

Example:

```html
<table>

    <tr>

        <th rowspan="2">
            Student
        </th>

        <td>HTML</td>

    </tr>

    <tr>

        <td>CSS</td>

    </tr>

</table>
```

Here:

```text
rowspan="2"
```

means the cell spans two rows.

---

# 53. Do Not Use Tables for Page Layout

Do not build a website layout like:

```html
<table>

    <tr>
        <td>Header</td>
    </tr>

    <tr>
        <td>Content</td>
    </tr>

</table>
```

Tables are for **tabular data**.

Page layout should use appropriate HTML structure and CSS.

---

# 54. Generic Container — `<div>`

`<div>` is a generic block container.

Example:

```html
<div>

    <h2>Student Information</h2>

    <p>
        Student details.
    </p>

</div>
```

It groups content without providing a more specific semantic meaning.

---

# 55. Why Use `<div>`?

A `div` is useful when you need a generic grouping container.

Example:

```html
<div>

    <h2>Courses</h2>

    <p>
        Python course information.
    </p>

</div>
```

Later CSS can target this structure.

---

# 56. Inline Generic Container — `<span>`

`<span>` is a generic inline container.

Example:

```html
<p>
    Learn
    <span>HTML</span>
    today.
</p>
```

It is useful for grouping a portion of text or other inline content when no more meaningful semantic element applies.

---

# 57. `<div>` vs `<span>`

Basic mental model:

```text
div
↓
Generic block-level container

span
↓
Generic inline container
```

Example:

```html
<div>
    A section of content
</div>
```

and:

```html
<p>
    Hello
    <span>Students</span>
</p>
```

---

# 58. Do Not Use `div` for Everything

Bad structure:

```html
<div>
    <div>
        <div>
            <div>
                Courses
            </div>
        </div>
    </div>
</div>
```

Prefer meaningful semantic elements where they describe the content correctly.

---

# 59. Semantic HTML

Semantic HTML means choosing HTML elements according to their meaning.

Instead of:

```html
<div>
    Navigation
</div>
```

use:

```html
<nav>
    Navigation
</nav>
```

Instead of:

```html
<div>
    Main Content
</div>
```

use:

```html
<main>
    Main Content
</main>
```

---

# 60. Why Semantic HTML?

Semantic HTML improves:

```text
Meaning
Structure
Accessibility
Maintainability
Search Engine Understanding
```

It helps browsers and assistive technologies understand the purpose of different parts of the page.

---

# 61. Important Semantic Elements

Today learn:

```text
header
nav
main
section
article
aside
footer
```

These are important HTML5 semantic elements.

---

# 62. `<header>`

`<header>` represents introductory content for a page or section.

Example:

```html
<header>

    <h1>College Website</h1>

    <p>
        Welcome to our college.
    </p>

</header>
```

A header can contain:

- Logo
- Heading
- Introductory content
- Navigation
- Other relevant introductory content

---

# 63. `<nav>`

`<nav>` represents a section containing navigation links.

Example:

```html
<nav>

    <a href="index.html">Home</a>

    <a href="about.html">About</a>

    <a href="courses.html">Courses</a>

    <a href="contact.html">Contact</a>

</nav>
```

---

# 64. `<main>`

`<main>` represents the dominant content of the document.

Example:

```html
<main>

    <h1>Python Full Stack Course</h1>

    <p>
        Course information.
    </p>

</main>
```

A document normally has one main element representing its primary content.

---

# 65. `<section>`

`<section>` represents a thematic grouping of content.

Example:

```html
<section>

    <h2>HTML Course</h2>

    <p>
        Learn HTML fundamentals.
    </p>

</section>
```

A section often has a heading.

---

# 66. `<article>`

`<article>` represents a self-contained composition that could stand independently.

Examples:

```text
Blog Post
News Article
Forum Post
Product Review
Course Article
```

Example:

```html
<article>

    <h2>Introduction to HTML</h2>

    <p>
        HTML is the foundation of web pages.
    </p>

</article>
```

---

# 67. `<aside>`

`<aside>` represents content related to the surrounding content but not part of its main flow.

Examples:

```text
Related Articles
Author Information
Related Courses
Side Notes
Advertisements
```

Example:

```html
<aside>

    <h2>Related Courses</h2>

    <p>
        Learn CSS next.
    </p>

</aside>
```

---

# 68. `<footer>`

`<footer>` represents footer information for a page or section.

Example:

```html
<footer>

    <p>
        Copyright 2026
    </p>

</footer>
```

It may contain:

- Copyright information
- Contact information
- Related links
- Author information

---

# 69. Semantic Page Structure

A typical page can look like:

```text
html
│
├── head
│
└── body
    │
    ├── header
    │
    ├── nav
    │
    ├── main
    │   │
    │   ├── section
    │   │
    │   ├── article
    │   │
    │   └── aside
    │
    └── footer
```

---

# 70. Complete Semantic HTML Example

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>Python Full Stack</title>

    </head>

    <body>

        <header>

            <h1>Python Full Stack Development</h1>

            <p>
                Learn full stack web development.
            </p>

        </header>

        <nav>

            <a href="index.html">Home</a>

            <a href="courses.html">Courses</a>

            <a href="about.html">About</a>

            <a href="contact.html">Contact</a>

        </nav>

        <main>

            <section>

                <h2>Frontend Development</h2>

                <p>
                    Learn HTML, CSS and JavaScript.
                </p>

            </section>

            <section>

                <h2>Backend Development</h2>

                <p>
                    Learn Python and Flask.
                </p>

            </section>

            <article>

                <h2>Why Learn Full Stack?</h2>

                <p>
                    Full stack development helps developers
                    understand complete web applications.
                </p>

            </article>

            <aside>

                <h2>Related Topic</h2>

                <p>
                    Database fundamentals.
                </p>

            </aside>

        </main>

        <footer>

            <p>
                Full Stack Development Course
            </p>

        </footer>

    </body>

</html>
```

---

# 71. Semantic HTML Tree

The previous page can be represented as:

```text
html
│
├── head
│   ├── meta
│   ├── meta
│   └── title
│
└── body
    │
    ├── header
    │   ├── h1
    │   └── p
    │
    ├── nav
    │   ├── a
    │   ├── a
    │   ├── a
    │   └── a
    │
    ├── main
    │   │
    │   ├── section
    │   │   ├── h2
    │   │   └── p
    │   │
    │   ├── section
    │   │   ├── h2
    │   │   └── p
    │   │
    │   ├── article
    │   │   ├── h2
    │   │   └── p
    │   │
    │   └── aside
    │       ├── h2
    │       └── p
    │
    └── footer
        └── p
```

---

# 72. Semantic HTML vs Generic HTML

Generic structure:

```html
<div>

    <div>
        Navigation
    </div>

    <div>
        Main Content
    </div>

    <div>
        Footer
    </div>

</div>
```

Semantic structure:

```html
<header>
    ...
</header>

<nav>
    ...
</nav>

<main>
    ...
</main>

<footer>
    ...
</footer>
```

Semantic HTML communicates meaning.

---

# 73. `section` vs `div`

Use:

```html
<section>
```

when the content forms a meaningful thematic section.

Use:

```html
<div>
```

when you need a generic container and there is no more appropriate semantic element.

Example:

```html
<section>

    <h2>Courses</h2>

    <p>
        Course information.
    </p>

</section>
```

Generic grouping:

```html
<div>
    ...
</div>
```

---

# 74. `article` vs `section`

A useful mental model:

```text
section
↓
Thematic grouping

article
↓
Self-contained content
```

Example:

```html
<section>

    <h2>Latest Articles</h2>

    <article>
        <h3>HTML Basics</h3>
        <p>...</p>
    </article>

    <article>
        <h3>CSS Basics</h3>
        <p>...</p>
    </article>

</section>
```

---

# 75. `header` Does Not Mean Only Page Header

A `<header>` can belong to:

```text
Page
Section
Article
```

Example:

```html
<article>

    <header>

        <h2>HTML Basics</h2>

        <p>
            Published on August 25, 2026
        </p>

    </header>

    <p>
        HTML provides structure.
    </p>

</article>
```

---

# 76. `footer` Does Not Mean Only Page Footer

A `<footer>` can also belong to an article or section.

Example:

```html
<article>

    <h2>HTML Basics</h2>

    <p>
        HTML provides structure.
    </p>

    <footer>

        <p>
            Written by Alex
        </p>

    </footer>

</article>
```

---

# 77. Links + Semantic Navigation

A strong website structure:

```html
<nav>

    <a href="index.html">
        Home
    </a>

    <a href="about.html">
        About
    </a>

    <a href="courses.html">
        Courses
    </a>

    <a href="contact.html">
        Contact
    </a>

</nav>
```

Remember:

```text
nav
↓
Navigation structure

a
↓
Individual link
```

---

# 78. Image + Figure

HTML also provides:

```text
figure
figcaption
```

These are useful when an image or other content is accompanied by a caption.

Example:

```html
<figure>

    <img
        src="college.jpg"
        alt="College building">

    <figcaption>
        Main College Building
    </figcaption>

</figure>
```

---

# 79. `<figure>`

`figure` represents self-contained content that is referenced from the main flow.

It may contain:

```text
Image
Diagram
Code Example
Illustration
Other Referenced Content
```

---

# 80. `<figcaption>`

`figcaption` provides a caption for the content inside a figure.

Example:

```html
<figure>

    <img
        src="python.jpg"
        alt="Python programming">

    <figcaption>
        Python Programming
    </figcaption>

</figure>
```

---

# 81. Complete Content Example

```html
<main>

    <section>

        <h2>Our Courses</h2>

        <ul>

            <li>Python</li>

            <li>HTML</li>

            <li>CSS</li>

            <li>JavaScript</li>

        </ul>

    </section>

    <section>

        <h2>Student Information</h2>

        <table>

            <caption>
                Student Details
            </caption>

            <thead>

                <tr>

                    <th>ID</th>
                    <th>Name</th>
                    <th>Course</th>

                </tr>

            </thead>

            <tbody>

                <tr>

                    <td>101</td>
                    <td>Alex</td>
                    <td>Python</td>

                </tr>

                <tr>

                    <td>102</td>
                    <td>John</td>
                    <td>JavaScript</td>

                </tr>

            </tbody>

        </table>

    </section>

</main>
```

---

# 82. Day 2 — One-Hour Schedule

| Time | Topic |
|---|---|
| 0–10 min | Links and `a`, `href`, URLs |
| 10–20 min | Images, `src`, `alt`, image paths |
| 20–30 min | Relative paths and folders |
| 30–40 min | Lists: `ul`, `ol`, `li`, `dl`, `dt`, `dd` |
| 40–50 min | Tables and table structure |
| 50–60 min | `div`, `span`, semantic HTML |

---

# 83. Day 2 — Practical Project

Create this folder:

```text
college-website/
│
├── index.html
├── about.html
├── courses.html
├── contact.html
│
└── images/
    ├── college.jpg
    └── student.jpg
```

---

# 84. `index.html` Requirements

The home page must contain:

```text
Header
Navigation
Main
Section
Image
Links
Footer
```

Basic structure:

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>College Website</title>

    </head>

    <body>

        <header>

            <h1>ABC College</h1>

        </header>

        <nav>

            <a href="index.html">Home</a>

            <a href="about.html">About</a>

            <a href="courses.html">Courses</a>

            <a href="contact.html">Contact</a>

        </nav>

        <main>

            <section>

                <h2>Welcome</h2>

                <p>
                    Welcome to ABC College.
                </p>

                <figure>

                    <img
                        src="images/college.jpg"
                        alt="ABC College building">

                    <figcaption>
                        ABC College
                    </figcaption>

                </figure>

            </section>

        </main>

        <footer>

            <p>
                ABC College
            </p>

        </footer>

    </body>

</html>
```

---

# 85. `courses.html` Requirements

Create:

```text
Courses
```

Include:

```text
Python
HTML
CSS
JavaScript
Flask
SQL
```

Use an unordered list.

Example:

```html
<h1>Courses</h1>

<ul>

    <li>Python</li>

    <li>HTML</li>

    <li>CSS</li>

    <li>JavaScript</li>

    <li>Flask</li>

    <li>SQL</li>

</ul>
```

---

# 86. `about.html` Requirements

Create:

```text
About ABC College
```

Include:

```text
About
Mission
Vision
Programs
```

Use:

```text
header
main
section
h1
h2
p
footer
```

---

# 87. `contact.html` Requirements

Create:

```text
Contact Us
```

Include:

```text
Email
Phone
Website
Address
```

Use links for:

```text
Email
Phone
Website
```

Example:

```html
<a href="mailto:admin@example.com">
    Email
</a>

<a href="tel:+911234567890">
    Call
</a>
```

---

# 88. Day 2 Table Exercise

Create:

```text
student.html
```

Create this table:

```text
Student ID | Name | Course | Marks
-----------------------------------
101        | Alex | Python | 90
102        | John | Java   | 85
103        | Ravi | HTML   | 88
104        | Tony | CSS    | 92
```

Use:

```html
<table>
<caption>
<thead>
<tbody>
<tr>
<th>
<td>
```

---

# 89. Day 2 Image Exercise

Create:

```text
images/
```

Place an image inside it.

Then reference it:

```html
<img
    src="images/student.jpg"
    alt="Student profile photo">
```

Then move the HTML page into another folder and observe what happens.

Example:

```text
website/
│
├── index.html
│
├── pages/
│   └── student.html
│
└── images/
    └── student.jpg
```

Now from `student.html`:

```html
<img
    src="../images/student.jpg"
    alt="Student profile photo">
```

This exercise is important for understanding paths.

---

# 90. Day 2 Link Exercise

Create:

```text
index.html
about.html
courses.html
contact.html
```

Connect all pages.

Each page should have:

```html
<nav>

    <a href="index.html">Home</a>

    <a href="about.html">About</a>

    <a href="courses.html">Courses</a>

    <a href="contact.html">Contact</a>

</nav>
```

Test every link.

You should be able to move:

```text
Home
 ↕
About
 ↕
Courses
 ↕
Contact
```

---

# 91. Day 2 — Important Tags

## Links

```text
a
```

## Images

```text
img
figure
figcaption
```

## Lists

```text
ul
ol
li
dl
dt
dd
```

## Tables

```text
table
caption
thead
tbody
tfoot
tr
th
td
```

## Generic Containers

```text
div
span
```

## Semantic HTML

```text
header
nav
main
section
article
aside
footer
```

---

# 92. Day 2 — Important Attributes

```text
href
target
rel
id
src
alt
width
height
colspan
rowspan
```

Examples:

```html
<a href="about.html">
```

```html
<a
    href="https://example.com"
    target="_blank"
    rel="noopener">
```

```html
<h2 id="courses">
```

```html
<img
    src="images/logo.png"
    alt="College Logo">
```

```html
<th colspan="2">
```

```html
<td rowspan="2">
```

---

# 93. Day 2 — Attribute Mental Model

Remember:

```text
Element
│
├── Attribute
│   └── Value
│
├── Attribute
│   └── Value
│
└── Content
```

Example:

```html
<a
    href="about.html"
    target="_blank">

    About

</a>
```

Structure:

```text
a
│
├── href
│   └── about.html
│
├── target
│   └── _blank
│
└── About
```

---

# 94. Day 2 — Important Differences

## `a` vs `img`

```text
a
↓
Creates a link

img
↓
Embeds an image
```

---

## `ul` vs `ol`

```text
ul
↓
Unordered list

ol
↓
Ordered list
```

---

## `th` vs `td`

```text
th
↓
Header cell

td
↓
Data cell
```

---

## `div` vs `span`

```text
div
↓
Generic block container

span
↓
Generic inline container
```

---

## `section` vs `div`

```text
section
↓
Meaningful thematic grouping

div
↓
Generic grouping
```

---

## `section` vs `article`

```text
section
↓
Thematic grouping

article
↓
Self-contained composition
```

---

# 95. Day 2 — Common Mistakes

## Mistake 1 — Missing `alt`

Avoid:

```html
<img src="student.jpg">
```

Prefer:

```html
<img
    src="student.jpg"
    alt="Student profile photo">
```

---

## Mistake 2 — Wrong Image Path

If the image is:

```text
images/student.jpg
```

then:

```html
<img src="student.jpg">
```

may be wrong if the HTML file is not in the same directory.

Correct:

```html
<img src="images/student.jpg">
```

---

## Mistake 3 — Wrong Parent Path

From:

```text
pages/about.html
```

to:

```text
images/logo.png
```

use:

```html
<img
    src="../images/logo.png"
    alt="Logo">
```

---

## Mistake 4 — Forgetting `href`

Incorrect:

```html
<a>
    About
</a>
```

Correct:

```html
<a href="about.html">
    About
</a>
```

---

## Mistake 5 — Putting `<li>` Directly in Body

Avoid:

```html
<li>HTML</li>
<li>CSS</li>
```

Prefer:

```html
<ul>

    <li>HTML</li>

    <li>CSS</li>

</ul>
```

---

## Mistake 6 — Using Tables for Layout

Do not use:

```html
<table>
```

to build page layout.

Use tables for actual tabular data.

---

## Mistake 7 — Using `div` Everywhere

Prefer:

```html
<header>
<nav>
<main>
<section>
<article>
<footer>
```

when those elements correctly describe the content.

---

# 96. Day 2 — Interview Questions

## Q1. What is the purpose of `<a>`?

It creates a hyperlink.

## Q2. What is `href`?

It specifies the destination of a link.

## Q3. What is a relative URL?

A URL interpreted relative to the current document's location.

## Q4. What does `../` mean?

It refers to the parent directory.

## Q5. What does `./` mean?

It refers to the current directory.

## Q6. What is the purpose of `alt`?

It provides alternative text for an image.

## Q7. What is `<ul>`?

An unordered list.

## Q8. What is `<ol>`?

An ordered list.

## Q9. What is `<li>`?

A list item.

## Q10. What is `<table>`?

An element representing tabular data.

## Q11. What is `<tr>`?

A table row.

## Q12. What is `<th>`?

A table header cell.

## Q13. What is `<td>`?

A table data cell.

## Q14. What is `<thead>`?

The header section of a table.

## Q15. What is `<tbody>`?

The main body section of a table.

## Q16. What is `<tfoot>`?

The footer section of a table.

## Q17. What is `colspan`?

It makes a table cell span multiple columns.

## Q18. What is `rowspan`?

It makes a table cell span multiple rows.

## Q19. What is `<div>`?

A generic block container.

## Q20. What is `<span>`?

A generic inline container.

## Q21. What is semantic HTML?

Using elements according to their meaning and purpose.

## Q22. What is `<nav>`?

A section containing navigation links.

## Q23. What is `<main>`?

The dominant content of the document.

## Q24. What is `<section>`?

A thematic grouping of content.

## Q25. What is `<article>`?

A self-contained composition.

## Q26. What is `<aside>`?

Related content that is tangential to the main content.

## Q27. What is `<footer>`?

Footer information for a page or section.

---

# 97. Day 2 — Coding Test

Without looking at the notes, create:

```text
course-website/
│
├── index.html
├── courses.html
└── images/
    └── course.jpg
```

`index.html` must contain:

```text
header
nav
main
section
image
footer
```

Navigation:

```text
Home
Courses
```

`courses.html` must contain:

```text
h1
ul
ol
table
```

The table must have:

```text
Course
Duration
Level
```

Example data:

```text
HTML
4 Days
Beginner

CSS
5 Days
Beginner

JavaScript
10 Days
Beginner → Intermediate
```

---

# 98. Day 2 — Mini Project

## Training Institute Website

Build:

```text
training-institute/
│
├── index.html
├── courses.html
├── students.html
├── about.html
├── contact.html
│
└── images/
    └── institute.jpg
```

---

# 99. Home Page Requirements

Use:

```text
header
nav
main
section
figure
img
figcaption
article
footer
```

Content:

```text
Training Institute

Home
Courses
Students
About
Contact

Welcome to our training institute.

Python Full Stack Development

Data Structures

Database Development

Frontend Development
```

---

# 100. Courses Page Requirements

Use:

```text
h1
h2
ul
ol
table
```

Create a course table:

```text
Course | Duration | Level
```

Add at least five courses.

---

# 101. Students Page Requirements

Create a student table:

```text
ID
Name
Course
Status
```

Use:

```html
<table>

    <caption>
        Student Information
    </caption>

    <thead>
        ...
    </thead>

    <tbody>
        ...
    </tbody>

</table>
```

---

# 102. About Page Requirements

Use semantic HTML:

```text
header
main
section
article
footer
```

Include:

```text
About Us
Mission
Vision
Training Philosophy
```

---

# 103. Contact Page Requirements

Use:

```text
main
section
address
```

Example:

```html
<address>

    Training Institute<br>

    Hyderabad<br>

    India<br>

    <a href="mailto:admin@example.com">
        admin@example.com
    </a>

</address>
```

---

# 104. `<address>`

The `<address>` element represents contact information for a person, organization, or relevant content.

Example:

```html
<address>

    ABC Training Institute<br>

    Hyderabad, India<br>

    <a href="mailto:admin@example.com">
        admin@example.com
    </a>

</address>
```

---

# 105. Day 2 — Semantic Structure Practice

Create this:

```html
<body>

    <header>

        <h1>Training Institute</h1>

    </header>

    <nav>

        <a href="index.html">Home</a>

        <a href="courses.html">Courses</a>

        <a href="about.html">About</a>

        <a href="contact.html">Contact</a>

    </nav>

    <main>

        <section>

            <h2>Our Courses</h2>

            <article>

                <h3>Python Full Stack</h3>

                <p>
                    Learn complete web development.
                </p>

            </article>

            <article>

                <h3>Data Structures</h3>

                <p>
                    Learn important data structures.
                </p>

            </article>

        </section>

        <aside>

            <h2>Upcoming Course</h2>

            <p>
                JavaScript Advanced.
            </p>

        </aside>

    </main>

    <footer>

        <p>
            Training Institute
        </p>

    </footer>

</body>
```

---

# 106. Day 2 — What You Should Understand

You should now understand how to build:

```text
Page
│
├── Header
│
├── Navigation
│
├── Main
│   │
│   ├── Section
│   │   ├── Article
│   │   └── Article
│   │
│   └── Aside
│
└── Footer
```

Inside those structures you can place:

```text
Headings
Paragraphs
Links
Images
Lists
Tables
```

---

# 107. HTML Content Model — Mental Model

Think:

```text
HTML Document
│
├── Structure
│
├── Content
│
├── Relationships
│
└── Meaning
```

Examples:

```text
Structure
→ header
→ main
→ section
→ footer

Content
→ text
→ image
→ list
→ table

Relationships
→ parent
→ child
→ link

Meaning
→ article
→ navigation
→ section
→ main
```

---

# 108. Day 2 — HTML Skills Matrix

| Skill | Covered |
|---|---|
| Hyperlinks | ✅ |
| Relative Links | ✅ |
| External Links | ✅ |
| Same-page Links | ✅ |
| Email Links | ✅ |
| Telephone Links | ✅ |
| Images | ✅ |
| `src` | ✅ |
| `alt` | ✅ |
| Image Paths | ✅ |
| Relative Paths | ✅ |
| `./` | ✅ |
| `../` | ✅ |
| Unordered Lists | ✅ |
| Ordered Lists | ✅ |
| Description Lists | ✅ |
| Nested Lists | ✅ |
| Tables | ✅ |
| Table Headers | ✅ |
| Table Body | ✅ |
| Table Footer | ✅ |
| Caption | ✅ |
| `colspan` | ✅ |
| `rowspan` | ✅ |
| `div` | ✅ |
| `span` | ✅ |
| Semantic HTML | ✅ |
| `header` | ✅ |
| `nav` | ✅ |
| `main` | ✅ |
| `section` | ✅ |
| `article` | ✅ |
| `aside` | ✅ |
| `footer` | ✅ |
| `figure` | ✅ |
| `figcaption` | ✅ |
| `address` | ✅ |

---

# 109. Day 2 — Revision Map

```text
HTML
│
├── Links
│   ├── a
│   ├── href
│   ├── target
│   ├── rel
│   ├── id
│   ├── mailto
│   └── tel
│
├── Images
│   ├── img
│   ├── src
│   ├── alt
│   ├── width
│   └── height
│
├── Paths
│   ├── same folder
│   ├── child folder
│   ├── ./
│   └── ../
│
├── Lists
│   ├── ul
│   ├── ol
│   ├── li
│   ├── dl
│   ├── dt
│   └── dd
│
├── Tables
│   ├── table
│   ├── caption
│   ├── thead
│   ├── tbody
│   ├── tfoot
│   ├── tr
│   ├── th
│   ├── td
│   ├── colspan
│   └── rowspan
│
├── Generic
│   ├── div
│   └── span
│
└── Semantic
    ├── header
    ├── nav
    ├── main
    ├── section
    ├── article
    ├── aside
    ├── footer
    ├── figure
    ├── figcaption
    └── address
```

---

# 110. Day 2 — Final Checklist

Before moving to **Day 38 — Day 3**, you should be able to:

- [ ] Create links using `<a>`
- [ ] Use `href`
- [ ] Create internal links
- [ ] Create external links
- [ ] Understand relative URLs
- [ ] Understand absolute URLs
- [ ] Use `target`
- [ ] Understand `rel="noopener"`
- [ ] Create email links
- [ ] Create telephone links
- [ ] Create same-page links
- [ ] Use `id`
- [ ] Add images using `<img>`
- [ ] Use `src`
- [ ] Use meaningful `alt` text
- [ ] Understand image paths
- [ ] Understand `./`
- [ ] Understand `../`
- [ ] Create unordered lists
- [ ] Create ordered lists
- [ ] Create description lists
- [ ] Create nested lists
- [ ] Create tables
- [ ] Use `caption`
- [ ] Use `thead`
- [ ] Use `tbody`
- [ ] Use `tfoot`
- [ ] Use `tr`
- [ ] Use `th`
- [ ] Use `td`
- [ ] Understand `colspan`
- [ ] Understand `rowspan`
- [ ] Understand `div`
- [ ] Understand `span`
- [ ] Understand semantic HTML
- [ ] Use `header`
- [ ] Use `nav`
- [ ] Use `main`
- [ ] Use `section`
- [ ] Use `article`
- [ ] Use `aside`
- [ ] Use `footer`
- [ ] Use `figure`
- [ ] Use `figcaption`
- [ ] Use `address`
- [ ] Build a multi-page HTML website
- [ ] Connect multiple HTML pages
- [ ] Organize images into folders
- [ ] Build a semantic page structure

---

# 111. Day 2 — Final Mental Model

```text
HTML
│
├── DOCUMENT
│   ├── html
│   ├── head
│   └── body
│
├── CONTENT
│   ├── headings
│   ├── paragraphs
│   ├── links
│   ├── images
│   ├── lists
│   └── tables
│
├── ORGANIZATION
│   ├── div
│   └── span
│
├── SEMANTIC STRUCTURE
│   ├── header
│   ├── nav
│   ├── main
│   ├── section
│   ├── article
│   ├── aside
│   └── footer
│
└── RESOURCES
    ├── paths
    ├── images
    └── links
```

---

# 112. Day 2 — The Big Picture

After Day 1 and Day 2:

```text
DAY 36
HTML FOUNDATION
│
├── What is HTML?
├── Browser
├── .html
├── DOCTYPE
├── html
├── head
├── body
├── meta
├── title
├── tags
├── elements
├── attributes
├── nesting
├── headings
├── paragraphs
├── text markup
├── comments
└── entities

        ↓

DAY 37
HTML CONTENT
│
├── Links
├── Images
├── Paths
├── Lists
├── Tables
├── div
├── span
├── figure
├── figcaption
├── address
└── Semantic HTML
    ├── header
    ├── nav
    ├── main
    ├── section
    ├── article
    ├── aside
    └── footer

        ↓

DAY 38
HTML FORMS + HTML5
│
├── Forms
├── Inputs
├── Labels
├── Select
├── Textarea
├── Buttons
├── Validation
├── Audio
├── Video
├── iframe
├── Global Attributes
├── Accessibility
└── Mini Project

        ↓

CSS
```

---

# DAY 2 — END

**Day 37 — HTML Content, Links, Images, Lists, Tables, Paths, `div`, `span` and Semantic HTML Completed**

**Next: Day 38 — HTML Forms, Input Types, Validation, Multimedia, iframe, Global Attributes, Accessibility and HTML5 Features**
