# CLAUDE.md

This file configures Claude Code for one-page website projects.
It is the single entry point — read it first, follow the order exactly.

---

## Reading Order — Do Not Skip

Read these files in this exact order before writing any code:

1. **This file** — `CLAUDE.md` — rules, workflow, content sourcing
2. **`PROJECT.md`** — client brief, colors, fonts, sections, assets
3. **`DESIGN.md`** — universal design principles (layout, spacing, motion, depth)
4. **`REFERENCES.md`** — reference handling protocol (URLs, screenshots, strictness)
5. **`TESTING.md`** — testing workflow (run tests continuously, not only at the end)
6. **Library `index.md`** — read before building (location provided per project)

---

## Library Usage

A reusable code library exists. Before building any component:

1. Read the library `index.md` 
2. Check the **Component Index** for matching components (nav, hero, cards, accordion, etc.)
3. If a match exists, read that project entry and use its code as a starting point
4. Adapt to the current project's design tokens and content — never copy blindly
5. If no match exists, build from scratch following DESIGN.md principles

This saves resources and ensures consistency across projects.

---

## Role

You are building a single-page website. Output: one `Website.html` file with all CSS inline. Tailwind via CDN. No build step. No frameworks.

---

## Architecture

```
index.html                ← the entire site
assets/                   ← images (provided by user or placeholders)
PROJECT.md                ← client brief (filled per project)
CLAUDE.md                 ← this file
DESIGN.md                 ← design principles
REFERENCES.md             ← reference protocol
TESTING.md                ← testing workflow
serve.mjs                 ← static file server
screenshot.mjs            ← multi-viewport screenshot tool
```

---

## Content Sourcing Rules

### Priority Order

1. **Provided content** — if the user provides text, use it exactly as written
2. **Client links** — if the user provides URLs (Facebook, website, directory listings), visit them and extract real data
3. **Sector research** — if content gaps remain, research similar websites from the same sector and use that information to fill structural or descriptive gaps only
4. **Placeholders** — for anything still unknown, use clearly marked placeholders

### Hard Content Rules

- Never invent factual business details: pricing, addresses, certifications, staff names, opening hours, or claims — unless supported by provided or researched sources
- Never copy competitor text word-for-word — paraphrase structure, ideas, and industry-standard wording only
- Contact details (phone, address, email) must come from provided or researched sources — never invented
- If the user provides exact text, use it verbatim — do not rephrase or "improve" it
- use lithaunian language for content if the user provides Lithuanian sources or specifies Lithuanian in PROJECT.md


### Placeholder Convention

When data is unknown and cannot be researched:

```html
<!-- Visible placeholder — warm italic style -->
<span class="placeholder">[PLACEHOLDER — needs confirmation]</span>
```

Placeholders must:
- Be **visually obvious** in the rendered page (styled, not hidden)
- Use warm muted italic styling so the client can see what needs confirming
- Never render as blank or invisible
- Include a brief note of what's needed: `[PLACEHOLDER — confirm price]`, `[PLACEHOLDER — add phone number]`

---

## Hard Rules — Always Active

These rules override everything else. No exceptions.

### CSS & Animation
- No `transition-all` anywhere — always specify exact properties
- Only animate `transform` and `opacity`
- `prefers-reduced-motion`: disable all non-essential animations
- All colors must be CSS custom properties at `:root` — no hardcoded hex in components
- No default Tailwind blue/indigo as primary color

### Interaction
- `cursor-pointer` on every interactive element — no exceptions
- Every button, link, and clickable element must have hover/focus states
- Accordion content expands via `max-height` transition — never `display: none` toggle

### Layout
- Two-column splits: strictly use the ratio from PROJECT.md (typically 61.8 / 38.2) — never equal columns unless specified
- Split section photos bleed to viewport edge — no container clipping
- Full-width sections (hero, photo grids) span all 12 columns with no outer padding

### Content Integrity
- Do not add sections not listed in PROJECT.md
- Do not use emojis as UI icons — SVG only (Heroicons or Lucide)

### Images
- Use real images from `assets/` when they exist
- Use `https://placehold.co/WxH/BG/TEXT` for placeholders — match the project's accent and text colors
- Apply consistent photo treatment per PROJECT.md (filter values if specified)

---

## Conflict Resolution — Priority Order

When specs conflict, resolve using this hierarchy (highest first):

1. **PROJECT.md section-specific specs** — most specific wins
2. **PROJECT.md global specs** — project-level tokens and rules
3. **REFERENCES.md** — P0 references before P1, P1 before P2
4. **DESIGN.md** — universal principles
5. **CLAUDE.md hard rules** — always active regardless of above

---

## CSS Architecture

### Dual Token System

Define colors twice — in CSS custom properties AND in Tailwind config — so both syntaxes work:

```html
<!-- In <script> Tailwind config -->
tailwind.config = {
  theme: {
    extend: {
      colors: {
        'bg-base': 'var(--bg-base)',
        'accent': 'var(--accent)',
        /* mirror all :root tokens here */
      }
    }
  }
}
```

This allows `var(--accent)` in inline styles and `text-accent` / `bg-bg-base` in Tailwind classes.

### Reusable Typography Classes

Define heading and label classes in `<style>` instead of repeating Tailwind chains:

```css
.heading-hero   { /* display font, italic, clamp(3rem, 7vw, 6rem) */ }
.heading-section { /* display font, upright, clamp(2rem, 4vw, 3.5rem) */ }
.heading-split  { /* display font, uppercase, split section titles */ }
.category-label { /* display font 600, letter-spacing: 0.15em */ }
.label-style    { /* body font, tiny uppercase, section eyebrows */ }
```

Values come from PROJECT.md — these are structural patterns, not exact values.

### Grain Texture Overlay

For warmth, use an SVG `feTurbulence` grain as a `::after` pseudo-element data URI at 3–5% opacity. Zero file cost, no external asset needed. Only apply if PROJECT.md requests texture.

---

## Font Loading

Always follow this pattern for Google Fonts:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=FONT1:wght@WEIGHTS&family=FONT2:wght@WEIGHTS&display=swap" rel="stylesheet">
```

Rules:
- `preconnect` to both domains — reduces connection latency
- `display=swap` — text renders immediately in fallback, swaps when fonts load
- Load only weights actually used (check PROJECT.md)
- Define system font fallbacks in CSS: `font-family: 'Display Font', Georgia, serif`
- Maximum 2 font families per project

---

## Image Best Practices

- `loading="lazy"` on all images below the fold (not on hero)
- `object-fit: cover` on all editorial/section images
- Define a reusable class for photo treatment:
  ```css
  .editorial-photo {
    width: 100%; height: 100%;
    object-fit: cover;
    filter: contrast(1.02) saturate(0.92); /* adjust per PROJECT.md */
  }
  ```
- Use `srcset` for hero images when multiple sizes are available
- Decorative images: `alt=""` — content images: descriptive `alt` text
- Placeholder images: `https://placehold.co/WxH/BG/TEXT` using project accent and text colors

---

## JavaScript Architecture

### Scroll Reveal (Intersection Observer)

Single observer instance for all `.reveal` elements. Trigger once, then unobserve:

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target);
    }
  });
}, { rootMargin: '0px 0px -40px 0px' });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

Stagger variants: add delay classes (`.stagger-1`, `.stagger-2`) with `transition-delay`.

### Accordion

- Toggle `.open` class on content container
- Animate via `max-height` transition (400ms ease) — never `display: none`
- **Calculate max-height dynamically using `scrollHeight`** — never hardcode a pixel value
- Update `aria-expanded` on the button
- Rotate toggle icon via `transform: rotate(45deg)`

```javascript
function toggleAccordion(btn) {
  const content = btn.nextElementSibling;
  const isOpen = content.classList.toggle('open');
  content.style.maxHeight = isOpen ? content.scrollHeight + 'px' : '0';
  btn.setAttribute('aria-expanded', isOpen);
}
```

### Mobile Menu

- Fixed overlay with z-index above content but below modals
- Toggle `.open` class
- Lock body scroll: `document.body.style.overflow = 'hidden'` on open, `''` on close
- Close menu on nav link click (so navigation works)

### Smooth Scroll

```javascript
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    e.preventDefault();
    document.querySelector(a.getAttribute('href'))
      ?.scrollIntoView({ behavior: 'smooth' });
  });
});
```

### Reduced Motion

Check `prefers-reduced-motion` in JS too — not just CSS:

```javascript
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
// Skip stagger delays, reduce durations, disable scroll animations if true
```

---

## Carousel / Slider Guidelines

When building an infinite carousel:

1. **Clone items** — duplicate the full list before and after originals for seamless loop
2. **Track index** starts at `cloneCount` (first real item)
3. On reaching end, listen for `transitionend` → instant jump (no animation) back to real items
4. **Touch/swipe**: track `touchstart` → `touchmove` → `touchend`, threshold ~20% of slide width
5. **Keyboard**: arrow keys trigger prev/next
6. **Responsive**: calculate card width via CSS variable, recalculate on `resize`
7. **Pagination dots**: generate dynamically, update active state using modular index
8. **Disable buttons during animation** to prevent multi-click issues
9. Parent container must not have `overflow: hidden` if using negative-margin breakout trick

---

## Modal / Multi-Step Form Pattern

### Modal

- `z-index` layering: nav (50) < backdrop (100) < modal (200)
- Backdrop: semi-transparent dark + `backdrop-filter: blur(8px)`
- Backdrop click closes modal
- Body scroll lock on open, release on close
- Close button + Escape key both close

### Multi-Step Form

- Track `currentStep` as state variable
- Validate current step before allowing "Next"
- Populate later steps from earlier selections (e.g. category → services)
- Show step indicators (dots, progress bar, or numbered steps)
- Summary screen before final submit
- Success state replaces form content

---

## Data Deduplication

Business data that appears in multiple places (phone, address, name, hours) must be defined once:

```javascript
const BUSINESS = {
  name: 'Business Name',
  phone: '+370...',
  phoneDisplay: '(0 601) 23874',
  address: 'Street, City',
  hours: { weekdays: '...', saturday: '...', sunday: '...' }
};
```

Then reference `BUSINESS.phone` everywhere — nav, footer, booking section, map panel. When the client updates a phone number, it changes in one place.

---

## Common Pitfalls

Avoid these — they caused real issues during builds:

| Pitfall | Fix |
|---------|-----|
| Accordion `max-height` hardcoded (e.g. 400px) | Use `el.scrollHeight` dynamically |
| Carousel parent has `overflow: hidden` | Remove it — breaks negative-margin breakout |
| `will-change: transform` left permanently on carousel | Remove after animation or use only during active slides |
| Google Maps needs API key for styling | Use iframe + CSS `filter: grayscale(1) contrast(1.1)` instead — no key needed |
| Phone/address duplicated in 3+ places | Use JS constants (see Data Deduplication above) |
| Hero loads full-size image on mobile | Use `srcset` or serve optimized size |
| `transition-all` slips in via Tailwind class | Search for it before delivery — replace with specific properties |
| Form inputs without associated `<label>` | Every input needs a `<label>` with matching `for`/`id` |

---

## Commands

```bash
# Install dependencies (run once if node_modules/ missing)
npm install

# Start dev server
node serve.mjs

# Take multi-viewport screenshots
node screenshot.mjs
```

---

## Screenshot Workflow

```bash
node serve.mjs         # start server (background)
node screenshot.mjs    # captures multiple viewports → ./screenshots/
```

After screenshotting, inspect the PNGs. Check against PROJECT.md section specs.
Stop iterating screenshots when localhost works cleanly. Hand off to user.

---

## Build Workflow

1. Read all files per **Reading Order** above
2. Check library for reusable components
3. Visit all reference URLs from REFERENCES.md — build a Reference Mapping
4. Extract content from provided sources (per Content Sourcing Rules)
5. Build `index.html`
6. Start server → take screenshots → review
7. Fix issues → re-screenshot once
8. Run Pre-Delivery Checklist from TESTING.md
9. Stop when localhost runs cleanly. Hand off.
