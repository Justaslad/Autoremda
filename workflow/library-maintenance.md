---
type: maintenance
updated: 2026-04-06
---

# Library Maintenance

Rules for maintaining this library so it stays useful as it grows.

---

## Adding a New Project

When a project is finished and you want to store it:

1. Create a new file in `projects/` named `project-name.md`
2. Use the **Project Entry Template** below — copy it into the new file
3. Fill in all fields, tag every reusable component
4. Update `[[index]]`:
   - Add a row to the **Past Projects** table
   - Add rows to the **Component Index** for each tagged component

---

## Tagging Rules

Tags make components findable across projects. Use this format:

```
#component/category-variant
```

**Tag categories:**

| Category | Examples |
|----------|---------|
| `nav` | `#component/nav-floating` `#component/nav-sticky` `#component/nav-hamburger` |
| `hero` | `#component/hero-fullscreen` `#component/hero-split` `#component/hero-video` |
| `cards` | `#component/cards-grid` `#component/cards-carousel` `#component/cards-masonry` |
| `split` | `#component/split-text-photo` `#component/split-photo-text` |
| `photo` | `#component/photo-grid` `#component/photo-gallery` `#component/photo-lightbox` |
| `accordion` | `#component/accordion` `#component/tabs` `#component/toggle` |
| `pricing` | `#component/pricing-table` `#component/pricing-accordion` |
| `footer` | `#component/footer-columns` `#component/footer-minimal` |
| `form` | `#component/form-contact` `#component/form-booking` `#component/form-newsletter` |
| `other` | `#component/modal` `#component/testimonials` `#component/map` `#component/carousel` `#component/marquee` `#component/cta-section` `#component/about-section` `#component/team-section` |

If none of these fit, create a new tag following the same pattern and add that tag to this file and index.md

---

## Naming Conventions

- **Project files:** `projects/project-name.md` — lowercase, hyphens, no spaces
- **Component tags:** `#component/category-variant` — lowercase, hyphens
- **Always use Obsidian wikilinks** when linking between files: `[[index]]`, `[[projects/project-name]]`

---

## When to Update index.md

Update the index whenever:
- A new project is added
- A component tag is added that doesn't exist in the Component Index yet
- A workflow file is added or renamed

---

## Project Entry Template

Copy everything below this line into a new `projects/project-name.md` file.

---

```markdown
---
type: project
name: "Project Name"
client: "Client Name"
date: YYYY-MM-DD
tech: ["Tailwind CDN", "Vanilla JS"]
components:
  - nav-floating
  - hero-fullscreen
  - cards-grid
  - accordion
  - footer-columns
status: complete
---

# Project Name

## Description

One to three sentences describing the project, the client, and what the site does.

## Sections

List every section in order:

1. **Navigation** — floating nav, left links / center wordmark / right CTA
2. **Hero** — full viewport, editorial photo, centered overlay
3. **About** — centered text block
4. ...continue for all sections

## Components

Tag each reusable component with notes on what makes it specific:

- `#component/nav-floating` — transparent on scroll, pill CTA right
- `#component/hero-fullscreen` — 100vh, gradient overlay, staggered load
- `#component/cards-grid` — 3-column, accent border, no radius
- ...continue for all components

## Design Tokens

Key color and typography values used in this project:

| Token | Value | Usage |
|-------|-------|-------|
| `--bg-base` | #value | Main background |
| `--text-primary` | #value | Body text |
| `--accent` | #value | Borders, highlights |
| Display font | Font Name | Headings |
| Body font | Font Name | Body text, UI |

## Notes

Anything notable about the build — what worked well, what was tricky, decisions made. 

## Full Code

​```html
<!-- Paste the complete index.html here -->
​```
```
