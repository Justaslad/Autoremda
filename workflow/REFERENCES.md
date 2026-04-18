# REFERENCES.md

Protocol for handling all design references — URLs, screenshots, and layout images.

---

## Reference Types

Every reference must have a **type** and a **strictness level**.

### Types

| Type | What it is |
|------|-----------|
| `layout` | Full-page screenshot or URL used for overall page structure |
| `section` | Screenshot or URL of a specific section to replicate |
| `component` | A single UI element (button, card, nav, accordion row) |
| `typography` | Font pairing, sizing, spacing reference |
| `palette` | Color scheme reference |
| `interaction` | Animation, hover state, or micro-interaction reference |
| `spacing` | Whitespace, padding, margin reference |

### Strictness Levels

| Level | Meaning | What to do |
|-------|---------|-----------|
| **COPY** | Replicate the structure as closely as possible | Match layout, proportions, element order, spacing rhythm. Do not copy text, brand marks, or images. |
| **INTERPRET** | Use as strong guidance, adapt to fit the project | Capture the essence — proportions, hierarchy, visual weight — but adjust details to match project tokens. |
| **INSPIRE** | Loose inspiration only | Take a general feeling or one specific aspect (e.g. "the whitespace") and apply it freely. |

---

## Reference Table

Fill this per project. One row per reference.

| ID | Type | Strictness | Source | What to extract | Notes |
|----|------|-----------|--------|----------------|-------|
| R1 | | | | | |
| R2 | | | | | |
| R3 | | | | | |

**Source:** URL, or path to screenshot file in `assets/references/`

**What to extract:** Be specific. Examples:
- "3-column card layout with thin border, no shadow, no radius"
- "Accordion row: number left, name center, toggle right"
- "Hero typography scale and letter-spacing"
- "Section vertical padding rhythm"

---

## Reference Workflow

### When a URL is provided:

1. **Fetch and inspect** the page using available tools (browser dev tools, extensions, or screenshot script)
2. **Identify** the specific section or pattern referenced
3. Build a **Reference Mapping** before coding:

```yaml
reference_mapping:
  R1:
    source: "url or file"
    applies_to: "Section 2 — Hero"
    extract:
      - "full viewport height background image"
      - "centered overlay with label → headline → CTA"
      - "gradient overlay treatment"
    do_not_copy:
      - "brand name or logo"
      - "exact text content"
      - "specific images"
```

4. **During build**, use the mapping to guide structure decisions
5. **After build**, compare against reference per TESTING.md visual comparison workflow

### When a screenshot is provided:

1. **View the image** to understand the layout
2. **Note** structure, proportions, spacing, hierarchy, typography treatment
3. Add to Reference Mapping with the same detail level
4. Compare the built result against the screenshot

### When multiple references conflict:

Priority order:
1. References with strictness **COPY** override **INTERPRET** and **INSPIRE**
2. Section-specific references override global layout references
3. If two COPY references conflict for the same section, ask the user

---

## Do-Not-Copy Constraints

Regardless of strictness level, never copy:

- Brand names, logos, or wordmarks
- Exact text content or copy
- Specific photographs or illustrations
- Proprietary icon sets
- Exact color hex values (use project tokens instead, unless specified otherwise in PROJECT.md)
- Domain-specific claims or certifications

You may replicate:
- Layout structure and proportions
- Spacing rhythm and whitespace patterns
- Typography scale relationships (not exact values)
- Animation timing and easing patterns
- Component interaction patterns (accordion behavior, hover states)
- Grid and column structures

---

## Visual Comparison Checklist

After building, compare each referenced section by using chrome dev tools to place the reference image side by side with your build. Check:

- [ ] **Structure** — element order matches reference
- [ ] **Proportions** — column ratios, aspect ratios match
- [ ] **Spacing** — vertical/horizontal rhythm is similar
- [ ] **Hierarchy** — visual weight distribution matches
- [ ] **Typography treatment** — scale, tracking, weight relationships match
- [ ] **Interaction** — hover/click behavior matches (for COPY references)
- [ ] **Edge behavior** — bleeds, overflows, clipping match reference intent
