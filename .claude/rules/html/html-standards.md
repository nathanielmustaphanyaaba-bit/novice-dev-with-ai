# HTML Coding Standards for Students

> These rules apply to ALL HTML written in this repository.
> AI agents enforce these rules during every code review.
> Students must follow them in every exercise and project submission.

---

## Rule 1 — Required Boilerplate (Every File, Every Time)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Descriptive Page Title Here</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>

    <!-- Your content here -->

  </body>
</html>
```

| Line | Purpose |
|---|---|
| `<!DOCTYPE html>` | Tells the browser: "This is HTML5" |
| `<html lang="en">` | Root container. `lang` helps screen readers and search engines |
| `<meta charset="UTF-8">` | Allows all characters: emoji, accents, international text |
| `<meta name="viewport" ...>` | Makes the page scale correctly on mobile devices |
| `<title>` | Text shown in the browser tab and in search results |
| `<link rel="stylesheet">` | Connects your external CSS file |

Every line is required. Submissions missing any of these fail the boilerplate check.

---

## Rule 2 — Semantic Elements Over Divs

| Content | Use This | Not This |
|---|---|---|
| Site-wide header / banner | `<header>` | `<div class="header">` |
| Navigation links | `<nav>` | `<div class="nav">` |
| Primary page content | `<main>` | `<div class="main">` |
| Thematic group of content | `<section>` | `<div class="section">` |
| Standalone content (post, card) | `<article>` | `<div class="article">` |
| Secondary / related content | `<aside>` | `<div class="sidebar">` |
| Page or section footer | `<footer>` | `<div class="footer">` |
| Important text | `<strong>` | `<b>` |
| Emphasized text | `<em>` | `<i>` |

Use `<div>` only when NO semantic element applies.

---

## Rule 3 — Heading Hierarchy

- **One `<h1>` per page** — it is the page's main title, not a font size
- Never skip heading levels (h1 → h2 → h3, never h1 → h3)
- Headings create a document outline, not visual styling

```html
<!-- CORRECT -->
<h1>My Portfolio</h1>
  <h2>Projects</h2>
    <h3>Project One</h3>
  <h2>About Me</h2>

<!-- WRONG — skipped h2 -->
<h1>My Portfolio</h1>
  <h3>Projects</h3>
```

---

## Rule 4 — Images Always Need Alt Text

```html
<!-- CORRECT — describes the image -->
<img src="images/team.jpg" alt="Three developers collaborating at a whiteboard">

<!-- CORRECT — decorative: empty alt so screen readers skip it -->
<img src="images/divider.png" alt="">

<!-- WRONG — no alt attribute -->
<img src="images/team.jpg">

<!-- WRONG — useless alt text -->
<img src="images/team.jpg" alt="image">
```

Alt text rule: describe what the image shows as if talking to someone who cannot see it.

---

## Rule 5 — Links Must Have Descriptive Text

```html
<!-- WRONG -->
<a href="/about">Click here</a>

<!-- CORRECT -->
<a href="/about">Learn about our team</a>

<!-- External links need target and rel -->
<a href="https://github.com" target="_blank" rel="noopener noreferrer">
  View on GitHub
</a>
```

---

## Rule 6 — Every Form Input Needs a Label

```html
<!-- CORRECT — label linked via for/id -->
<label for="email">Email address</label>
<input type="email" id="email" name="email" required>

<!-- WRONG — no label -->
<input type="email" placeholder="Enter email">

<!-- WRONG — label not linked -->
<label>Email</label>
<input type="email" name="email">
```

`placeholder` is NOT a replacement for `<label>`. Always use both.

---

## Rule 7 — Indentation: 2 Spaces Per Level

```html
<!-- CORRECT -->
<main>
  <section>
    <h2>Projects</h2>
    <article>
      <h3>Project One</h3>
      <p>Description here.</p>
    </article>
  </section>
</main>

<!-- WRONG -->
<main>
<section>
<h2>Projects</h2>
</section>
</main>
```

---

## Rule 8 — Section Comments

```html
<body>
  <!-- ===== Header ===== -->
  <header>...</header>

  <!-- ===== Navigation ===== -->
  <nav>...</nav>

  <!-- ===== Main Content ===== -->
  <main>
    <!-- Projects Section -->
    <section id="projects">...</section>
  </main>

  <!-- ===== Footer ===== -->
  <footer>...</footer>
</body>
```

---

## Rule 9 — Attribute Formatting

- All attribute values in **double quotes**
- All tags and attribute names in **lowercase**
- Boolean attributes written without a value: `required`, `disabled`, `checked`

```html
<!-- CORRECT -->
<img src="photo.jpg" alt="A developer typing" width="400" height="300">
<input type="text" id="name" name="name" required>

<!-- WRONG -->
<img src=photo.jpg alt=photo>
<IMG SRC="photo.jpg">
```

---

## Rule 10 — Forbidden Patterns

```
❌ <table> for page layout          tables are for DATA only
❌ <br> for spacing                 use CSS margin/padding
❌ <b> and <i> for meaning          use <strong> and <em>
❌ Inline styles: style=""          CSS goes in external files
❌ <center>, <font>, <marquee>      deprecated, never use
❌ Missing alt on meaningful images always required
❌ "click here" or "read more"      links must describe the destination
❌ Multiple <h1> elements           one per page only
❌ Skipping heading levels          h1 → h2 → h3, never skip
```

---

## Rule 11 — Recommended Meta Tags

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title — Site Name</title>
  <meta name="description" content="Brief description (150–160 chars)">
  <meta name="author" content="Your Name">
  <link rel="stylesheet" href="style.css">
</head>
```

---

## Rule 12 — Validate Before Every Submission

1. Go to **https://validator.w3.org/**
2. Choose "Validate by Direct Input"
3. Paste your entire HTML
4. Fix ALL errors before submitting
5. Zero errors required to pass any milestone
