# TESTING.md

Testing workflow for one-page website projects.
Tests run continuously during implementation — not only at the end.

---

## When to Test

| Moment | What to test |
|--------|-------------|
| After building each section | Layout fidelity for that section |
| After all sections built | Full responsive pass, visual consistency |
| After adding interactions | Functionality (accordion, nav, modals) |
| Before delivery | Full checklist below |

---

## Test Categories

### 1. Layout Fidelity

Verify each section matches PROJECT.md specs:

- [ ] Section order matches PROJECT.md exactly
- [ ] Column ratios match spec (61.8/38.2 for splits, etc.)
- [ ] Full-bleed sections span entire viewport width
- [ ] Split photos bleed to viewport edge (no container clipping)
- [ ] Photo grids have zero gutters (if specified)
- [ ] Card grids use correct column count and gap
- [ ] Spacing between sections meets DESIGN.md minimums
- [ ] Content containers respect max-width constraints
- [ ] Hero fills specified height (100vh or as defined)

### 2. Responsive Behavior

Test at these widths: **375px**, **768px**, **1024px**, **1440px**

- [ ] Navigation collapses to hamburger on mobile
- [ ] Cards stack correctly (3-col → 2-col → 1-col or carousel)
- [ ] Split sections stack on mobile (correct order: photo/text)
- [ ] Photo grids adapt (2×2 → stacked on narrow screens)
- [ ] Font sizes scale smoothly (no abrupt jumps)
- [ ] No horizontal overflow at any viewport
- [ ] Touch targets are minimum 44×44px on mobile
- [ ] Adequate padding on mobile (nothing touching edges)

### 3. Functionality

- [ ] All nav links scroll to correct sections
- [ ] Accordion opens/closes smoothly (max-height transition)
- [ ] Accordion toggle icon rotates on open
- [ ] Only one accordion item open at a time (if specified)
- [ ] CTA buttons trigger correct action (scroll, modal, link)
- [ ] Modal opens and closes (if applicable)
- [ ] Mobile hamburger menu opens/closes
- [ ] Phone/email links use correct `tel:` and `mailto:` href
- [ ] External links open in new tab
- [ ] Smooth scroll behavior works

### 4. Visual Consistency

- [ ] All colors use CSS custom properties — no hardcoded hex in components
- [ ] All CTA buttons look identical (same size, color, shape)
- [ ] All section headings use consistent font and scale
- [ ] All labels use consistent tracking and size
- [ ] Photo treatment (filter) applied consistently
- [ ] Hover states work on all interactive elements
- [ ] No `transition-all` in code
- [ ] No default Tailwind blue/indigo visible

### 5. Accessibility Basics

- [ ] Color contrast: 4.5:1 body text, 3:1 large text
- [ ] All images have meaningful `alt` text
- [ ] Focus states visible on all interactive elements
- [ ] Semantic HTML used (`nav`, `main`, `section`, `footer`, `button`)
- [ ] `aria-expanded` on accordion buttons
- [ ] Page is navigable by keyboard (tab order makes sense)
- [ ] `prefers-reduced-motion` disables non-essential animation

### 6. Reference Comparison

For each reference in REFERENCES.md:

- [ ] Structure matches (element order, hierarchy)
- [ ] Proportions match (column ratios, aspect ratios)
- [ ] Spacing rhythm is similar
- [ ] Typography treatment matches (scale, tracking, weight)
- [ ] Interaction patterns match (for COPY-strictness references)
- [ ] Edge behavior matches (bleeds, overflows)

### 7. Code Quality

- [ ] All CSS in `<style>` block or Tailwind classes — no external stylesheet
- [ ] No unused CSS or classes
- [ ] HTML is semantic and well-structured
- [ ] No console errors
- [ ] No broken image paths
- [ ] Placeholder text is visibly styled (not hidden or blank)
- [ ] Google Fonts loaded with correct weights
- [ ] No hardcoded hex values in component HTML
- [ ] JavaScript is minimal and at bottom of file
- [ ] No performance-heavy operations (no layout thrashing in scroll handlers)

---

## Screenshot Workflow

### Setup

```bash
node serve.mjs         # start dev server (background)
node screenshot.mjs    # capture all viewports → ./screenshots/
```

### Viewports Captured

| Name | Width | Use |
|------|-------|-----|
| Mobile | 375px | iPhone SE |
| Tablet | 768px | iPad portrait |
| Laptop | 1024px | Small laptop |
| Desktop | 1440px | Full desktop |

### Screenshot Review Process

After capturing, inspect each screenshot for:

1. **Hero** — fills correct height, overlay readable, CTA visible
2. **Cards** — correct column count, borders visible, no overflow
3. **Split sections** — correct ratio, photo bleeds to edge
4. **Photo grid** — zero gutters (if specified), fills viewport width
5. **Accordion** — border-top on every row including first, numbers aligned
6. **Footer** — columns balanced, all info visible
7. **Mobile** — nothing overflows, text readable, spacing adequate

### Reference Comparison Screenshots

When comparing against reference URLs or images:

1. Screenshot the reference (if URL) or view the provided image
2. Screenshot your build at the same viewport width
3. Place them side by side
4. Check: structure, spacing, hierarchy, styling, visual balance
5. Note differences and decide which to fix (based on strictness level)
6. Fix and re-screenshot once

---

## Pre-Delivery Checklist

Run this before handing off. Every box must be checked.

### Structure
- [ ] All sections from PROJECT.md present in correct order
- [ ] No extra sections added beyond PROJECT.md
- [ ] Correct split ratios on all two-column layouts

### Tokens
- [ ] `:root` CSS variables match PROJECT.md color tokens
- [ ] Typography: correct fonts loaded, correct weights
- [ ] All component code uses variables, not hardcoded values

### Content
- [ ] All provided client text used exactly as given
- [ ] Extracted data matches source URLs
- [ ] Unknown data marked with visible `[PLACEHOLDER]` styling
- [ ] Content language matches PROJECT.md specification

### Assets
- [ ] Real images from `assets/` used where they exist
- [ ] Placeholder images use project colors
- [ ] All images have `alt` text

### Interactions
- [ ] `cursor-pointer` on every interactive element
- [ ] All hover states working
- [ ] Accordion expand/collapse working
- [ ] `prefers-reduced-motion` respected

### Final
- [ ] No console errors
- [ ] No horizontal scroll at any viewport
- [ ] Screenshots reviewed at all 4 viewports
- [ ] Reference comparison done for all COPY/INTERPRET references

---

## Recommended Tooling

Tools that improve code quality for this workflow:

| Tool | Purpose | When to use |
|------|---------|-------------|
| `serve.mjs` | Local dev server | Always — serves project at localhost |
| `screenshot.mjs` | Multi-viewport screenshots | After each major build pass |
| Playwright | Browser automation for screenshots | Installed via npm |
| `fetch_webpage` | Inspect reference URLs | When building Reference Mapping |
| Browser DevTools | Layout debugging, responsive testing | During development |
| WAVE/axe | Accessibility audit | Pre-delivery |
| Lighthouse | Performance + accessibility score | Optional pre-delivery |
| Sharp (npm) | Image optimization | If images need resizing/compression |
