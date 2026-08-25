
# DAY 1 — HTML FOUNDATION

## Front-End Development — Day 36

**Duration:** 1 Hour  
**Level:** Beginner  
**Module:** Front-End Development  
**Topic:** HTML — Foundation  
**Focus:** HTML Only

> **Day 36 = HTML Foundation**
>
> CSS, JavaScript and Flask are intentionally not covered today.

---

# 1. What Is HTML?

HTML stands for:

**HyperText Markup Language**

HTML is the standard **markup language** used to create the structure and content of web pages.

HTML is **not a programming language**.

HTML describes what different pieces of content represent.

Examples:

- Heading
- Paragraph
- Link
- Image
- List
- Table
- Form
- Section
- Article
- Navigation

---

# 2. Why Do We Need HTML?

A web page contains different types of content.

For example:

```text
My College Website

Welcome to ABC College.

Courses

Python
Java
JavaScript

Contact Us
````

The browser needs to understand:

* What is the main heading?
* What is a paragraph?
* What is a link?
* What is a list?
* What is a section?

HTML provides this structure.

```text
HTML
│
├── Heading
├── Paragraph
├── Link
├── Image
├── List
├── Table
└── Form
```

---

# 3. HTML = Structure

Web development can be understood using three major technologies:

```text
HTML
│
└── Structure + Content

CSS
│
└── Presentation + Design

JavaScript
│
└── Behaviour + Interaction
```

For this phase:

```text
HTML
↓
CSS
↓
JavaScript
↓
Flask
```

Today we focus only on:

```text
HTML
```

---

# 4. What Does HyperText Mean?

**HyperText** means text that can contain links to other documents or resources.

Example:

```html
<a href="about.html">
    About Us
</a>
```

The user can click the link.

The browser can move from:

```text
index.html
    |
    v
about.html
```

This ability to connect documents through links is one of the foundations of the World Wide Web.

---

# 5. What Does Markup Mean?

Markup means using special tags to describe the structure and meaning of content.

Example:

```html
<h1>Welcome</h1>
```

The browser understands:

```text
h1
│
└── Main heading
```

Another example:

```html
<p>Welcome to my website.</p>
```

The browser understands:

```text
p
│
└── Paragraph
```

Therefore:

> **Markup describes the structure and meaning of content.**

---

# 6. HTML Is Not a Programming Language

HTML describes content and structure.

Example:

```html
<h1>Student Management System</h1>

<p>Welcome to the student portal.</p>
```

HTML does not normally provide programming logic such as:

```text
if
else
for
while
function
calculation
```

Programming logic can be provided later by JavaScript or Python.

Therefore:

```text
HTML
→ Structure

CSS
→ Presentation

JavaScript
→ Browser Behaviour

Python
→ Programming Language

Flask
→ Python Web Framework
```

---

# 7. What Is a Web Browser?

A **web browser** is software that retrieves and displays web content.

Examples:

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari

The browser:

1. Requests a web resource.
2. Receives HTML.
3. Parses the HTML.
4. Builds the document structure.
5. Displays the page.

---

# 8. Browser and HTML

Suppose the browser receives:

```html
<h1>Hello World</h1>
```

The browser understands:

```text
This is a heading.
```

Suppose it receives:

```html
<p>Welcome to my website.</p>
```

The browser understands:

```text
This is a paragraph.
```

The browser does not simply treat HTML as ordinary text.

It **parses** the HTML and creates a structured document.

---

# 9. Basic Web Flow

A simplified web flow:

```text
User
  |
  v
Browser
  |
  v
Web Server
  |
  v
HTML Response
  |
  v
Browser
  |
  v
HTML Parsing
  |
  v
Document Structure
  |
  v
Web Page
```

Later:

```text
HTML
+
CSS
+
JavaScript
```

will create a complete interactive web application.

---

# 10. HTML File Extension

HTML files normally use:

```text
.html
```

Examples:

```text
index.html
home.html
about.html
contact.html
login.html
register.html
student.html
course.html
```

---

# 11. The `index.html` File

A common starting page is:

```text
index.html
```

For example:

```text
website/
│
├── index.html
├── about.html
├── contact.html
└── login.html
```

When a website is opened without specifying a particular page, `index.html` is commonly used as the default document.

---

# 12. Create Your First HTML File

Create a folder:

```text
html-course
```

Inside it create:

```text
index.html
```

Folder structure:

```text
html-course/
│
└── index.html
```

Open the file in a text editor.

Examples of editors:

* Visual Studio Code
* Notepad
* Notepad++
* Sublime Text

---

# 13. First HTML Document

Write:

```html
<!DOCTYPE html>

<html>

</html>
```

This is the basic beginning of an HTML document.

---

# 14. DOCTYPE

The first line is:

```html
<!DOCTYPE html>
```

This is the HTML document type declaration.

For modern HTML:

```html
<!DOCTYPE html>
```

is the standard declaration.

It tells the browser to use standards mode for the document.

---

# 15. HTML5 DOCTYPE

HTML5 uses the simple declaration:

```html
<!DOCTYPE html>
```

Older HTML versions used much longer DOCTYPE declarations.

Modern HTML keeps it simple:

```html
<!DOCTYPE html>
```

Remember it.

---

# 16. The `<html>` Element

The root element of the HTML document is:

```html
<html>
</html>
```

Everything in the document is normally contained inside:

```html
<html>
```

and:

```html
</html>
```

Basic structure:

```text
html
│
├── head
│
└── body
```

---

# 17. The `lang` Attribute

A common modern HTML document starts with:

```html
<html lang="en">
```

The `lang` attribute specifies the primary language of the document.

Example:

```html
<html lang="en">
```

This helps:

* Browsers
* Search engines
* Screen readers
* Accessibility tools

---

# 18. The `<head>` Element

The `<head>` contains information **about the document**.

Example:

```html
<head>

    <title>My Website</title>

    <meta charset="UTF-8">

</head>
```

The `<head>` may contain:

* Title
* Metadata
* Character encoding
* Viewport information
* External resource references
* Other document information

---

# 19. The `<body>` Element

The `<body>` contains the actual page content.

Example:

```html
<body>

    <h1>Welcome</h1>

    <p>Hello Students.</p>

</body>
```

Think of it as:

```text
<head>
    Information about the document
</head>

<body>
    Content of the document
</body>
```

---

# 20. Basic HTML Document Structure

The basic HTML5 document:

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <title>My First Web Page</title>

    </head>

    <body>

        <h1>Welcome</h1>

        <p>This is my first web page.</p>

    </body>

</html>
```

This structure should eventually become automatic for you.

---

# 21. HTML Document Tree

The document can be visualized as:

```text
Document
│
└── html
    │
    ├── head
    │   ├── meta
    │   └── title
    │
    └── body
        ├── h1
        └── p
```

HTML is therefore hierarchical.

---

# 22. The `<title>` Element

The `<title>` element defines the document title.

Example:

```html
<title>Student Portal</title>
```

It belongs inside:

```html
<head>
```

Example:

```html
<head>

    <title>Student Portal</title>

</head>
```

The title is typically displayed in the browser tab.

---

# 23. The `<meta>` Element

The `<meta>` element provides metadata about the document.

Example:

```html
<meta charset="UTF-8">
```

Another common example:

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0">
```

---

# 24. Character Encoding

Use:

```html
<meta charset="UTF-8">
```

This tells the browser that the document uses UTF-8 character encoding.

UTF-8 supports a very large range of characters and languages.

A modern HTML document should normally include it.

---

# 25. Viewport Meta Tag

A common HTML document contains:

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0">
```

This provides viewport information useful for displaying pages across different screen sizes.

Responsive design itself will be covered later with CSS.

---

# 26. Tags

HTML uses tags.

Example:

```html
<p>Hello</p>
```

The opening tag is:

```html
<p>
```

The closing tag is:

```html
</p>
```

General structure:

```html
<tag>
    Content
</tag>
```

---

# 27. Opening Tag

Example:

```html
<h1>
```

This is an opening tag.

---

# 28. Closing Tag

Example:

```html
</h1>
```

This is a closing tag.

Notice:

```text
Opening tag:
<h1>

Closing tag:
</h1>
```

The `/` indicates the closing tag.

---

# 29. HTML Element

Consider:

```html
<h1>Welcome</h1>
```

The complete structure is an HTML element.

Conceptually:

```text
Opening Tag
     +
Content
     +
Closing Tag
     =
HTML Element
```

Example:

```html
<p>Hello</p>
```

The entire:

```html
<p>Hello</p>
```

is an element.

---

# 30. Tag vs Element

This is an important distinction.

```html
<p>
```

is a tag.

```html
<p>Hello</p>
```

is an element.

Therefore:

```text
TAG
→ <p>

ELEMENT
→ <p>Hello</p>
```

---

# 31. HTML Attributes

Attributes provide additional information about HTML elements.

Example:

```html
<a href="about.html">
    About
</a>
```

Here:

```text
href
```

is an attribute.

The value is:

```text
about.html
```

General syntax:

```html
<tag attribute="value">
```

---

# 32. Attribute Example

```html
<img src="photo.jpg">
```

Here:

```text
src
│
└── Attribute

photo.jpg
│
└── Attribute Value
```

---

# 33. Multiple Attributes

An element can contain multiple attributes.

Example:

```html
<img
    src="student.jpg"
    alt="Student Photo">
```

Here:

```text
src
→ student.jpg

alt
→ Student Photo
```

---

# 34. Attributes Belong to Elements

Example:

```html
<a
    href="about.html"
    title="About our college">
    About
</a>
```

The element is:

```text
a
```

The attributes are:

```text
href
title
```

---

# 35. HTML Nesting

HTML elements can contain other HTML elements.

Example:

```html
<body>

    <h1>Welcome</h1>

    <p>Hello Students.</p>

</body>
```

Structure:

```text
body
│
├── h1
│
└── p
```

---

# 36. Parent and Child

Consider:

```html
<body>

    <h1>Welcome</h1>

</body>
```

The relationship is:

```text
body
│
└── h1
```

Therefore:

```text
body
→ Parent

h1
→ Child
```

---

# 37. Nested Elements

Example:

```html
<body>

    <section>

        <h1>Courses</h1>

        <p>Learn HTML.</p>

    </section>

</body>
```

Structure:

```text
body
│
└── section
    │
    ├── h1
    │
    └── p
```

Here:

```text
body
→ Parent of section

section
→ Child of body
→ Parent of h1 and p

h1
→ Child of section

p
→ Child of section
```

---

# 38. Correct Nesting

Correct:

```html
<p>
    <strong>Hello</strong>
</p>
```

Incorrect:

```html
<p>
    <strong>Hello
</p>
</strong>
```

HTML elements should be correctly nested.

Think:

```text
Open
↓
Open
↓
Close
↓
Close
```

Correct:

```html
<p>
    <strong>
        Hello
    </strong>
</p>
```

---

# 39. HTML Comments

Comments are written as:

```html
<!-- This is a comment -->
```

Example:

```html
<!-- Main Heading -->

<h1>Student Portal</h1>
```

Comments are not displayed as normal page content.

---

# 40. Why Use Comments?

Comments can explain the purpose of sections.

Example:

```html
<!-- Student Information -->

<h2>Student Details</h2>
```

Another example:

```html
<!-- Course Information -->

<section>

</section>
```

Comments are especially useful in large projects.

---

# 41. Headings

HTML provides six heading levels:

```html
<h1>Heading 1</h1>

<h2>Heading 2</h2>

<h3>Heading 3</h3>

<h4>Heading 4</h4>

<h5>Heading 5</h5>

<h6>Heading 6</h6>
```

---

# 42. Heading Hierarchy

The hierarchy is:

```text
h1
│
├── h2
│   │
│   ├── h3
│   │
│   └── h3
│
└── h2
    │
    └── h3
```

Use headings according to the structure of the content.

---

# 43. `<h1>`

Example:

```html
<h1>Python Full Stack Development</h1>
```

It usually represents the primary heading of the page.

---

# 44. `<h2>`

Example:

```html
<h2>Frontend Development</h2>
```

It can represent a major section under the main heading.

---

# 45. `<h3>`

Example:

```html
<h2>Frontend Development</h2>

<h3>HTML</h3>

<h3>CSS</h3>

<h3>JavaScript</h3>
```

---

# 46. `<h4>`, `<h5>`, `<h6>`

Examples:

```html
<h4>HTML Forms</h4>

<h5>Input Types</h5>

<h6>Email Input</h6>
```

These should be used when the document structure requires those levels.

---

# 47. Do Not Use Headings Only for Size

Do not think:

```text
h1 = biggest text
h2 = smaller text
h3 = smaller text
```

The primary purpose of headings is **document structure and meaning**.

Visual styling belongs to CSS.

---

# 48. Paragraphs

The paragraph element is:

```html
<p>
```

Example:

```html
<p>
    HTML is used to structure web pages.
</p>
```

Multiple paragraphs:

```html
<p>
    HTML defines page structure.
</p>

<p>
    CSS controls presentation.
</p>

<p>
    JavaScript provides behaviour.
</p>
```

---

# 49. Line Break

The `<br>` element creates a line break.

Example:

```html
<p>
    Hello<br>
    Welcome<br>
    Students
</p>
```

Conceptually:

```text
Hello
Welcome
Students
```

---

# 50. `<br>` Is a Void Element

A void element does not have normal content and does not require a closing tag.

Correct:

```html
<br>
```

Do not write:

```html
<br></br>
```

Other void elements will be covered later.

---

# 51. Horizontal Rule

The `<hr>` element represents a thematic break.

Example:

```html
<h2>HTML</h2>

<p>
    HTML provides structure.
</p>

<hr>

<h2>CSS</h2>

<p>
    CSS provides presentation.
</p>
```

---

# 52. Text Markup

HTML provides several elements for text.

Common elements:

```html
<strong>Important</strong>

<em>Emphasis</em>

<b>Bold</b>

<i>Italic</i>

<mark>Highlighted</mark>

<small>Small text</small>

<del>Deleted text</del>

<ins>Inserted text</ins>

<sub>Subscript</sub>

<sup>Superscript</sup>
```

---

# 53. `<strong>`

`<strong>` represents strong importance.

Example:

```html
<p>
    <strong>Important:</strong>
    Submit the assignment today.
</p>
```

---

# 54. `<em>`

`<em>` represents emphasis.

Example:

```html
<p>
    You <em>must</em> complete this exercise.
</p>
```

---

# 55. `<b>`

`<b>` represents text that is stylistically offset from surrounding content without adding strong semantic importance.

Example:

```html
<p>
    <b>HTML</b> is the first topic.
</p>
```

---

# 56. `<i>`

`<i>` represents text in an alternate voice or mood, or text conventionally rendered in italics.

Example:

```html
<p>
    The term <i>markup</i> is important.
</p>
```

---

# 57. `<strong>` vs `<b>`

Use:

```html
<strong>
```

when the content has strong importance.

Use:

```html
<b>
```

when you need to draw attention without conveying strong importance.

---

# 58. `<em>` vs `<i>`

Use:

```html
<em>
```

when the text is emphasized.

Use:

```html
<i>
```

when the text is in an alternate voice, mood, technical term, or similar semantic context.

---

# 59. `<mark>`

`<mark>` represents text that is highlighted or marked for reference.

Example:

```html
<p>
    Learn <mark>HTML</mark> before CSS.
</p>
```

---

# 60. `<small>`

`<small>` represents side comments or small print.

Example:

```html
<p>
    Main information.
    <small>Additional information.</small>
</p>
```

---

# 61. `<del>`

`<del>` represents deleted content.

Example:

```html
<p>
    Original price:
    <del>₹1000</del>
</p>
```

---

# 62. `<ins>`

`<ins>` represents inserted content.

Example:

```html
<p>
    New price:
    <ins>₹800</ins>
</p>
```

---

# 63. `<sub>`

`<sub>` represents subscript.

Example:

```html
H<sub>2</sub>O
```

Conceptually:

```text
H₂O
```

---

# 64. `<sup>`

`<sup>` represents superscript.

Example:

```html
X<sup>2</sup>
```

Conceptually:

```text
X²
```

---

# 65. HTML Entities

Some characters have special meanings in HTML.

Common entities:

```html
&lt;
&gt;
&amp;
&nbsp;
```

Meaning:

```text
&lt;   <
&gt;   >
&amp;  &
&nbsp; Non-breaking space
```

---

# 66. Why Do We Need HTML Entities?

The character:

```text
<
```

has special meaning because it starts an HTML tag.

If we want to display it as normal text, we can write:

```html
&lt;
```

Example:

```html
<p>
    5 &lt; 10
</p>
```

---

# 67. Greater Than Symbol

Use:

```html
&gt;
```

Example:

```html
<p>
    10 &gt; 5
</p>
```

---

# 68. Ampersand

Use:

```html
&amp;
```

Example:

```html
<p>
    HTML &amp; CSS
</p>
```

---

# 69. Non-Breaking Space

Use:

```html
&nbsp;
```

It represents a non-breaking space.

Example:

```html
<p>
    Hello&nbsp;World
</p>
```

Use it only when a non-breaking space is actually needed. Do not use it as a general replacement for CSS spacing.

---

# 70. Complete HTML5 Foundation Example

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>Student Profile</title>

    </head>

    <body>

        <!-- Main Page Heading -->

        <h1>Student Profile</h1>

        <hr>

        <!-- Student Information -->

        <h2>About the Student</h2>

        <p>
            My name is Alex.
        </p>

        <p>
            I am learning
            <strong>HTML</strong>
            as part of
            <em>Full Stack Development</em>.
        </p>

        <h2>Learning Goals</h2>

        <p>
            I want to learn HTML, CSS,
            JavaScript and Flask.
        </p>

        <h3>Current Topic</h3>

        <p>
            HTML is the foundation of web development.
        </p>

    </body>

</html>
```

---

# 71. Understand the Complete Document Tree

The previous example can be visualized as:

```text
DOCTYPE
│
└── html
    │
    ├── head
    │   │
    │   ├── meta
    │   ├── meta
    │   └── title
    │
    └── body
        │
        ├── comment
        ├── h1
        ├── hr
        ├── comment
        ├── h2
        ├── p
        ├── p
        ├── h2
        ├── p
        └── h3
```

This is a very important concept.

> **HTML is a hierarchical document structure.**

---

# 72. HTML Elements Covered Today

## Document Structure

```text
html
head
body
title
meta
```

## Headings

```text
h1
h2
h3
h4
h5
h6
```

## Text

```text
p
br
hr
strong
em
b
i
mark
small
del
ins
sub
sup
```

## Other

```text
DOCTYPE
comments
HTML entities
```

---

# 73. Attributes Covered Today

```text
lang
charset
name
content
```

Example:

```html
<html lang="en">
```

Example:

```html
<meta charset="UTF-8">
```

Example:

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0">
```

---

# 74. Important HTML Concepts

You should understand:

```text
HTML
HyperText
Markup
Browser
HTML File
.html
DOCTYPE
HTML Document
Tag
Element
Attribute
Attribute Value
Nesting
Parent
Child
Head
Body
Meta
Title
Heading
Paragraph
Comment
Text Markup
HTML Entity
```

---

# 75. Day 1 Practical Exercise

Create:

```text
student-profile.html
```

Create the following conceptual structure:

```text
Student Profile
│
├── Name
├── Education
├── Skills
├── Career Goal
└── Learning Journey
```

Use:

```html
<h1>
<h2>
<h3>
<p>
<strong>
<em>
<br>
<hr>
```

Also include:

```html
<!DOCTYPE html>
<html>
<head>
<meta>
<title>
<body>
```

Add at least two HTML comments.

---

# 76. Day 1 Practical Exercise — Expected Structure

Your file should broadly follow:

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>Student Profile</title>

    </head>

    <body>

        <!-- Main Heading -->

        <h1>Student Profile</h1>

        <!-- Personal Information -->

        <h2>About Me</h2>

        <p>
            My name is ...
        </p>

        <!-- Education -->

        <h2>Education</h2>

        <p>
            I completed ...
        </p>

        <!-- Skills -->

        <h2>Skills</h2>

        <p>
            My current skills include
            <strong>Python</strong>
            and <em>HTML</em>.
        </p>

        <!-- Career Goal -->

        <h2>Career Goal</h2>

        <p>
            My goal is ...
        </p>

    </body>

</html>
```

---

# 77. Day 1 Challenge

Create:

```text
course.html
```

The page represents:

```text
Python Full Stack Development
│
├── Introduction
│
├── Frontend
│   ├── HTML
│   ├── CSS
│   └── JavaScript
│
├── Backend
│   └── Flask
│
└── Database
```

Use heading hierarchy.

Example:

```html
<h1>Python Full Stack Development</h1>

<h2>Introduction</h2>

<h2>Frontend</h2>

<h3>HTML</h3>

<h3>CSS</h3>

<h3>JavaScript</h3>

<h2>Backend</h2>

<h3>Flask</h3>

<h2>Database</h2>
```

---

# 78. Day 1 Challenge — Add Content

Add paragraphs under each heading.

Example:

```html
<h2>Frontend</h2>

<p>
    Frontend development focuses on the part
    of the application users interact with.
</p>
```

Then:

```html
<h3>HTML</h3>

<p>
    HTML provides structure and content.
</p>
```

Then:

```html
<h3>CSS</h3>

<p>
    CSS provides presentation and styling.
</p>
```

Then:

```html
<h3>JavaScript</h3>

<p>
    JavaScript provides behaviour and interaction.
</p>
```

---

# 79. Day 1 — One Hour Schedule

| Time      | Topic                                   |
| --------- | --------------------------------------- |
| 0–10 min  | HTML, HyperText, Markup, Browser        |
| 10–20 min | `.html`, DOCTYPE, HTML document         |
| 20–30 min | `html`, `head`, `body`, `meta`, `title` |
| 30–40 min | Tags, elements, attributes, nesting     |
| 40–50 min | Headings, paragraphs, text markup       |
| 50–60 min | Practical HTML coding                   |

---

# 80. Day 1 — Learning Method

Do not only read the examples.

For every concept:

```text
Read
↓
Understand
↓
Type
↓
Run in Browser
↓
Change the Code
↓
Observe
↓
Explain
```

For example:

```html
<h1>Hello</h1>
```

Change it to:

```html
<h1>Welcome Students</h1>
```

Then:

```html
<h2>HTML Course</h2>
```

Then:

```html
<p>
    I am learning HTML.
</p>
```

The objective is to become comfortable writing HTML manually.

---

# 81. Day 1 — Self-Test

Answer these without looking at the notes.

## Q1. What does HTML stand for?

---

## Q2. Is HTML a programming language?

---

## Q3. What is HyperText?

---

## Q4. What does Markup mean?

---

## Q5. What is the purpose of:

```html
<!DOCTYPE html>
```

---

## Q6. What is the root element of an HTML document?

---

## Q7. What is the purpose of `<head>`?

---

## Q8. What is the purpose of `<body>`?

---

## Q9. What is the purpose of `<title>`?

---

## Q10. What is the purpose of:

```html
<meta charset="UTF-8">
```

---

## Q11. What is an HTML tag?

---

## Q12. What is an HTML element?

---

## Q13. What is an attribute?

---

## Q14. Where are attributes normally written?

---

## Q15. What is nesting?

---

## Q16. What is a parent element?

---

## Q17. What is a child element?

---

## Q18. What is the difference between:

```html
<p>
```

and:

```html
<p>Hello</p>
```

---

## Q19. What is the purpose of `<h1>`?

---

## Q20. How many heading levels does HTML provide?

---

## Q21. What is the purpose of `<p>`?

---

## Q22. What is the purpose of `<br>`?

---

## Q23. What is a void element?

---

## Q24. What is the purpose of `<hr>`?

---

## Q25. What is the difference between `<strong>` and `<b>`?

---

## Q26. What is the difference between `<em>` and `<i>`?

---

## Q27. What is an HTML comment?

---

## Q28. What is an HTML entity?

---

## Q29. What does:

```html
&lt;
```

represent?

---

## Q30. What does:

```html
&amp;
```

represent?

---

# 82. Day 1 — Interview Questions

### 1. What is HTML?

HTML is the standard markup language used to structure web content.

### 2. Why is HTML called a markup language?

Because it uses markup tags to describe the structure and meaning of content.

### 3. Is HTML case-sensitive?

HTML syntax is generally treated as case-insensitive for element and attribute names, but lowercase is the standard convention and recommended practice.

### 4. What is HTML5?

HTML5 is the modern HTML standard that introduced and standardized many semantic elements, multimedia capabilities, form features, and APIs.

### 5. What is DOCTYPE?

It is the document type declaration that tells the browser which parsing mode to use. In modern HTML it is:

```html
<!DOCTYPE html>
```

### 6. What is the difference between `<head>` and `<body>`?

`<head>` contains document metadata and related information.

`<body>` contains the page's actual content.

### 7. What is an HTML element?

An HTML element consists of an opening tag, content when applicable, and a closing tag.

Example:

```html
<p>Hello</p>
```

### 8. What is an attribute?

An attribute provides additional information about an HTML element.

Example:

```html
<a href="about.html">
```

### 9. What is nesting?

Nesting means placing one HTML element inside another.

### 10. What are void elements?

Void elements do not have normal closing tags.

Examples:

```text
br
hr
img
input
meta
link
```

---

# 83. Day 1 — Common Mistakes

## Mistake 1 — Forgetting DOCTYPE

Incorrect:

```html
<html>
```

Preferred:

```html
<!DOCTYPE html>

<html>
```

---

## Mistake 2 — Incorrect Nesting

Incorrect:

```html
<p>
    <strong>Hello
</p>
</strong>
```

Correct:

```html
<p>
    <strong>Hello</strong>
</p>
```

---

## Mistake 3 — Putting Page Content in `<head>`

Avoid:

```html
<head>

    <h1>Welcome</h1>

</head>
```

Normal page content belongs in:

```html
<body>
```

---

## Mistake 4 — Forgetting `<title>`

A proper page should normally include:

```html
<head>

    <title>My Website</title>

</head>
```

---

## Mistake 5 — Treating Headings as Styling Tools

Do not choose:

```html
<h1>
```

just because you want large text.

Choose headings according to document hierarchy.

CSS will handle presentation later.

---

## Mistake 6 — Using `<br>` for Page Layout

Do not create page layout using many `<br>` elements.

Bad:

```html
<p>
    Hello
    <br><br><br><br>
    Welcome
</p>
```

HTML should provide structure.

CSS will later control spacing and layout.

---

# 84. Day 1 — Important Mental Model

Think of HTML as a tree.

```text
HTML Document
│
└── html
    │
    ├── head
    │   ├── meta
    │   └── title
    │
    └── body
        │
        ├── h1
        ├── p
        ├── h2
        ├── p
        └── section
            │
            ├── h3
            └── p
```

This tree is extremely important.

Later:

```text
HTML
↓
DOM
↓
JavaScript
```

JavaScript will interact with this document structure.

---

# 85. HTML → DOM Connection

Suppose HTML contains:

```html
<h1 id="title">
    Welcome
</h1>
```

The browser creates a document structure from this HTML.

Later JavaScript can access it using:

```javascript
document.getElementById("title");
```

Therefore:

```text
HTML
↓
Creates document structure

Browser
↓
Parses HTML

DOM
↓
Represents the document

JavaScript
↓
Interacts with the DOM
```

You do not need to learn JavaScript DOM programming today.

Just understand the connection.

---

# 86. Day 1 — Important Tags Reference

## Document

```text
html
head
body
title
meta
```

## Headings

```text
h1
h2
h3
h4
h5
h6
```

## Text

```text
p
br
hr
strong
em
b
i
mark
small
del
ins
sub
sup
```

## Other

```text
comments
entities
```

---

# 87. Day 1 — Important Attributes Reference

```text
lang
charset
name
content
```

Examples:

```html
<html lang="en">
```

```html
<meta charset="UTF-8">
```

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0">
```

---

# 88. Day 1 — Complete Practice Page

Create this yourself rather than copying it first.

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

        <!-- Main Heading -->

        <h1>Python Full Stack Development</h1>

        <p>
            Welcome to the Python Full Stack Development course.
        </p>

        <hr>

        <!-- Frontend -->

        <h2>Frontend Development</h2>

        <p>
            Frontend development focuses on
            the structure, presentation and
            behaviour of web pages.
        </p>

        <h3>HTML</h3>

        <p>
            <strong>HTML</strong>
            provides the structure of web pages.
        </p>

        <h3>CSS</h3>

        <p>
            <strong>CSS</strong>
            provides presentation and styling.
        </p>

        <h3>JavaScript</h3>

        <p>
            <strong>JavaScript</strong>
            provides behaviour and interaction.
        </p>

        <hr>

        <!-- Backend -->

        <h2>Backend Development</h2>

        <p>
            Flask can be used to build
            Python web applications.
        </p>

        <h3>Flask</h3>

        <p>
            Flask is a Python web framework.
        </p>

        <hr>

        <!-- Database -->

        <h2>Database</h2>

        <p>
            Web applications commonly store
            application data in databases.
        </p>

    </body>

</html>
```

---

# 89. Day 1 — What You Must Remember

The most important concepts are:

```text
HTML
↓
HyperText Markup Language

HTML
↓
Markup Language

HTML
↓
Structure + Content

HTML File
↓
.html

HTML Document
↓
DOCTYPE
↓
html
↓
head
+
body

HTML
↓
Tags
↓
Elements
↓
Attributes
↓
Nesting
↓
Parent / Child
```

---

# 90. Day 1 — Completion Checklist

Before moving to **Day 37 — Day 2**, you should be able to:

* [ ] Explain what HTML means
* [ ] Explain HyperText
* [ ] Explain Markup
* [ ] Explain why HTML is not a programming language
* [ ] Explain what a browser does
* [ ] Create an `.html` file
* [ ] Explain `index.html`
* [ ] Write `<!DOCTYPE html>` from memory
* [ ] Create `<html>`
* [ ] Create `<head>`
* [ ] Create `<body>`
* [ ] Add `<title>`
* [ ] Add `<meta charset="UTF-8">`
* [ ] Add viewport metadata
* [ ] Explain tags
* [ ] Explain elements
* [ ] Explain attributes
* [ ] Explain attribute values
* [ ] Understand nesting
* [ ] Understand parent and child
* [ ] Create `<h1>` through `<h6>`
* [ ] Create paragraphs
* [ ] Use `<br>`
* [ ] Use `<hr>`
* [ ] Use `<strong>`
* [ ] Use `<em>`
* [ ] Understand `<b>` and `<i>`
* [ ] Use `<mark>`
* [ ] Use `<small>`
* [ ] Use `<del>`
* [ ] Use `<ins>`
* [ ] Use `<sub>`
* [ ] Use `<sup>`
* [ ] Write HTML comments
* [ ] Understand HTML entities
* [ ] Build a complete HTML document
* [ ] Open the document in a browser
* [ ] Inspect the HTML document structure

---

# 91. Day 1 — Final Goal

At the end of **Day 36**, you should be able to look at a blank file and independently write:

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>My Web Page</title>

    </head>

    <body>

        <h1>My Web Page</h1>

        <h2>Introduction</h2>

        <p>
            This is my first HTML page.
        </p>

    </body>

</html>
```

You should understand **why every major part exists**, not merely memorize the syntax.

---

# 92. Front-End Course Roadmap

```text
DAY 36
│
└── HTML Foundation
    ├── HTML
    ├── HyperText
    ├── Markup
    ├── Browser
    ├── .html
    ├── DOCTYPE
    ├── html
    ├── head
    ├── body
    ├── meta
    ├── title
    ├── Tags
    ├── Elements
    ├── Attributes
    ├── Nesting
    ├── Headings
    ├── Paragraphs
    ├── Text Markup
    ├── Comments
    └── Entities

        ↓

DAY 37
│
└── HTML Content
    ├── Links
    ├── Images
    ├── Lists
    ├── Tables
    ├── Paths
    ├── div
    ├── span
    └── Semantic HTML

        ↓

DAY 38
│
└── HTML Forms + HTML5
    ├── Forms
    ├── Input Types
    ├── Labels
    ├── Select
    ├── Textarea
    ├── Buttons
    ├── Validation
    ├── Audio
    ├── Video
    ├── iframe
    ├── Accessibility
    ├── Global Attributes
    └── Mini Project

        ↓

CSS

        ↓

JavaScript

        ↓

Flask
```

---

# DAY 1 — FINAL SUMMARY

```text
HTML
=
HyperText Markup Language

HTML
=
Structure + Content

HTML Document
=
DOCTYPE
+
html
+
head
+
body

HEAD
=
Document Information

BODY
=
Page Content

HTML
=
Tags
+
Elements
+
Attributes
+
Nesting

Basic Content
=
h1-h6
+
p
+
br
+
hr

Text Markup
=
strong
+
em
+
b
+
i
+
mark
+
small
+
del
+
ins
+
sub
+
sup

Other Foundation Concepts
=
Comments
+
Entities
+
Parent / Child
+
Document Tree
```

---

# DAY 1 — END

**Day 36 — HTML Foundation Completed**

**Next: Day 37 — HTML Content, Links, Images, Lists, Tables, Paths, `div`, `span` and Semantic HTML**

```
```
