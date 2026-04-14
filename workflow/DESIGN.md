# DESIGN.md

Universal design principles for one-page websites.
These rules apply to every project regardless of industry, style, or client.
Project-specific values (colors, fonts, exact spacing) live in PROJECT.md.

---

## Layout Composition

### Rule of Thirds

Every section's primary focal element sits at a thirds intersection — not dead center.

- Hero headline: upper-center thirds line
- Split section headings: upper-left thirds of their column
- CTAs: lower-center or lower-right thirds

Never stack all elements dead center vertically. Offset label, heading, and CTA to different third-lines.

### Golden Ratio

Two-column splits default to **61.8% / 38.2%** unless PROJECT.md specifies otherwise.
Never use equal columns for text + photo splits.

Apply to:
- Text column vs photo column
- Photo with bio section (photo side gets the larger share or smaller — PROJECT.md decides)

### Z-Pattern

Hero and split sections follow the Z-path:
```
Label (top-left) → Element (top-right)
         ↘ Visual (mid-diagonal) ↘
              CTA (bottom-right)
```

Guide the eye naturally through content hierarchy.

### Grid System

Use a 12-column conceptual grid:

- **Full-bleed sections** (hero, photo grids): span all 12, no outer padding
- **Contained sections** (about, accordion): content centered within `max-width`
- **Split sections**: one column bleeds to viewport edge, other stays contained
- **Card grids**: equal columns within container

---

## Gestalt Principles

### Proximity
- Related elements (card title + description + CTA) cluster tightly
- Unrelated sections have generous whitespace between them
- More space between sections than between elements within a section

### Similarity
- All CTA buttons: identical size, color, shape across the page
- All nav links: visually identical treatment
- All section headings: same font, scale, and spacing

### Closure
- Hero bleeds to all four viewport edges — no visible container
- Full-width photo grids have no outer gutters
- Split section photos bleed past the grid boundary to viewport edge

---

## Spacing System

### Vertical Rhythm

| Context | Desktop | Mobile |
|---------|---------|--------|
| Between sections | min 80px | min 48px |
| Section internal padding (top/bottom) | 80–120px | 48–80px |
| Between heading and body text | 24px | 16px |
| Between body text and CTA | 32px | 24px |
| Card internal padding | 24–32px | 16–24px |

**Principle:** when in doubt, add more whitespace, not less.

### Horizontal

- Contained content: `max-width` between 720px (text-heavy) and 1280px (cards/grids)
- Body text: `max-width` between 480px and 600px for readability
- Side padding on container: `1.5rem` minimum (mobile), `6vw` (desktop)
- Full-bleed elements: zero side padding

---

## Typography Hierarchy

Specific fonts and sizes come from PROJECT.md. These are structural rules:

| Level | Role | Typical Treatment |
|-------|------|------------------|
| Display | Hero headline | Largest size, display font, may be italic |
| H2 | Section headings | Display font, upright, uppercase or title case |
| Label | Section pre-headings | Uppercase, wide letter-spacing, small size, muted or accent color |
| Body | Paragraph text | Body font, regular weight, generous line-height (1.7–1.8) |
| UI | Buttons, nav, links | Body font, medium weight, uppercase for nav, tracked |
| Small | Captions, metadata | Body font, smaller size, muted color |

### Rules
- Line height for body: minimum 1.7
- Letter-spacing for labels/nav: 0.10em–0.18em
- Heading letter-spacing: tight (-0.02em to -0.03em) for large sizes
- Use `clamp()` for responsive font sizing — never fixed pixel values for headings
- Maximum of 2 font families per project

---

## Depth & Texture

### Approach
- Depth through **photography and whitespace**, not excessive shadows
- Cards: border only (1px solid accent) — no box-shadow unless PROJECT.md specifies
- Navigation: subtle box-shadow is acceptable (ambient + key light)
- Modals: backdrop + elevation shadow

### Photo Treatment
- Apply consistent filter globally (specified in PROJECT.md)
- Hover treatment: subtle saturation or brightness shift
- Gradient overlays on hero: specified per section in PROJECT.md

### Optional Texture
- SVG grain overlay at low opacity (3–5%) for warmth — only if PROJECT.md requests
- Never add texture that competes with content readability

---

## Animation & Motion

### Scroll Animations

Default entrance pattern (override in PROJECT.md if needed):

```css
/* Element starts hidden */
opacity: 0;
transform: translateY(24px);

/* Revealed by Intersection Observer */
opacity: 1;
transform: translateY(0);
transition: opacity 600ms cubic-bezier(0.22, 1, 0.36, 1),
            transform 600ms cubic-bezier(0.22, 1, 0.36, 1);
```

### Stagger
- Sequential elements stagger with 80–120ms delay between each
- Hero: label → headline → CTA, 120ms apart
- Grid cells: 100ms between each cell

### Micro-Interactions
- CTA buttons: hover → fill change, slight scale(1.02), shadow change — `200ms`
- Text links: underline scaleX from left on hover
- Accordion toggles: rotate 45° on open — `200ms`
- Nav links: inactive links dim when one is hovered

### Hard Rules
- Only animate `transform` and `opacity` — never width, height, margin, padding, color, background
- No `transition-all` — always list specific properties
- `prefers-reduced-motion`: disable all non-essential animations
- Motion duration: 200ms for micro-interactions, 400ms for accordion expand, 600ms for scroll reveal

---

## Responsive Breakpoints

| Name | Width | Typical Layout Changes |
|------|-------|----------------------|
| Mobile | < 640px | Single column, stacked sections, hamburger nav |
| Tablet | 640–1023px | 2-column where applicable, smaller type scale |
| Desktop | 1024–1439px | Full layout, all columns active |
| Wide | ≥ 1440px | Max-width containers, generous whitespace |

### Responsive Rules
- Cards: 3-col → 2-col → 1-col (or carousel on mobile)
- Split sections: side-by-side → stacked (photo on top or bottom per PROJECT.md)
- Photo grids: maintain grid on tablet, single column below 480px
- Navigation: full nav on desktop, hamburger on mobile
- Font sizes: use `clamp()` so they scale smoothly — no breakpoint jumps

---

## Accessibility Minimums

- Color contrast: 4.5:1 for body text, 3:1 for large text (WCAG AA)
- All images: meaningful `alt` text
- All buttons: visible focus states (outline or ring)
- Semantic HTML: use `<nav>`, `<main>`, `<section>`, `<footer>`, `<button>` correctly
- Accordion buttons: `aria-expanded` attribute toggled on click
- Skip-to-content link (hidden, visible on focus)
- Interactive elements: minimum 44×44px touch target on mobile
