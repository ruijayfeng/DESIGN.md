# Contributing

Thanks for your interest in contributing a design language spec.

<br>

## What to Submit

A pull request containing one file: `{style-name}-DESIGN.md`

The style name should be in **kebab-case**, written in English. Examples:

- `pop-brutalism-DESIGN.md`
- `glass-morphism-DESIGN.md`
- `neo-skeuomorphism-DESIGN.md`
- `swiss-minimalism-DESIGN.md`

<br>

## File Requirements

Your DESIGN.md must include all of the following sections:

### 1. Overview

- Style name and a one-line description
- Origin — where did you observe this design? (product URL, open-source project, etc.)
- Core philosophy — what makes this style distinct in 2-3 sentences

### 2. Color Tokens

- All color values as CSS custom properties
- Light and dark mode variants (if applicable)
- Semantic roles (brand, text, background, accent, etc.)

### 3. Typography

- Font stacks with fallbacks
- Which fonts are used for which purposes (display, body, data, etc.)
- Font weights and sizes for key roles

### 4. Component Styles

- At least 3 core components with full CSS
- Interactive states (hover, active, focus)
- Variants (size, color, etc.)

### 5. Textures / Patterns

- Background patterns, borders, decorative effects
- Must be reproducible in CSS (no image dependencies preferred)

### 6. Animation / Motion

- Keyframe definitions for at least 2 animations
- When and where to use each one

### 7. Theme Variants

- If the design supports multiple themes, document the switching strategy
- How components degrade across themes

### 8. Quick Start

- A minimal CSS snippet that someone can paste into a project and immediately see the style

<br>

## Screenshot Requirement

You **must** include a screenshot showing the design in action.

Two options:

**Option A — Production screenshot (preferred)**

Capture a real product using this design language. Include:

- Full-page or key-section screenshot
- At least one component visible (card, button, form, etc.)
- Light or dark mode (ideally both)

Save as `{style-name}.png` in the `/previews/` folder.

**Option B — Self-built demo**

Build a minimal HTML page demonstrating the design system. Deploy it (Vercel, Netlify, GitHub Pages) and include:

- The live URL in your DESIGN.md header
- A screenshot in `/previews/`

<br>

## Quality Bar

Before submitting, check:

- [ ] Every section has real, usable CSS (not pseudocode)
- [ ] Color tokens are copy-pasteable into a `:root` block
- [ ] Components render correctly without JavaScript
- [ ] Screenshot accurately represents the design
- [ ] No copyrighted assets (fonts, images, icons) included without license

<br>

## Naming Convention

```
{style-name}-DESIGN.md    ← the spec
previews/{style-name}.png ← the screenshot
```

Examples:
```
pop-brutalism-DESIGN.md
previews/pop-brutalism.png

glass-morphism-DESIGN.md
previews/glass-morphism.png
```

<br>

## License

All contributions are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

By submitting a PR, you agree to this license.
