# CSS Coding Standards for Students

> These rules apply to ALL CSS written in this repository.
> AI agents enforce these rules during every code review.
> Students must follow them in every exercise and project submission.

---

## Rule 1 — CSS Lives in External Files Only

```html
<!-- CORRECT — external file in <head> -->
<head>
  <link rel="stylesheet" href="style.css">
</head>

<!-- WRONG — <style> block in HTML -->
<head>
  <style>
    body { color: red; }
  </style>
</head>

<!-- WRONG — inline style attribute -->
<p style="color: red;">Text</p>
```

The only exception: inline styles used for quick demos during teaching.
All submitted code must use external CSS files.

---

## Rule 2 — Required Reset (Top of Every CSS File)

```css
/* === CSS Reset === */
*, *::before, *::after {
  box-sizing: border-box; /* padding and border included in width */
  margin: 0;              /* remove browser default margins */
  padding: 0;             /* remove browser default padding */
}

/* === Base Styles === */
body {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 1rem;          /* 16px equivalent */
  line-height: 1.6;         /* comfortable reading spacing */
  color: #1e293b;           /* dark slate — not pure black */
  background-color: #ffffff;
}
```

Every CSS file must start with this reset. No exceptions.

---

## Rule 3 — Selectors: Use Classes, Not IDs

```css
/* CORRECT — class selectors */
.card { background: white; }
.nav-link { color: #2563eb; }
.hero-title { font-size: 2.5rem; }

/* WRONG — ID selectors for styling */
#card { background: white; }
#nav-link { color: blue; }
```

**Why:** IDs must be unique per page. Classes are reusable.
IDs are reserved for JavaScript targeting and anchor links.

---

## Rule 4 — Class Naming: BEM-Lite (lowercase + hyphens)

```css
/* Block — the component */
.card { ... }
.navigation { ... }
.hero { ... }

/* Element — a part of the block */
.card__title { ... }
.card__image { ... }
.card__body { ... }
.navigation__link { ... }

/* Modifier — a variation */
.card--featured { ... }
.card--small { ... }
.button--primary { ... }
.button--outline { ... }
```

Rules:
- All lowercase
- Words separated by hyphens: `.nav-link`, not `.navLink` or `.NavLink`
- Descriptive: `.hero-button`, not `.btn1` or `.blue-thing`

---

## Rule 5 — Units Guide

| Use Case | Unit | Why |
|---|---|---|
| Font sizes | `rem` | Scales with user's browser font setting |
| Padding, margin | `rem` or `em` | Proportional spacing |
| Container widths | `%` or `max-width` in `px` | Fluid and responsive |
| Full-screen height | `100dvh` | Accounts for mobile browser bars |
| Borders, icons | `px` | Precise, pixel-level detail |
| **Never for font-size** | `px` | Breaks user accessibility settings |
| Grid fractions | `fr` | Proportional grid columns |

```css
/* CORRECT */
body { font-size: 1rem; }
h1 { font-size: 2.5rem; }
.card { padding: 1.5rem; max-width: 600px; }

/* WRONG */
body { font-size: 16px; }   /* breaks accessibility zoom */
.card { font-size: 14; }    /* missing unit */
```

---

## Rule 6 — CSS Custom Properties (Introduced in Module 3+)

```css
/* Define in :root for global access */
:root {
  /* Color palette */
  --color-primary:    #2563eb;
  --color-secondary:  #7c3aed;
  --color-accent:     #f59e0b;
  --color-text:       #1e293b;
  --color-text-muted: #64748b;
  --color-bg:         #ffffff;
  --color-bg-alt:     #f8fafc;

  /* Spacing scale */
  --space-xs:  0.25rem;
  --space-sm:  0.5rem;
  --space-md:  1rem;
  --space-lg:  1.5rem;
  --space-xl:  2rem;
  --space-2xl: 3rem;

  /* Typography */
  --font-body:    'Inter', system-ui, sans-serif;
  --font-heading: 'Inter', system-ui, sans-serif;
  --font-mono:    'Fira Code', monospace;
}

/* Use throughout your CSS */
.card {
  background-color: var(--color-bg-alt);
  padding: var(--space-lg);
  color: var(--color-text);
}
```

---

## Rule 7 — CSS File Structure and Order

Write your CSS in this order:

```css
/* 1. Reset (always first) */
/* 2. Custom properties / variables */
/* 3. Base element styles (body, h1-h6, p, a, img) */
/* 4. Layout utilities (.container, .grid, .flex) */
/* 5. Component styles (.card, .nav, .hero, .button) */
/* 6. State and modifier styles (.is-active, .card--featured) */
/* 7. Responsive media queries (at the bottom) */
```

Add a comment before each major section:
```css
/* ===== Components: Cards ===== */
.card { ... }
.card__title { ... }
.card__body { ... }

/* ===== Components: Navigation ===== */
.nav { ... }
```

---

## Rule 8 — Flexbox: Container First, Items Second

```css
/* Step 1: Container */
.card-row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: stretch;
  gap: var(--space-lg);
  flex-wrap: wrap;
}

/* Step 2: Items (only after container works) */
.card {
  flex: 1;
  min-width: 250px; /* prevents cards from getting too small */
}
```

---

## Rule 9 — Grid: Named Areas for Complex Layouts

```css
.page-layout {
  display: grid;
  grid-template-areas:
    "header"
    "main"
    "footer";
  gap: 0;
}

@media (min-width: 768px) {
  .page-layout {
    grid-template-areas:
      "header  header"
      "sidebar main"
      "footer  footer";
    grid-template-columns: 240px 1fr;
  }
}

.site-header  { grid-area: header;  }
.site-sidebar { grid-area: sidebar; }
.site-main    { grid-area: main;    }
.site-footer  { grid-area: footer;  }
```

---

## Rule 10 — Responsive Design: Mobile First

```css
/* 1. Base styles — designed for mobile (smallest screen) */
.card-grid {
  display: grid;
  grid-template-columns: 1fr; /* 1 column on mobile */
  gap: var(--space-md);
}

/* 2. Tablet (640px and up) */
@media (min-width: 640px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr); /* 2 columns */
  }
}

/* 3. Desktop (1024px and up) */
@media (min-width: 1024px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr); /* 3 columns */
  }
}
```

**Common breakpoints:**
- `480px` — small mobile
- `640px` — large mobile / small tablet
- `768px` — tablet
- `1024px` — desktop
- `1280px` — wide desktop

---

## Rule 11 — Focus Styles: Never Remove Without Replacing

```css
/* CORRECT — visible custom focus style */
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 3px;
  border-radius: 2px;
}

/* WRONG — removes focus with no replacement */
:focus {
  outline: none; /* keyboard users cannot navigate */
}
```

---

## Rule 12 — Forbidden Patterns

```
❌ !important         Use sparingly. Fix specificity issues properly.
❌ px for font-size   Use rem instead (respects user browser settings).
❌ Fixed width        Use max-width; fixed widths break on small screens.
❌ #id in CSS         Use .class selectors for all styling.
❌ outline: none      Never remove focus without replacing it.
❌ Deep nesting       More than 3 selector levels is too specific.
❌ Magic numbers      If you write padding: 37px, add a comment explaining why.
❌ Inline styles      All CSS goes in the external stylesheet.
❌ height: 100vh      Use min-height: 100dvh for mobile safety.
```

---

## Rule 13 — Validate Before Submission

1. Go to **https://jigsaw.w3.org/css-validator/**
2. Choose "By direct input"
3. Paste your CSS
4. Fix all errors before submitting
5. Zero errors required to pass any milestone
