# Day 39 — HTML Final Revision (Compact)

**Focus:** HTML only. No CSS. Structure + Content + Semantics + Accessibility.

---

## 1. Document Skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
</head>
<body>

</body>
</html>
```

## 2. Semantic Structure

```text
header → nav → main( section / article / aside ) → footer
```

- `header` — intro content
- `nav` — navigation links
- `main` — one per page, primary content
- `section` — thematic grouping
- `article` — self-contained content
- `aside` — related/complementary content
- `footer` — closing content
- `div`/`span` — generic containers only, no meaning

## 3. Content Elements

| Element | Purpose |
|---|---|
| `h1`–`h6` | Heading hierarchy (structure, not size) |
| `p` | Paragraph |
| `strong` / `em` | Importance / emphasis |
| `a href` | Link (`target="_blank"` → add `rel="noopener noreferrer"`) |
| `img alt` | Image with alt text (`alt=""` if decorative) |
| `figure` + `figcaption` | Self-contained illustration with caption |
| `ul` / `ol` / `dl` | Unordered / ordered / description lists |
| `table` (`caption`, `thead`, `tbody`, `th scope`) | Tabular data |

## 4. Forms Cheat Sheet

```html
<label for="x">Label</label>
<input type="text" id="x" name="x" required minlength="3" maxlength="20">
```

- Match `label for` ↔ `input id`
- Key input types: text, email, password, number, date, time, tel, url, file, checkbox, radio, range, color
- Validation attrs: `required`, `minlength`, `maxlength`, `min`, `max`, `pattern`
- `select` + `option`, `textarea`, `button` (submit/reset/button)
- `fieldset` + `legend` to group related controls
- Radios share the same `name`; checkboxes are independent

## 5. Multimedia & Embeds

```html
<audio controls><source src="a.mp3" type="audio/mpeg"></audio>
<video controls><source src="v.mp4" type="video/mp4">
  <track src="captions.vtt" kind="captions" srclang="en" label="English">
</video>
<iframe src="https://example.com" title="Example"></iframe>
```

## 6. HTML5 Extras

- `details` + `summary` — built-in collapsible section
- `dialog` — native dialog box (behavior needs JS later)
- `data-*` — custom data attributes for later JS use

## 7. Global Attributes

`id`, `class`, `title`, `lang`, `dir`, `hidden`, `data-*`, `tabindex`, `contenteditable`, `draggable`, `spellcheck`

- `id` → unique per page
- `class` → reusable, shared across elements
- Avoid unnecessary positive `tabindex`

## 8. Accessibility Rules

1. Prefer semantic elements over generic `div`/`span`
2. Every form control needs a `label`
3. Every meaningful `img` needs descriptive `alt`
4. Headings must follow logical nesting (no skipping for size)
5. Use native interactive elements (`button`, `a`, `input`) — they're keyboard accessible by default
6. Add captions (`track`) to videos with speech

## 9. Best Practices

- Semantic tags > generic divs
- Meaningful `id`/`class` names
- Lowercase tags, quoted attribute values
- Consistent indentation, properly closed tags

## 10. HTML vs CSS vs JS

```text
HTML = Skeleton (structure, content, meaning)
CSS  = Appearance (colors, layout, responsive design)
JS   = Behavior (events, DOM, interactivity)
```

Today: structure and content only — no colors, fonts, spacing, or layout.

## 11. Validation Checklist

```text
[ ] doctype, html lang, head (charset, viewport, title), body
[ ] Logical heading order
[ ] Semantic layout (header/nav/main/section/article/aside/footer)
[ ] Alt text on meaningful images
[ ] Labels on every form control + validation attributes
[ ] Table caption + th scope
[ ] Video captions where speech is present
[ ] No unnecessary divs; proper nesting and closing tags
```

## 12. Self-Test (answer without notes)

1. Purpose of HTML?
2. `div` vs `section` — difference?
3. Why does `alt` matter?
4. Why must form controls have labels?
5. `id` vs `class`?
6. Purpose of `header`, `nav`, `main`, `footer`?
7. Purpose of `fieldset` + `legend`?
8. `GET` vs `POST` — high level?
9. What does `required` do?
10. Why separate HTML structure from CSS presentation?

---

**Next module:** CSS — selectors, box model, flexbox, grid, responsive design.


---

## Mini Project 1 — Student Portfolio

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Personal learning portfolio">
    <title>My Learning Portfolio</title>
</head>
<body>

    <header id="home">
        <h1>Alex Kumar — Learning Portfolio</h1>
        <p>Aspiring Web Developer &amp; Programmer</p>
    </header>

    <nav aria-label="Main Navigation">
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#education">Education</a>
        <a href="#projects">Projects</a>
        <a href="#faq">FAQ</a>
        <a href="#contact">Contact</a>
    </nav>

    <main>

        <section id="about">
            <h2>About Me</h2>
            <figure>
                <img src="profile.jpg" alt="Portrait photo of Alex Kumar" width="200" height="200">
                <figcaption>Alex Kumar — Web Development Student</figcaption>
            </figure>
            <p>
                I am learning front-end and back-end web development,
                starting with HTML as the foundation of every webpage.
            </p>
        </section>

        <section id="skills">
            <h2>Skills</h2>
            <ul>
                <li>HTML</li>
                <li>Problem Solving</li>
                <li>Python (in progress)</li>
            </ul>
            <ol>
                <li>Learn fundamentals</li>
                <li>Practice daily</li>
                <li>Build projects</li>
            </ol>
        </section>

        <section id="education">
            <h2>Education</h2>
            <table>
                <caption>Academic Background</caption>
                <thead>
                    <tr>
                        <th scope="col">Qualification</th>
                        <th scope="col">Institution</th>
                        <th scope="col">Year</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>B.Sc Computer Science</td>
                        <td>ABC College</td>
                        <td>2023 – 2026</td>
                    </tr>
                    <tr>
                        <td>Higher Secondary</td>
                        <td>XYZ Junior College</td>
                        <td>2021 – 2023</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <article id="projects">
            <h2>Projects</h2>
            <p>
                A selection of small projects completed while learning
                HTML, Python, and general programming concepts.
            </p>
            <ul>
                <li>Student Training Portal (HTML)</li>
                <li>BMI &amp; EMI Calculator (Python)</li>
                <li>Personal Portfolio (this page)</li>
            </ul>
        </article>

        <section id="faq">
            <h2>FAQ</h2>
            <details>
                <summary>What am I currently learning?</summary>
                <p>I am currently completing the HTML foundation before moving to CSS.</p>
            </details>
            <details>
                <summary>What will I learn next?</summary>
                <p>CSS for styling and layout, followed by JavaScript and Flask.</p>
            </details>
        </section>

        <aside>
            <h2>Currently Exploring</h2>
            <ul>
                <li>CSS Basics</li>
                <li>Git &amp; GitHub</li>
                <li>Databases</li>
            </ul>
        </aside>

        <section id="contact-form">
            <h2>Contact Me</h2>
            <form action="/contact" method="post">

                <fieldset>
                    <legend>Your Details</legend>

                    <p>
                        <label for="name">Full Name</label><br>
                        <input type="text" id="name" name="name" placeholder="Enter your name" required minlength="3">
                    </p>

                    <p>
                        <label for="email">Email Address</label><br>
                        <input type="email" id="email" name="email" placeholder="Enter your email" required>
                    </p>

                    <p>
                        <label for="reason">Reason for Contact</label><br>
                        <select id="reason" name="reason" required>
                            <option value="">Select a reason</option>
                            <option value="collaboration">Collaboration</option>
                            <option value="feedback">Feedback</option>
                            <option value="job">Job Opportunity</option>
                        </select>
                    </p>

                    <p>
                        <label for="message">Message</label><br>
                        <textarea id="message" name="message" rows="5" cols="40" placeholder="Write your message"></textarea>
                    </p>
                </fieldset>

                <button type="submit">Send Message</button>
                <button type="reset">Reset</button>

            </form>
        </section>

    </main>

    <footer id="contact">
        <p>Email: <a href="mailto:alex@example.com">alex@example.com</a></p>
        <p>&copy; 2026 Alex Kumar — Learning Portfolio</p>
    </footer>

</body>
</html>

```

## Mini Project 2 — Student & Course Information

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Student and course information portal">
    <title>Student &amp; Course Information Portal</title>
</head>
<body>

    <header id="home">
        <h1>Student &amp; Course Information Portal</h1>
        <p>Track student records, courses, and schedules.</p>
    </header>

    <nav aria-label="Main Navigation">
        <a href="#students">Students</a>
        <a href="#courses">Courses</a>
        <a href="#schedule">Schedule</a>
        <a href="#notice">Notice</a>
        <a href="#enroll">Enroll</a>
        <a href="#contact">Contact</a>
    </nav>

    <main>

        <section id="students">
            <h2>Student Directory</h2>
            <table>
                <caption>Registered Students</caption>
                <thead>
                    <tr>
                        <th scope="col">Name</th>
                        <th scope="col">Roll No.</th>
                        <th scope="col">Course</th>
                        <th scope="col">Score</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Alex</td>
                        <td>101</td>
                        <td>Python</td>
                        <td>90</td>
                    </tr>
                    <tr>
                        <td>John</td>
                        <td>102</td>
                        <td>HTML</td>
                        <td>85</td>
                    </tr>
                    <tr>
                        <td>Priya</td>
                        <td>103</td>
                        <td>JavaScript</td>
                        <td>88</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <section id="courses">
            <h2>Available Courses</h2>
            <ul>
                <li>HTML</li>
                <li>CSS</li>
                <li>JavaScript</li>
                <li>Python</li>
                <li>Flask</li>
            </ul>

            <dl>
                <dt>HTML</dt>
                <dd>Structure of a webpage.</dd>
                <dt>Python</dt>
                <dd>General-purpose programming language.</dd>
            </dl>

            <figure>
                <img src="classroom.jpg" alt="Students attending a programming class" width="500" height="300">
                <figcaption>A typical classroom session at the portal.</figcaption>
            </figure>
        </section>

        <section id="schedule">
            <h2>Course Schedule</h2>
            <table>
                <caption>Weekly Training Schedule</caption>
                <thead>
                    <tr>
                        <th scope="col">Course</th>
                        <th scope="col">Duration</th>
                        <th scope="col">Level</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>HTML</td>
                        <td>4 Days</td>
                        <td>Beginner</td>
                    </tr>
                    <tr>
                        <td>Python</td>
                        <td>15 Days</td>
                        <td>Beginner → Intermediate</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <article id="notice">
            <h2>Latest Notice</h2>
            <p>
                The next batch for the Python course begins soon.
                Students are encouraged to complete the HTML foundation
                before enrolling in advanced courses.
            </p>
        </article>

        <section id="faq">
            <h2>FAQ</h2>
            <details>
                <summary>How do I check my score?</summary>
                <p>Scores are listed in the Student Directory table above.</p>
            </details>
            <details>
                <summary>Can I enroll in multiple courses?</summary>
                <p>Yes, students may enroll in more than one course at a time.</p>
            </details>
        </section>

        <aside>
            <h2>Related Links</h2>
            <ul>
                <li><a href="#courses">Course List</a></li>
                <li><a href="#schedule">Schedule</a></li>
            </ul>
        </aside>

        <section id="enroll">
            <h2>Student Enrollment Form</h2>
            <form action="/enroll" method="post">

                <fieldset>
                    <legend>Personal Information</legend>

                    <p>
                        <label for="name">Full Name</label><br>
                        <input type="text" id="name" name="name" required minlength="3" maxlength="50" placeholder="Enter full name">
                    </p>

                    <p>
                        <label for="email">Email Address</label><br>
                        <input type="email" id="email" name="email" required placeholder="Enter email">
                    </p>

                    <p>
                        <label for="age">Age</label><br>
                        <input type="number" id="age" name="age" min="10" max="60">
                    </p>
                </fieldset>

                <fieldset>
                    <legend>Course Selection</legend>

                    <p>
                        <label for="course">Select Course</label><br>
                        <select id="course" name="course" required>
                            <option value="">Select a course</option>
                            <option value="html">HTML</option>
                            <option value="python">Python</option>
                            <option value="javascript">JavaScript</option>
                        </select>
                    </p>

                    <p><strong>Preferred Mode</strong></p>
                    <label><input type="radio" name="mode" value="online" required> Online</label>
                    <label><input type="radio" name="mode" value="offline"> Offline</label>
                </fieldset>

                <fieldset>
                    <legend>Additional Notes</legend>
                    <p>
                        <label for="notes">Notes</label><br>
                        <textarea id="notes" name="notes" rows="4" cols="40" placeholder="Any additional information"></textarea>
                    </p>
                </fieldset>

                <p>
                    <label><input type="checkbox" name="terms" required> I agree to the terms and conditions.</label>
                </p>

                <button type="submit">Enroll</button>
                <button type="reset">Reset</button>
            </form>
        </section>

    </main>

    <footer id="contact">
        <p>Email: <a href="mailto:info@studentportal.example.com">info@studentportal.example.com</a></p>
        <p>&copy; 2026 Student &amp; Course Information Portal</p>
    </footer>

</body>
</html>

```

## Mini Project 3 — Gym & Nutrition Coaching

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Gym and nutrition coaching program">
    <title>PeakForm — Gym &amp; Nutrition Coaching</title>
</head>
<body>

    <header id="home">
        <h1>PeakForm Coaching</h1>
        <p>Strength Training, Fitness &amp; Nutrition Guidance</p>
    </header>

    <nav aria-label="Main Navigation">
        <a href="#about">About</a>
        <a href="#programs">Programs</a>
        <a href="#schedule">Schedule</a>
        <a href="#nutrition">Nutrition</a>
        <a href="#faq">FAQ</a>
        <a href="#join">Join</a>
        <a href="#contact">Contact</a>
    </nav>

    <main>

        <section id="about">
            <h2>About the Program</h2>
            <figure>
                <img src="gym.jpg" alt="Coach guiding a client through a strength training session" width="500" height="300">
                <figcaption>Personalized coaching sessions at PeakForm.</figcaption>
            </figure>
            <p>
                PeakForm Coaching offers structured strength training and
                nutrition guidance for beginners and intermediate fitness
                enthusiasts.
            </p>
        </section>

        <section id="programs">
            <h2>Coaching Programs</h2>
            <ul>
                <li>Strength Training</li>
                <li>Weight Loss Coaching</li>
                <li>Muscle Building</li>
                <li>Nutrition Planning</li>
            </ul>

            <ol>
                <li>Fitness assessment</li>
                <li>Goal setting</li>
                <li>Personalized plan</li>
                <li>Weekly check-ins</li>
            </ol>
        </section>

        <section id="schedule">
            <h2>Weekly Schedule</h2>
            <table>
                <caption>Sample Training Week</caption>
                <thead>
                    <tr>
                        <th scope="col">Day</th>
                        <th scope="col">Focus</th>
                        <th scope="col">Duration</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Monday</td>
                        <td>Upper Body Strength</td>
                        <td>60 min</td>
                    </tr>
                    <tr>
                        <td>Wednesday</td>
                        <td>Lower Body Strength</td>
                        <td>60 min</td>
                    </tr>
                    <tr>
                        <td>Friday</td>
                        <td>Full Body Conditioning</td>
                        <td>45 min</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <article id="nutrition">
            <h2>Why Nutrition Matters</h2>
            <p>
                Consistent training works best when paired with a structured
                eating routine. Coaching includes general guidance on meal
                timing, portion awareness, and building sustainable habits.
            </p>
            <dl>
                <dt>Assessment</dt>
                <dd>Understanding current habits and goals.</dd>
                <dt>Guidance</dt>
                <dd>Simple, sustainable nutrition recommendations.</dd>
            </dl>
        </article>

        <section id="media">
            <h2>Coaching Preview</h2>
            <video controls width="500">
                <source src="preview.mp4" type="video/mp4">
                <track src="captions.vtt" kind="captions" srclang="en" label="English">
                Your browser does not support video.
            </video>
        </section>

        <section id="faq">
            <h2>Frequently Asked Questions</h2>
            <details>
                <summary>Do I need prior gym experience?</summary>
                <p>No. Programs are designed for beginners as well as experienced trainees.</p>
            </details>
            <details>
                <summary>Is a diet plan included?</summary>
                <p>Yes, general nutrition guidance is included with every program.</p>
            </details>
            <details>
                <summary>How often are check-ins held?</summary>
                <p>Check-ins are typically held weekly to track progress.</p>
            </details>
        </section>

        <aside>
            <h2>Client Tips</h2>
            <ul>
                <li>Stay consistent with sessions</li>
                <li>Track your progress weekly</li>
                <li>Prioritize recovery and sleep</li>
            </ul>
        </aside>

        <section id="join">
            <h2>Join the Program</h2>
            <form action="/join" method="post">

                <fieldset>
                    <legend>Personal Information</legend>

                    <p>
                        <label for="name">Full Name</label><br>
                        <input type="text" id="name" name="name" required minlength="3" maxlength="50" placeholder="Enter your full name">
                    </p>

                    <p>
                        <label for="email">Email Address</label><br>
                        <input type="email" id="email" name="email" required placeholder="Enter your email">
                    </p>

                    <p>
                        <label for="phone">Phone Number</label><br>
                        <input type="tel" id="phone" name="phone" placeholder="Enter phone number">
                    </p>

                    <p>
                        <label for="age">Age</label><br>
                        <input type="number" id="age" name="age" min="16" max="70">
                    </p>
                </fieldset>

                <fieldset>
                    <legend>Program Preference</legend>

                    <p>
                        <label for="goal">Primary Goal</label><br>
                        <select id="goal" name="goal" required>
                            <option value="">Select a goal</option>
                            <option value="strength">Strength Training</option>
                            <option value="weightloss">Weight Loss</option>
                            <option value="muscle">Muscle Building</option>
                        </select>
                    </p>

                    <p><strong>Training Mode</strong></p>
                    <label><input type="radio" name="mode" value="in-person" required> In-Person</label>
                    <label><input type="radio" name="mode" value="online"> Online</label>
                </fieldset>

                <fieldset>
                    <legend>Current Activity</legend>
                    <label><input type="checkbox" name="activity" value="cardio"> Cardio</label>
                    <label><input type="checkbox" name="activity" value="weights"> Weight Training</label>
                    <label><input type="checkbox" name="activity" value="none"> None currently</label>
                </fieldset>

                <fieldset>
                    <legend>Additional Information</legend>
                    <p>
                        <label for="notes">Health notes or goals</label><br>
                        <textarea id="notes" name="notes" rows="5" cols="40" placeholder="Share any relevant details"></textarea>
                    </p>
                </fieldset>

                <p>
                    <label><input type="checkbox" name="terms" required> I agree to the terms and conditions.</label>
                </p>

                <button type="submit">Join Now</button>
                <button type="reset">Reset</button>
            </form>
        </section>

    </main>

    <footer id="contact">
        <p>Email: <a href="mailto:coach@peakform.example.com">coach@peakform.example.com</a></p>
        <p>&copy; 2026 PeakForm Coaching</p>
    </footer>

</body>
</html>

```
