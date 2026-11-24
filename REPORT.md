# Personal Portfolio Website: Analytical Report
**Name:** Nishat Jamal Ashik  |  **Technologies:** HTML5, CSS3, JavaScript

## Part A: Planning and Website Structure

**What the website is.** A four-page personal portfolio that presents my education, skills, projects and contact details. It targets recruiters and hiring managers, and also teachers and teammates who want a quick view of my work.

**Why this design.** Recruiters scan quickly, so I used a clean light layout, one accent colour (teal), and short sections. The teal line that draws itself across the Home page and ends in a glowing amber dot refers to my electronics work (a circuit trace ending in an LED, like my clap switch project). It is the only animation, and it is switched off for visitors who prefer reduced motion.

**Sitemap**
```
Home (index.html) ──► About (about.html)
  │                     │
  ├──► Projects (projects.html)
  └──► Contact (contact.html)
Every page links to every other page through the shared navigation bar.
Home also links to GitHub (external).
```

**Home page wireframe**
```
+--------------------------------------------------+
| Nishat.            Home About Projects Contact   |
+--------------------------------------------------+
| Hi, I am                         +-------------+ |
| NISHAT JAMAL ASHIK               |             | |
| short introduction               |  portrait   | |
| [See my projects] [Contact me]   |             | |
|                                  +-------------+ |
| ~~~~~~~~ animated trace line ~~~~~~~~~~~~~~~~ o  |
| What I work with  (3 bullet points + links)      |
+--------------------------------------------------+
| (c) 2026 Nishat Jamal Ashik        Back to top   |
+--------------------------------------------------+
```

**Purpose of each page**
- **Home:** first impression. Says who I am, what I do, and sends visitors to projects or contact.
- **About:** my background, strengths, a skills table, education list, awards and languages.
- **Projects:** four projects with descriptions and technology tags, plus a summary table.
- **Contact:** email, phone, location and a message form.

## Part B: Implementation

**Files:** `index.html`, `about.html`, `projects.html`, `contact.html`, `css/style.css`, `js/main.js`, `images/portrait.jpg`.

**Requirements covered**
- Four linked pages with one common navigation menu; the current page is marked with `aria-current="page"`.
- Correct structure on every page: `<!DOCTYPE html>`, `html`, `head` (with `title`), `body`.
- Headings (`h1` to `h3`), paragraphs, unordered lists (strengths, awards), an ordered list (education), an image (portrait), internal links (navigation) and an external link (GitHub, opened with `target="_blank" rel="noopener"`).
- Tables: skills table (About) and project summary table (Projects).

**Code snippet 1: the animated line (HTML + CSS)**
```html
<svg class="trace" viewBox="0 0 600 80" aria-hidden="true">
  <path pathLength="1" d="M0 60 H170 L210 20 H430 L470 60 H585"/>
  <circle cx="592" cy="60" r="7"/>
</svg>
```
```css
.trace path{stroke-dasharray:1;stroke-dashoffset:1;animation:draw 2.2s ease-out .3s forwards}
@keyframes draw{to{stroke-dashoffset:0}}
```
*What it does:* `pathLength="1"` makes the line length equal to 1, so a dash of 1 hides the whole line. Animating `stroke-dashoffset` to 0 reveals it like a drawing. The circle fades in at the end. *Why:* it needs no library and no image, stays sharp at any size, and `aria-hidden` keeps it out of screen readers because it is decoration.

**Code snippet 2: shared navigation with the current page marked**
```html
<nav aria-label="Main"><ul>
  <li><a href="index.html" aria-current="page">Home</a></li>
  <li><a href="about.html">About</a></li>
  ...
</ul></nav>
```
```css
nav a:hover, nav a[aria-current]{border-color:var(--trace)}
```
*What it does:* the same list of links is on every page; the CSS underlines the link that has `aria-current`. *Why:* one CSS rule serves both the visual highlight and screen-reader information, and a list inside `nav` is the standard structure for menus.

**Code snippet 3: form validation (JavaScript)**
```js
email: function (v) { return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v) ? "" : "Enter a valid email address."; }
...
form.addEventListener("submit", function (e) { e.preventDefault(); ... });
```
*What it does:* on submit, each field is checked against a rule; a short error is written under the field that failed, and a confirmation shows if all pass. `preventDefault()` stops the page reloading. *Why:* instant, specific feedback is easier than a generic browser popup, and the rules live in one object so adding a field is one line.

**Screenshots (take these yourself).** Open each page in the browser, press `Win + Shift + S` (or `Cmd + Shift + 4` on Mac), and paste them here:
- Figure 1: Home  
- Figure 2: About  
- Figure 3: Projects  
- Figure 4: Contact (also one with the validation errors showing)

## Part C: Form, Testing and Justification

**Contact form.** Located in `contact.html`: text input (name), email input, radio buttons (topic), dropdown `select` (preferred reply), `textarea` (message) and a submit button. Every input has a `<label>`; the radio group is wrapped in `fieldset` and `legend`.

**Browser testing (fill in after you test).**

| Check | Chrome (version ___) | Firefox (version ___) |
|---|---|---|
| Line animation plays | | |
| Navigation links work | | |
| Tables fit on a phone-width window | | |
| Form shows errors for empty fields | | |
| Fonts load | | |

Write two or three sentences on the differences you saw (for example, spacing of form controls or font rendering).

**Problem 1: the animated line did not draw smoothly when the SVG stretched.** The SVG scales to the page width, which also stretched the stroke thickness. *Solution:* added `vector-effect: non-scaling-stroke` so the line keeps a constant 3px width at any size.

**Problem 2: the menu and the layout broke on narrow screens.** The two-column layouts squeezed the text on phones. *Solution:* added a `@media (max-width:720px)` rule that switches the grids to one column and reduces the menu gap.

**Design justification.**
- `header`, `nav`, `main`, `section`, `article`, `footer` instead of many `div`s: the meaning of each block is clear to search engines and screen readers.
- Tables for skills and project summary because the data has rows and columns; `th` with `scope` tells assistive tools how to read it. Tables were not used for layout; CSS grid is used instead.
- An ordered list (reversed) for education because it is a sequence, and unordered lists for items with no order.
- Separate pages instead of one long scroll: each page has one job, loads fast, and can be linked or printed on its own.
- One shared CSS file and one JS file so the look is consistent and changes are made once.

**Future improvements**
- Add real project screenshots and a link to each GitHub repository.
- Connect the form to a backend or a service so messages are delivered, and add server-side validation.
- Add a dark mode, a downloadable CV (PDF), and a Bangla language option.
- Run Lighthouse for accessibility and speed, and compress images.
