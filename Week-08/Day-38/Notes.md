# DAY 3 — HTML FORMS, INPUTS, VALIDATION, MULTIMEDIA, IFRAME, GLOBAL ATTRIBUTES & ACCESSIBILITY

## Front-End Development — Day 38

**Duration:** 1 Hour  
**Level:** Beginner → Intermediate  
**Module:** Front-End Development  
**Topic:** HTML — Forms, HTML5 Features & Practical HTML  
**Focus:** HTML Only

> **Day 38 = HTML Forms + HTML5**
>
> CSS, JavaScript and Flask are intentionally not covered today.

---

# 1. Day 3 Objective

By the end of Day 3, you should be able to create a structured HTML form and understand the most important HTML5 features used in real websites.

Today we cover:

```text
Forms
Labels
Inputs
Input Types
Name
Value
Placeholder
Required
Select
Option
Textarea
Button
Fieldset
Legend
Form Validation
Checkbox
Radio Button
File Input
Date
Number
Email
Password
URL
Search
Range
Color
Audio
Video
iframe
Global Attributes
Accessibility
HTML5
```

The goal is:

```text
HTML Page
    ↓
HTML Content
    ↓
HTML Forms
    ↓
User Input
    ↓
HTML5 Features
    ↓
Real Website Structure
```

---

# 2. Day 1 → Day 2 → Day 3

```text
DAY 36
HTML FOUNDATION
│
├── HTML
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
└── Text Markup

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

        ↓

DAY 38
HTML FORMS + HTML5
│
├── Forms
├── Labels
├── Inputs
├── Input Types
├── Select
├── Textarea
├── Buttons
├── Validation
├── Multimedia
├── iframe
├── Global Attributes
├── Accessibility
└── Mini Project
```

---

# 3. Why Do We Need Forms?

Most websites need to receive information from users.

Examples:

```text
Login
Registration
Contact
Search
Feedback
Job Application
Course Enrollment
Payment Information
Profile
File Upload
```

HTML provides the structure for collecting this information.

---

# 4. The `<form>` Element

The main form element is:

```html
<form>
</form>
```

Example:

```html
<form>

    <label>Name</label>

    <input type="text">

</form>
```

A form groups controls used for collecting user input.

---

# 5. Basic Form

```html
<form>

    <label>Name:</label>

    <input type="text">

    <button type="submit">
        Submit
    </button>

</form>
```

Structure:

```text
form
│
├── label
├── input
└── button
```

---

# 6. The `<label>` Element

A label describes a form control.

Example:

```html
<label>
    Name
</label>

<input type="text">
```

Better:

```html
<label for="name">
    Name
</label>

<input
    type="text"
    id="name">
```

The `for` value should match the input's `id`.

---

# 7. Label Relationship

Example:

```html
<label for="email">
    Email
</label>

<input
    type="email"
    id="email">
```

Relationship:

```text
label
│
└── for="email"
          │
          ↓
input
└── id="email"
```

This connects the label to the form control.

---

# 8. Why Labels Matter

Labels improve:

```text
Usability
Accessibility
Form Understanding
Click Target
Screen Reader Interpretation
```

Do not create forms without meaningful labels.

---

# 9. `<input>`

The most commonly used form control is:

```html
<input>
```

It is a void element.

Example:

```html
<input type="text">
```

There is no:

```html
</input>
```

---

# 10. Text Input

```html
<label for="name">
    Name
</label>

<input
    type="text"
    id="name">
```

Used for:

```text
Name
Username
City
Job Title
Course
```

---

# 11. `name` Attribute

The `name` attribute identifies the form control when form data is submitted.

Example:

```html
<input
    type="text"
    id="name"
    name="name">
```

Think:

```text
id
↓
Identifies element in the document

name
↓
Identifies submitted form field
```

---

# 12. `value` Attribute

`value` specifies the current/default value of many form controls.

Example:

```html
<input
    type="text"
    name="country"
    value="India">
```

For a button:

```html
<input
    type="submit"
    value="Submit">
```

---

# 13. `placeholder`

A placeholder provides a hint about expected input.

Example:

```html
<input
    type="text"
    name="username"
    placeholder="Enter your username">
```

Important:

```text
placeholder
↓
Hint

label
↓
Actual description
```

Do not use placeholder as a replacement for a label.

---

# 14. Required Fields

Use:

```html
required
```

Example:

```html
<input
    type="text"
    name="name"
    required>
```

The browser will prevent normal form submission when the required field has not been completed.

---

# 15. Email Input

Use:

```html
<input type="email">
```

Example:

```html
<label for="email">
    Email
</label>

<input
    type="email"
    id="email"
    name="email"
    required>
```

Browsers can perform basic built-in validation for email input.

---

# 16. Password Input

Use:

```html
<input type="password">
```

Example:

```html
<label for="password">
    Password
</label>

<input
    type="password"
    id="password"
    name="password"
    required>
```

The browser hides the characters visually.

---

# 17. Number Input

Use:

```html
<input type="number">
```

Example:

```html
<label for="age">
    Age
</label>

<input
    type="number"
    id="age"
    name="age">
```

Useful attributes:

```text
min
max
step
```

Example:

```html
<input
    type="number"
    name="age"
    min="18"
    max="100">
```

---

# 18. `min`, `max`, `step`

Example:

```html
<input
    type="number"
    min="0"
    max="100"
    step="5">
```

Meaning:

```text
minimum = 0
maximum = 100
increment = 5
```

---

# 19. Date Input

Use:

```html
<input type="date">
```

Example:

```html
<label for="dob">
    Date of Birth
</label>

<input
    type="date"
    id="dob"
    name="dob">
```

The browser provides an appropriate date control.

---

# 20. Time Input

```html
<input
    type="time"
    name="appointment_time">
```

Useful for:

```text
Appointment
Meeting
Class Time
Booking
```

---

# 21. Date and Time

HTML also supports:

```html
<input type="datetime-local">
```

Example:

```html
<label for="meeting">
    Meeting
</label>

<input
    type="datetime-local"
    id="meeting"
    name="meeting">
```

This represents a local date and time.

---

# 22. Month Input

```html
<input
    type="month"
    name="joining_month">
```

This allows selection of a month and year.

---

# 23. Week Input

```html
<input
    type="week"
    name="training_week">
```

This represents a week of a year.

---

# 24. URL Input

Use:

```html
<input type="url">
```

Example:

```html
<label for="website">
    Website
</label>

<input
    type="url"
    id="website"
    name="website">
```

---

# 25. Telephone Input

Use:

```html
<input type="tel">
```

Example:

```html
<label for="phone">
    Phone
</label>

<input
    type="tel"
    id="phone"
    name="phone">
```

`tel` indicates that the field is intended for telephone numbers.

---

# 26. Search Input

Use:

```html
<input type="search">
```

Example:

```html
<label for="search">
    Search
</label>

<input
    type="search"
    id="search"
    name="q">
```

---

# 27. Radio Buttons

Radio buttons allow selection of one option from a group.

Example:

```html
<p>Gender</p>

<input
    type="radio"
    id="male"
    name="gender"
    value="male">

<label for="male">
    Male
</label>

<input
    type="radio"
    id="female"
    name="gender"
    value="female">

<label for="female">
    Female
</label>
```

The important concept:

```text
Same name
↓
Same radio group
```

---

# 28. Radio Button Group

Example:

```html
<input
    type="radio"
    name="course"
    value="python">

<label>
    Python
</label>

<input
    type="radio"
    name="course"
    value="java">

<label>
    Java
</label>

<input
    type="radio"
    name="course"
    value="javascript">

<label>
    JavaScript
</label>
```

Because all three have:

```text
name="course"
```

they form one group.

---

# 29. Checkbox

Checkboxes allow independent selections.

Example:

```html
<input
    type="checkbox"
    id="html"
    name="skills"
    value="html">

<label for="html">
    HTML
</label>
```

Multiple checkboxes can be selected.

---

# 30. Multiple Checkboxes

```html
<input
    type="checkbox"
    id="html"
    name="skills"
    value="html">

<label for="html">
    HTML
</label>

<input
    type="checkbox"
    id="css"
    name="skills"
    value="css">

<label for="css">
    CSS
</label>

<input
    type="checkbox"
    id="javascript"
    name="skills"
    value="javascript">

<label for="javascript">
    JavaScript
</label>
```

Possible selection:

```text
HTML       ✓
CSS        ✓
JavaScript ☐
```

---

# 31. Radio vs Checkbox

```text
Radio
↓
Usually one choice from a group

Checkbox
↓
Zero, one or multiple independent choices
```

Example:

```text
Gender
○ Male
○ Female
○ Other
```

Radio.

```text
Skills
☐ HTML
☐ CSS
☐ JavaScript
```

Checkbox.

---

# 32. File Input

Use:

```html
<input type="file">
```

Example:

```html
<label for="resume">
    Upload Resume
</label>

<input
    type="file"
    id="resume"
    name="resume">
```

Used for:

```text
Resume
Profile Photo
Documents
Certificates
```

---

# 33. Multiple File Selection

Use:

```html
<input
    type="file"
    name="documents"
    multiple>
```

The `multiple` attribute allows selection of multiple files where supported.

---

# 34. Accept Attribute

You can indicate expected file types:

```html
<input
    type="file"
    name="resume"
    accept=".pdf">
```

Another example:

```html
<input
    type="file"
    name="photo"
    accept="image/*">
```

`accept` provides a hint to the browser about file types.

---

# 35. Hidden Input

Use:

```html
<input
    type="hidden"
    name="user_id"
    value="101">
```

A hidden input is not normally visible to the user.

Important:

```text
Hidden does NOT mean secure.
```

Users can inspect and modify client-side HTML.

Never trust hidden fields for security decisions.

---

# 36. Color Input

HTML provides:

```html
<input type="color">
```

Example:

```html
<label for="favorite_color">
    Favorite Color
</label>

<input
    type="color"
    id="favorite_color"
    name="favorite_color">
```

CSS is not being used here. This is an HTML input control.

---

# 37. Range Input

Use:

```html
<input type="range">
```

Example:

```html
<label for="volume">
    Volume
</label>

<input
    type="range"
    id="volume"
    name="volume"
    min="0"
    max="100">
```

---

# 38. Submit Input

Example:

```html
<input
    type="submit"
    value="Register">
```

It submits the form.

---

# 39. Reset Input

Example:

```html
<input
    type="reset"
    value="Reset">
```

It resets form controls to their initial values.

---

# 40. Button Element

HTML provides:

```html
<button>
</button>
```

Example:

```html
<button type="submit">
    Register
</button>
```

---

# 41. Button Types

Important button types:

```text
submit
reset
button
```

Example:

```html
<button type="submit">
    Submit
</button>

<button type="reset">
    Reset
</button>

<button type="button">
    Normal Button
</button>
```

The `button` type does not submit the form by itself.

---

# 42. Why Explicit Button Type Matters

Inside a form:

```html
<button>
    Click
</button>
```

The default behavior of a button in a form is generally submit.

Therefore, when a button should not submit the form, explicitly use:

```html
<button type="button">
    Click
</button>
```

---

# 43. `<textarea>`

For multi-line text, use:

```html
<textarea>
</textarea>
```

Example:

```html
<label for="message">
    Message
</label>

<textarea
    id="message"
    name="message">
</textarea>
```

Useful attributes include:

```text
rows
cols
placeholder
required
maxlength
minlength
```

---

# 44. Textarea Example

```html
<label for="feedback">
    Feedback
</label>

<textarea
    id="feedback"
    name="feedback"
    rows="5"
    cols="40"
    placeholder="Enter your feedback">
</textarea>
```

---

# 45. `<select>`

Use `<select>` for a selection control.

Example:

```html
<label for="course">
    Course
</label>

<select
    id="course"
    name="course">

    <option value="python">
        Python
    </option>

    <option value="java">
        Java
    </option>

    <option value="javascript">
        JavaScript
    </option>

</select>
```

---

# 46. `<option>`

Each choice inside a select is represented by:

```html
<option>
```

Example:

```html
<option value="python">
    Python
</option>
```

There are two concepts:

```text
Displayed text
↓
Python

Submitted value
↓
python
```

---

# 47. `selected`

To make an option initially selected:

```html
<option
    value="python"
    selected>
    Python
</option>
```

---

# 48. `disabled`

A control can be disabled.

Example:

```html
<input
    type="text"
    disabled>
```

Disabled controls generally cannot be edited or activated by the user.

---

# 49. Disabled Option

```html
<option
    value=""
    disabled
    selected>
    Select Course
</option>
```

This can provide an initial prompt.

---

# 50. `<optgroup>`

Options can be grouped.

Example:

```html
<select name="course">

    <optgroup label="Programming">

        <option value="python">
            Python
        </option>

        <option value="java">
            Java
        </option>

    </optgroup>

    <optgroup label="Web">

        <option value="html">
            HTML
        </option>

        <option value="javascript">
            JavaScript
        </option>

    </optgroup>

</select>
```

---

# 51. `<datalist>`

`datalist` provides suggested values for an input.

Example:

```html
<label for="browser">
    Browser
</label>

<input
    list="browsers"
    id="browser"
    name="browser">

<datalist id="browsers">

    <option value="Chrome">

    <option value="Firefox">

    <option value="Edge">

    <option value="Safari">

</datalist>
```

Important:

```text
select
↓
Choose from defined options

datalist
↓
Suggestions for an input
```

---

# 52. `<fieldset>`

`fieldset` groups related form controls.

Example:

```html
<fieldset>

    <legend>
        Personal Information
    </legend>

    <label for="name">
        Name
    </label>

    <input
        type="text"
        id="name"
        name="name">

</fieldset>
```

---

# 53. `<legend>`

`legend` provides a caption for a `<fieldset>`.

Example:

```html
<fieldset>

    <legend>
        Contact Information
    </legend>

    ...

</fieldset>
```

---

# 54. Form Grouping

A larger form can be organized:

```html
<form>

    <fieldset>

        <legend>
            Personal Information
        </legend>

        ...

    </fieldset>

    <fieldset>

        <legend>
            Course Information
        </legend>

        ...

    </fieldset>

</form>
```

This makes the form structure clearer.

---

# 55. Form `action`

A form can specify where the submitted data should go.

Example:

```html
<form action="/register">
```

The `action` attribute specifies the form submission destination.

Later, Flask will handle these requests on the server.

---

# 56. Form `method`

A form can specify how data is submitted.

Common methods:

```text
GET
POST
```

Example:

```html
<form
    action="/search"
    method="get">
```

Another:

```html
<form
    action="/register"
    method="post">
```

---

# 57. GET Method

Example:

```html
<form
    action="/search"
    method="get">

    <input
        type="search"
        name="q">

    <button type="submit">
        Search
    </button>

</form>
```

GET is commonly used for requests that retrieve information.

The submitted values may appear in the URL as query parameters.

Example conceptually:

```text
/search?q=python
```

---

# 58. POST Method

Example:

```html
<form
    action="/register"
    method="post">

    <input
        type="text"
        name="name">

    <button type="submit">
        Register
    </button>

</form>
```

POST is commonly used when submitting data to be processed or changed on the server.

---

# 59. GET vs POST

Basic mental model:

```text
GET
↓
Retrieve/search data

POST
↓
Submit data for processing
```

Do not interpret this as a security rule.

For example:

```text
GET is not "secure"
POST is not automatically "secure"
```

Security requires HTTPS and proper server-side handling.

---

# 60. Form Validation

HTML provides built-in validation features.

Important attributes:

```text
required
min
max
minlength
maxlength
pattern
type
```

---

# 61. `minlength`

Example:

```html
<input
    type="text"
    name="username"
    minlength="4">
```

The user should provide at least the specified number of characters.

---

# 62. `maxlength`

Example:

```html
<input
    type="text"
    name="username"
    maxlength="20">
```

The control limits the number of characters entered.

---

# 63. `pattern`

The `pattern` attribute allows a regular expression constraint.

Example:

```html
<input
    type="text"
    name="code"
    pattern="[A-Z]{3}[0-9]{3}">
```

Conceptually:

```text
ABC123
```

matches the pattern.

---

# 64. Pattern Is Not Security

Client-side validation can be bypassed.

Therefore:

```text
HTML Validation
↓
User Experience + Basic Client-Side Validation

Server-Side Validation
↓
Security + Data Integrity
```

When Flask is introduced, validation must also be performed on the server.

---

# 65. Complete Registration Form

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>Student Registration</title>

    </head>

    <body>

        <main>

            <h1>Student Registration</h1>

            <form
                action="/register"
                method="post">

                <fieldset>

                    <legend>
                        Personal Information
                    </legend>

                    <p>

                        <label for="name">
                            Full Name
                        </label>

                        <input
                            type="text"
                            id="name"
                            name="name"
                            required>

                    </p>

                    <p>

                        <label for="email">
                            Email
                        </label>

                        <input
                            type="email"
                            id="email"
                            name="email"
                            required>

                    </p>

                    <p>

                        <label for="phone">
                            Phone
                        </label>

                        <input
                            type="tel"
                            id="phone"
                            name="phone">

                    </p>

                    <p>

                        <label for="dob">
                            Date of Birth
                        </label>

                        <input
                            type="date"
                            id="dob"
                            name="dob">

                    </p>

                </fieldset>

                <fieldset>

                    <legend>
                        Course Information
                    </legend>

                    <p>

                        <label for="course">
                            Course
                        </label>

                        <select
                            id="course"
                            name="course"
                            required>

                            <option
                                value=""
                                selected
                                disabled>
                                Select Course
                            </option>

                            <option value="python">
                                Python
                            </option>

                            <option value="javascript">
                                JavaScript
                            </option>

                            <option value="fullstack">
                                Full Stack
                            </option>

                        </select>

                    </p>

                    <p>

                        <label>
                            Mode
                        </label>

                        <input
                            type="radio"
                            id="online"
                            name="mode"
                            value="online">

                        <label for="online">
                            Online
                        </label>

                        <input
                            type="radio"
                            id="offline"
                            name="mode"
                            value="offline">

                        <label for="offline">
                            Offline
                        </label>

                    </p>

                </fieldset>

                <fieldset>

                    <legend>
                        Skills
                    </legend>

                    <input
                        type="checkbox"
                        id="html"
                        name="skills"
                        value="html">

                    <label for="html">
                        HTML
                    </label>

                    <input
                        type="checkbox"
                        id="css"
                        name="skills"
                        value="css">

                    <label for="css">
                        CSS
                    </label>

                    <input
                        type="checkbox"
                        id="javascript"
                        name="skills"
                        value="javascript">

                    <label for="javascript">
                        JavaScript
                    </label>

                </fieldset>

                <fieldset>

                    <legend>
                        Message
                    </legend>

                    <label for="message">
                        Message
                    </label>

                    <textarea
                        id="message"
                        name="message"
                        rows="5"
                        cols="40">
                    </textarea>

                </fieldset>

                <button type="submit">
                    Register
                </button>

                <button type="reset">
                    Reset
                </button>

            </form>

        </main>

    </body>

</html>
```

---

# 66. HTML Multimedia

HTML5 introduced native multimedia elements.

Important elements:

```text
audio
video
source
track
```

---

# 67. Audio

Basic example:

```html
<audio controls>

    <source
        src="audio/song.mp3"
        type="audio/mpeg">

</audio>
```

The `controls` attribute provides browser controls.

---

# 68. Audio with Multiple Sources

```html
<audio controls>

    <source
        src="audio/song.mp3"
        type="audio/mpeg">

    <source
        src="audio/song.ogg"
        type="audio/ogg">

    Your browser does not support audio.

</audio>
```

The browser can choose a supported source.

---

# 69. Important Audio Attributes

Common attributes:

```text
controls
autoplay
loop
muted
preload
```

Example:

```html
<audio
    controls
    loop>

    <source
        src="audio/song.mp3"
        type="audio/mpeg">

</audio>
```

---

# 70. Video

Basic example:

```html
<video controls>

    <source
        src="videos/course.mp4"
        type="video/mp4">

</video>
```

---

# 71. Video Width and Height

Example:

```html
<video
    controls
    width="640"
    height="360">

    <source
        src="videos/course.mp4"
        type="video/mp4">

</video>
```

CSS will later provide better responsive sizing.

---

# 72. Video Poster

A poster image can be specified:

```html
<video
    controls
    poster="images/video-cover.jpg">

    <source
        src="videos/course.mp4"
        type="video/mp4">

</video>
```

The poster is displayed before playback.

---

# 73. Video Multiple Sources

```html
<video controls>

    <source
        src="videos/course.mp4"
        type="video/mp4">

    <source
        src="videos/course.webm"
        type="video/webm">

    Your browser does not support video.

</video>
```

---

# 74. Track and Captions

Video can include text tracks:

```html
<video controls>

    <source
        src="course.mp4"
        type="video/mp4">

    <track
        src="captions.vtt"
        kind="captions"
        srclang="en"
        label="English">

</video>
```

The `<track>` element can provide captions and other timed text.

---

# 75. Why Captions Matter

Captions improve:

```text
Accessibility
Understanding
Learning
Content Availability
```

They are especially important for users who cannot hear the audio or prefer reading along.

---

# 76. iframe

The `<iframe>` element embeds another HTML browsing context.

Example:

```html
<iframe
    src="https://example.com"
    title="Example website">
</iframe>
```

---

# 77. Common iframe Uses

Examples:

```text
Maps
Videos
External Documents
Embedded Pages
Online Tools
```

---

# 78. iframe with Width and Height

Example:

```html
<iframe
    src="https://example.com"
    title="Example website"
    width="600"
    height="400">
</iframe>
```

CSS can later control responsive sizing.

---

# 79. YouTube Embed Concept

A video platform can provide an iframe embed code.

Conceptually:

```html
<iframe
    src="..."
    title="Course Video">
</iframe>
```

The exact URL depends on the video and platform.

---

# 80. iframe Security Concept

An iframe can be restricted using:

```text
sandbox
allow
referrerpolicy
```

Example:

```html
<iframe
    src="https://example.com"
    title="Example"
    sandbox>
</iframe>
```

`sandbox` applies restrictions to the embedded document.

---

# 81. HTML Global Attributes

Global attributes can generally be used on many HTML elements.

Important ones:

```text
id
class
title
lang
dir
hidden
tabindex
data-*
contenteditable
draggable
spellcheck
```

Some have special behavior and applicability rules.

---

# 82. `id`

Example:

```html
<section id="courses">
```

`id` identifies an element.

It can be used for:

```text
Fragment links
CSS
JavaScript
DOM identification
```

---

# 83. `class`

Example:

```html
<section class="course">
```

Multiple elements can share the same class.

Example:

```html
<article class="course">
    ...
</article>

<article class="course">
    ...
</article>
```

Today we are only learning the HTML meaning.

CSS will use classes extensively later.

---

# 84. `id` vs `class`

Basic mental model:

```text
id
↓
Specific element identifier

class
↓
Reusable grouping/category
```

Example:

```html
<h1 id="main-title">
    Courses
</h1>

<article class="course">
    Python
</article>

<article class="course">
    JavaScript
</article>
```

---

# 85. `title`

The `title` attribute can provide advisory information.

Example:

```html
<p title="This is additional information">
    HTML
</p>
```

Do not rely on `title` as the primary way to communicate essential information.

---

# 86. `lang`

The `lang` attribute identifies the language of content.

Example:

```html
<html lang="en">
```

For another language:

```html
<html lang="te">
```

This helps browsers and assistive technologies interpret the document language.

---

# 87. `dir`

`dir` controls text direction.

Common values:

```text
ltr
rtl
auto
```

Example:

```html
<p dir="ltr">
    Hello
</p>
```

Right-to-left example:

```html
<p dir="rtl">
    ...
</p>
```

---

# 88. `hidden`

The `hidden` attribute indicates that an element is not currently relevant for presentation.

Example:

```html
<p hidden>
    This content is hidden.
</p>
```

Important:

```text
hidden
↓
Not visible in normal rendering

hidden
≠
Security
```

Do not put secrets into hidden HTML.

---

# 89. `data-*` Attributes

Custom data attributes can store application-specific data.

Example:

```html
<article
    data-course-id="101">

    Python Full Stack

</article>
```

Another:

```html
<button
    data-student-id="5001">

    View Student

</button>
```

Later JavaScript can access these values.

---

# 90. `contenteditable`

An element can be made editable by the user:

```html
<p contenteditable="true">
    Edit this text.
</p>
```

This creates browser-level editable content.

---

# 91. `spellcheck`

Example:

```html
<textarea
    spellcheck="true">
</textarea>
```

This indicates whether browser spell checking should be enabled where supported.

---

# 92. `tabindex`

`tabindex` can control keyboard focus behavior.

Example:

```html
<button tabindex="0">
    Submit
</button>
```

Be careful with positive tabindex values because poor focus ordering can hurt accessibility.

---

# 93. Accessibility

HTML should be written so that people using assistive technologies can understand and operate the page.

Important practices:

```text
Use semantic HTML
Use labels
Use meaningful headings
Use alt text
Use descriptive links
Use keyboard-friendly controls
Use correct language
Use captions where appropriate
```

---

# 94. Heading Structure

Good:

```html
<h1>
    Python Full Stack
</h1>

<h2>
    Frontend
</h2>

<h3>
    HTML
</h3>

<h3>
    CSS
</h3>

<h2>
    Backend
</h2>
```

The headings communicate hierarchy.

---

# 95. Avoid Heading Misuse

Do not choose headings only because they look visually large.

Bad:

```html
<h1>
    Small piece of text
</h1>

<h6>
    Important section
</h6>
```

Heading levels should represent document structure.

CSS will later control visual appearance.

---

# 96. Descriptive Link Text

Avoid:

```html
<a href="courses.html">
    Click here
</a>
```

Prefer:

```html
<a href="courses.html">
    View Python Courses
</a>
```

The link text should communicate the destination or purpose.

---

# 97. Image Accessibility

Weak:

```html
<img
    src="student.jpg"
    alt="image">
```

Better:

```html
<img
    src="student.jpg"
    alt="Student attending a programming class">
```

If the image is decorative:

```html
<img
    src="decoration.png"
    alt="">
```

---

# 98. Form Accessibility

Good:

```html
<label for="email">
    Email Address
</label>

<input
    type="email"
    id="email"
    name="email">
```

Poor:

```html
<input
    type="email"
    placeholder="Email">
```

A placeholder is not a replacement for a proper label.

---

# 99. HTML5

HTML5 is the modern generation of HTML that introduced many useful capabilities and semantic elements.

Important examples:

```text
header
nav
main
section
article
aside
footer
figure
figcaption
audio
video
track
canvas
form improvements
new input types
```

---

# 100. HTML5 Semantic Elements

Before semantic HTML:

```html
<div id="header">
```

```html
<div id="navigation">
```

```html
<div id="content">
```

```html
<div id="footer">
```

HTML5 provides meaningful elements:

```html
<header>
```

```html
<nav>
```

```html
<main>
```

```html
<footer>
```

---

# 101. HTML5 Form Improvements

HTML5 introduced or standardized useful input types such as:

```text
email
url
number
range
date
time
datetime-local
month
week
search
tel
color
```

It also provides built-in validation features such as:

```text
required
min
max
minlength
maxlength
pattern
```

---

# 102. HTML5 Multimedia

Before native HTML multimedia, websites often depended heavily on plugins.

HTML5 provides:

```html
<audio>
```

and:

```html
<video>
```

This allows browsers to provide native multimedia support.

---

# 103. HTML5 Doctype

Modern HTML uses:

```html
<!DOCTYPE html>
```

It is intentionally simple.

It tells the browser to use standards mode for the document.

---

# 104. Complete HTML5 Form Page

```html
<!DOCTYPE html>

<html lang="en">

    <head>

        <meta charset="UTF-8">

        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0">

        <title>Course Registration</title>

    </head>

    <body>

        <header>

            <h1>Course Registration</h1>

        </header>

        <nav>

            <a href="index.html">
                Home
            </a>

            <a href="courses.html">
                Courses
            </a>

        </nav>

        <main>

            <section>

                <h2>Register for a Course</h2>

                <form
                    action="/register"
                    method="post">

                    <fieldset>

                        <legend>
                            Personal Information
                        </legend>

                        <p>

                            <label for="name">
                                Full Name
                            </label>

                            <input
                                type="text"
                                id="name"
                                name="name"
                                placeholder="Enter your full name"
                                required>

                        </p>

                        <p>

                            <label for="email">
                                Email
                            </label>

                            <input
                                type="email"
                                id="email"
                                name="email"
                                placeholder="Enter your email"
                                required>

                        </p>

                        <p>

                            <label for="phone">
                                Phone
                            </label>

                            <input
                                type="tel"
                                id="phone"
                                name="phone">

                        </p>

                        <p>

                            <label for="dob">
                                Date of Birth
                            </label>

                            <input
                                type="date"
                                id="dob"
                                name="dob">

                        </p>

                    </fieldset>

                    <fieldset>

                        <legend>
                            Course Information
                        </legend>

                        <p>

                            <label for="course">
                                Course
                            </label>

                            <select
                                id="course"
                                name="course"
                                required>

                                <option
                                    value=""
                                    disabled
                                    selected>
                                    Select Course
                                </option>

                                <option value="python">
                                    Python
                                </option>

                                <option value="html">
                                    HTML
                                </option>

                                <option value="javascript">
                                    JavaScript
                                </option>

                                <option value="fullstack">
                                    Full Stack
                                </option>

                            </select>

                        </p>

                        <p>

                            <span>
                                Learning Mode
                            </span>

                        </p>

                        <input
                            type="radio"
                            id="online"
                            name="mode"
                            value="online">

                        <label for="online">
                            Online
                        </label>

                        <input
                            type="radio"
                            id="offline"
                            name="mode"
                            value="offline">

                        <label for="offline">
                            Offline
                        </label>

                    </fieldset>

                    <fieldset>

                        <legend>
                            Skills
                        </legend>

                        <input
                            type="checkbox"
                            id="python"
                            name="skills"
                            value="python">

                        <label for="python">
                            Python
                        </label>

                        <input
                            type="checkbox"
                            id="html"
                            name="skills"
                            value="html">

                        <label for="html">
                            HTML
                        </label>

                        <input
                            type="checkbox"
                            id="css"
                            name="skills"
                            value="css">

                        <label for="css">
                            CSS
                        </label>

                    </fieldset>

                    <fieldset>

                        <legend>
                            Additional Information
                        </legend>

                        <p>

                            <label for="experience">
                                Years of Experience
                            </label>

                            <input
                                type="number"
                                id="experience"
                                name="experience"
                                min="0"
                                max="50">

                        </p>

                        <p>

                            <label for="website">
                                Website
                            </label>

                            <input
                                type="url"
                                id="website"
                                name="website">

                        </p>

                        <p>

                            <label for="message">
                                Message
                            </label>

                            <textarea
                                id="message"
                                name="message"
                                rows="5"
                                cols="40">
                            </textarea>

                        </p>

                    </fieldset>

                    <button type="submit">
                        Register
                    </button>

                    <button type="reset">
                        Reset
                    </button>

                </form>

            </section>

        </main>

        <footer>

            <p>
                Course Registration
            </p>

        </footer>

    </body>

</html>
```

---

# 105. Day 3 — One-Hour Schedule

| Time | Topic |
|---|---|
| 0–10 min | Form, label, input, name, value |
| 10–20 min | Input types |
| 20–30 min | Radio, checkbox, select, textarea |
| 30–40 min | Validation, GET, POST, action, method |
| 40–50 min | Audio, video, iframe, HTML5 |
| 50–60 min | Accessibility + mini project |

---

# 106. Day 3 — Important Form Tags

```text
form
label
input
button
select
option
optgroup
textarea
datalist
fieldset
legend
```

---

# 107. Day 3 — Important Input Types

```text
text
password
email
number
date
time
datetime-local
month
week
url
tel
search
radio
checkbox
file
hidden
color
range
submit
reset
```

---

# 108. Day 3 — Important Form Attributes

```text
action
method
name
value
id
for
placeholder
required
disabled
readonly
checked
selected
multiple
min
max
step
minlength
maxlength
pattern
accept
list
```

---

# 109. Day 3 — Multimedia Tags

```text
audio
video
source
track
iframe
```

---

# 110. Day 3 — Semantic and Supporting Tags

```text
fieldset
legend
datalist
address
figure
figcaption
```

---

# 111. Day 3 — Global Attributes

```text
id
class
title
lang
dir
hidden
tabindex
data-*
contenteditable
spellcheck
```

---

# 112. Day 3 — Accessibility Checklist

Use:

```text
Meaningful HTML
```

Use:

```text
<label>
```

for form controls.

Use:

```text
alt
```

for meaningful images.

Use:

```text
<h1> → <h2> → <h3>
```

to represent hierarchy.

Use descriptive:

```text
link text
```

Provide:

```text
captions
```

for relevant video content.

Use:

```text
semantic elements
```

instead of unnecessary generic containers.

Ensure important functionality is usable with the keyboard.

---

# 113. Day 3 — Common Mistakes

## Mistake 1 — No Label

Avoid:

```html
<input type="text">
```

Prefer:

```html
<label for="name">
    Name
</label>

<input
    type="text"
    id="name"
    name="name">
```

---

## Mistake 2 — Placeholder Used as Label

Avoid:

```html
<input
    type="text"
    placeholder="Name">
```

Prefer:

```html
<label for="name">
    Name
</label>

<input
    type="text"
    id="name"
    placeholder="Enter your name">
```

---

## Mistake 3 — Radio Buttons with Different Names

Wrong:

```html
<input
    type="radio"
    name="online">

<input
    type="radio"
    name="offline">
```

If they represent one choice, use the same name:

```html
<input
    type="radio"
    name="mode"
    value="online">

<input
    type="radio"
    name="mode"
    value="offline">
```

---

## Mistake 4 — Missing `name`

Example:

```html
<input
    type="text"
    id="name">
```

For form submission, normally include:

```html
name="name"
```

Example:

```html
<input
    type="text"
    id="name"
    name="name">
```

---

## Mistake 5 — Assuming HTML Validation Is Security

Wrong idea:

```text
required
=
secure
```

Correct:

```text
HTML validation
+
Server-side validation
+
Authentication/authorization
+
Secure transport
+
Proper server handling
```

---

## Mistake 6 — Sensitive Data in Hidden Fields

Do not assume:

```html
<input
    type="hidden"
    value="secret">
```

is secret.

HTML is sent to the browser and can be inspected.

---

# 114. Day 3 — Interview Questions

## Q1. What is `<form>`?

It groups controls used to collect and submit user input.

## Q2. What is `<label>`?

It provides a label for a form control.

## Q3. What is the purpose of `for`?

It associates a label with the form control whose `id` matches it.

## Q4. What is `name`?

It identifies a form control's submitted field name.

## Q5. What is `value`?

It specifies the value associated with a control.

## Q6. What is `placeholder`?

It provides a hint about expected input.

## Q7. What does `required` do?

It requires a value before normal form submission can proceed.

## Q8. What is the difference between radio and checkbox?

Radio buttons are generally used for one choice from a group; checkboxes support independent selections.

## Q9. What is `<select>`?

It provides a selection control.

## Q10. What is `<option>`?

It represents an option within a select or datalist-related context.

## Q11. What is `<textarea>`?

It provides a multi-line text input.

## Q12. What is `<fieldset>`?

It groups related form controls.

## Q13. What is `<legend>`?

It provides a caption for a fieldset.

## Q14. What is `action`?

It specifies where form submission is sent.

## Q15. What is `method`?

It specifies the HTTP method used for form submission.

## Q16. What are common form methods?

GET and POST.

## Q17. What is `pattern`?

It provides a regular expression constraint for applicable form controls.

## Q18. What is `<audio>`?

It embeds audio content.

## Q19. What is `<video>`?

It embeds video content.

## Q20. What is `<source>`?

It provides a media resource for elements such as audio and video.

## Q21. What is `<track>`?

It provides timed text such as captions.

## Q22. What is `<iframe>`?

It embeds another browsing context.

## Q23. What is a global attribute?

An attribute that is generally available across many HTML elements.

## Q24. Why is semantic HTML important?

It communicates structure and meaning and supports accessibility and maintainability.

## Q25. Why is server-side validation necessary?

Client-side validation can be bypassed, so the server must validate untrusted input.

---

# 115. Day 3 — Practical Project

Create:

```text
course-registration/
│
├── index.html
├── courses.html
├── register.html
├── contact.html
│
├── images/
│   └── course.jpg
│
└── videos/
    └── introduction.mp4
```

---

# 116. `register.html` Requirements

Create a complete registration form containing:

```text
Full Name
Email
Phone
Password
Date of Birth
Course
Learning Mode
Skills
Experience
Resume
Message
Submit
Reset
```

Use:

```text
form
fieldset
legend
label
input
select
option
textarea
button
```

---

# 117. Registration Form Input Requirements

Use:

```text
Full Name
→ text

Email
→ email

Phone
→ tel

Password
→ password

Date of Birth
→ date

Course
→ select

Learning Mode
→ radio

Skills
→ checkbox

Experience
→ number

Resume
→ file

Message
→ textarea
```

---

# 118. Validation Requirements

At minimum:

```text
Name
→ required

Email
→ required

Password
→ required

Course
→ required
```

Add:

```text
minlength
maxlength
min
max
```

where appropriate.

---

# 119. Day 3 — Final Mini Project Structure

```text
course-registration/
│
├── index.html
│
│   ├── header
│   ├── nav
│   ├── main
│   └── footer
│
├── courses.html
│
│   ├── heading
│   ├── list
│   └── table
│
├── register.html
│
│   ├── form
│   ├── fieldset
│   ├── legend
│   ├── label
│   ├── input
│   ├── select
│   ├── textarea
│   └── button
│
└── contact.html
```

---

# 120. Day 3 — Coding Challenge

Create a **Job Application Form**.

The form must contain:

```text
Full Name
Email
Phone
Date of Birth
Portfolio URL
Years of Experience
Position
Work Mode
Skills
Resume
Cover Letter
Availability
Submit
Reset
```

Use as many appropriate HTML input types as possible.

---

# 121. Job Application Requirements

## Full Name

```html
<input
    type="text"
    name="full_name"
    required>
```

## Email

```html
<input
    type="email"
    name="email"
    required>
```

## Phone

```html
<input
    type="tel"
    name="phone">
```

## Portfolio

```html
<input
    type="url"
    name="portfolio">
```

## Experience

```html
<input
    type="number"
    name="experience"
    min="0"
    max="50">
```

## Resume

```html
<input
    type="file"
    name="resume"
    accept=".pdf">
```

---

# 122. Day 3 — HTML Form Architecture

Think:

```text
FORM
│
├── ACTION
│
├── METHOD
│
├── FIELDSET
│   │
│   ├── LEGEND
│   │
│   ├── LABEL
│   ├── INPUT
│   │
│   ├── LABEL
│   ├── INPUT
│   │
│   └── SELECT
│
├── FIELDSET
│   │
│   ├── RADIO
│   ├── CHECKBOX
│   └── TEXTAREA
│
└── BUTTON
```

---

# 123. HTML → Flask Connection

Today:

```text
HTML Form
    ↓
action="/register"
    ↓
method="post"
```

Later:

```text
HTML
    ↓
Browser
    ↓
HTTP Request
    ↓
Flask
    ↓
Python
    ↓
Database
```

This is why understanding HTML forms is essential before learning Flask.

---

# 124. HTML → CSS Connection

Today:

```html
<form>
    ...
</form>
```

Later CSS will control:

```text
Layout
Spacing
Typography
Borders
Sizing
Alignment
Responsive Design
```

HTML provides:

```text
Structure + Meaning
```

CSS provides:

```text
Presentation + Layout
```

---

# 125. HTML → JavaScript Connection

Today:

```html
<input
    id="email"
    name="email">
```

Later JavaScript can:

```text
Read the input
Validate data
React to events
Change content
Submit data
Manipulate DOM
```

HTML provides the elements.

JavaScript provides behavior.

---

# 126. HTML → Flask Connection

Eventually:

```text
HTML Form
      ↓
POST /register
      ↓
Flask Route
      ↓
Python Function
      ↓
Validate Data
      ↓
Database
      ↓
Response
      ↓
HTML Page
```

This is the foundation of a full-stack web application.

---

# 127. Day 3 — Skills Matrix

| Skill | Covered |
|---|---|
| Form | ✅ |
| Label | ✅ |
| Input | ✅ |
| Text Input | ✅ |
| Password | ✅ |
| Email | ✅ |
| Number | ✅ |
| Date | ✅ |
| Time | ✅ |
| Datetime Local | ✅ |
| Month | ✅ |
| Week | ✅ |
| URL | ✅ |
| Telephone | ✅ |
| Search | ✅ |
| Radio | ✅ |
| Checkbox | ✅ |
| File | ✅ |
| Hidden | ✅ |
| Color | ✅ |
| Range | ✅ |
| Submit | ✅ |
| Reset | ✅ |
| Button | ✅ |
| Select | ✅ |
| Option | ✅ |
| Optgroup | ✅ |
| Textarea | ✅ |
| Datalist | ✅ |
| Fieldset | ✅ |
| Legend | ✅ |
| GET | ✅ |
| POST | ✅ |
| Action | ✅ |
| Required | ✅ |
| Min | ✅ |
| Max | ✅ |
| Step | ✅ |
| Minlength | ✅ |
| Maxlength | ✅ |
| Pattern | ✅ |
| Audio | ✅ |
| Video | ✅ |
| Source | ✅ |
| Track | ✅ |
| iframe | ✅ |
| Global Attributes | ✅ |
| Accessibility | ✅ |
| HTML5 | ✅ |

---

# 128. Day 3 — Final Checklist

Before moving to Day 4, you should be able to:

- [ ] Create a form
- [ ] Create labels
- [ ] Associate labels with inputs
- [ ] Understand `id`
- [ ] Understand `name`
- [ ] Understand `value`
- [ ] Use text input
- [ ] Use password input
- [ ] Use email input
- [ ] Use number input
- [ ] Use date input
- [ ] Use time input
- [ ] Use URL input
- [ ] Use telephone input
- [ ] Use search input
- [ ] Use radio buttons
- [ ] Use checkboxes
- [ ] Use file upload
- [ ] Use hidden input
- [ ] Use range input
- [ ] Use color input
- [ ] Use submit button
- [ ] Use reset button
- [ ] Use `select`
- [ ] Use `option`
- [ ] Use `optgroup`
- [ ] Use `textarea`
- [ ] Use `datalist`
- [ ] Use `fieldset`
- [ ] Use `legend`
- [ ] Understand GET
- [ ] Understand POST
- [ ] Understand `action`
- [ ] Use `required`
- [ ] Use `min`
- [ ] Use `max`
- [ ] Use `step`
- [ ] Use `minlength`
- [ ] Use `maxlength`
- [ ] Understand `pattern`
- [ ] Embed audio
- [ ] Embed video
- [ ] Understand `source`
- [ ] Understand `track`
- [ ] Understand iframe
- [ ] Understand global attributes
- [ ] Understand basic accessibility
- [ ] Build a complete HTML form
- [ ] Understand how HTML forms connect to Flask

---

# 129. Day 3 — Final Mental Model

```text
HTML
│
├── DOCUMENT
│
├── CONTENT
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
│   └── Validation
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

# 130. Day 3 — HTML Completion Status

After Day 3:

```text
HTML FOUNDATION       ✅
HTML CONTENT          ✅
HTML LINKS            ✅
HTML IMAGES           ✅
HTML LISTS            ✅
HTML TABLES           ✅
HTML PATHS            ✅
HTML SEMANTIC         ✅
HTML FORMS            ✅
HTML INPUTS           ✅
HTML VALIDATION       ✅
HTML MULTIMEDIA       ✅
HTML IFRAMES          ✅
HTML5 FEATURES        ✅
HTML GLOBAL ATTRS     ✅
HTML ACCESSIBILITY    ✅
```

The remaining HTML work should now focus on:

```text
Advanced HTML details
Accessibility refinement
Practical page construction
Final HTML project
Revision
```

Then move to:

```text
CSS
```

---

# 131. Day 3 — Final Architecture

```text
FRONT END
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
│   └── Accessibility
│
├── CSS
│   ↓
│   Presentation
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

# DAY 3 — END

**Day 38 — HTML Forms, Inputs, Validation, Multimedia, iframe, Global Attributes, HTML5 and Accessibility Completed**

**Next: Day 39 — Final HTML Revision + Advanced HTML + Complete HTML Mini Project**

