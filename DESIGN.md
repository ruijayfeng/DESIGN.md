# Pop-Brutalism DESIGN.md

> A design language that fuses Neo-Brutalism's raw physicality with POP art's chromatic energy.

**Origin**: Reverse-engineered from [app.ziwei.pro](https://app.ziwei.pro) (StarAsk — AI astrology analysis)
**Showcase**: [pop-chroma.vercel.app](https://pop-chroma.vercel.app)

---

## Core Philosophy

Pop-Brutalism is built on **three tensions**:

| Axis | One End | The Other | How |
|------|---------|-----------|-----|
| Serious vs Playful | Bold display fonts | Rounded cute fonts | Font stack layering |
| Immersive vs Energetic | Dark cosmic backgrounds | Neon accent colors | Color contrast |
| Hard vs Soft | Hard offset shadows | Glassmorphism blur | Theme switching |

The result: an interface that feels like a **handmade zine meets a professional dashboard**.

---

## 1. Color System

### Dual-Layer Architecture

Pop-Brutalism uses **two independent color layers** that switch separately:

**Brand Layer** — standard UI elements, toggles via `prefers-color-scheme` or class:

| Role | Light | Dark |
|------|-------|------|
| Brand | `#C74B2A` (vermillion) | `#E8633F` |
| Text | `#18181b` | `#F4EDE4` (warm white) |
| Background | `#faf9f6` | `#0f0d0b` |

**POP Layer** — Neo-Brutalism components, toggles via `data-pop-theme`:

| Token | Default | Soft | Glass |
|-------|---------|------|-------|
| `--ink` | `#0a0a0f` (pure black) | `#141414` | `#2f2e2b` (warm gray) |
| `--paper` | `#faf7ee` (warm white) | `#fffefa` | `rgba(255,255,255,.58)` |
| `--neon-yellow` | `#ffe53d` | `#ffec1f` | `#b86c55` (desaturated) |
| `--neon-magenta` | `#ff3df4` | `#9b7cff` | `#b86c55` (desaturated) |
| `--neon-cyan` | `#3dd5ff` | `#62e5ff` | `#8a9492` (desaturated) |
| `--neon-lime` | `#b6ff3c` | `#b9f66f` | `#8c8f7c` (desaturated) |
| `--neon-violet` | `#a17bff` | `#aa8fff` | `#ded8cf` (desaturated) |

**Key insight**: In Glass theme, all neon colors desaturate to brown/gray — this is intentional. Glassmorphism requires low saturation to feel premium.

### Chat Bubble Colors

Independent from the above, tuned for readability in conversation:

```
bubble-yellow:  #fdffde
bubble-lime:    #d8ff94
bubble-cyan:    #adedff
bubble-purple:  #cdd6ff
```

---

## 2. Typography

### Four-Layer Font Stack

| Layer | Font Stack | Use Case |
|-------|-----------|----------|
| **Display** | Bowlby One → ZCOOL KuaiLe → Noto Sans SC | Headlines, logo |
| **Cute** | ZCOOL KuaiLe → Bowlby One → Noto Sans SC | Playful labels |
| **Data** | JetBrains Mono → SF Mono → Consolas | Numbers, code, badges |
| **Body** | Noto Sans SC → PingFang SC → system-ui | Paragraphs, buttons |

**Design intent**:
- Bowlby One's weight → authority, strength
- ZCOOL KuaiLe's roundness → friendliness, fun
- JetBrains Mono's monospace → precision, data
- Noto Sans SC's neutrality → comfortable reading

---

## 3. The POP Formula

Every Pop-Brutalism component shares this CSS recipe:

```css
.component {
  background:    var(--paper);           /* paper base */
  border:        var(--outline);         /* bold solid outline */
  box-shadow:    var(--shadow-hard);     /* hard offset shadow */
  border-radius: var(--radius-card);     /* rounded corners */
  transform:     rotate(var(--rot, 0deg)); /* micro-rotation */
}
```

### Shadow Scale

```css
--shadow-hard-sm:  2px 2px  0 var(--ink);  /* small  */
--shadow-hard:     3px 3px  0 var(--ink);  /* medium */
--shadow-hard-md:  6px 6px  0 var(--ink);  /* large  */
--shadow-hard-lg: 10px 10px 0 var(--ink);  /* xlarge */
```

### Outline Scale

```css
--outline-thin:  2.5px solid var(--ink);
--outline:       3px   solid var(--ink);
--outline-thick: 5px   solid var(--ink);
```

### Border Radius

```css
--radius-chip:    8px;   /* tags */
--radius-card:    11px;  /* cards */
--radius-sticker: 14px;  /* stickers */
--radius-pill:    999px; /* capsules */
```

---

## 4. Component Kit

### Sticker Card

The base building block. Color variants via background override:

```
default (paper) | cyan | lime | yellow | magenta | violet | ink
```

### Chip (Tag)

Inline label with icon gap:

```css
.chip {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 14px;
  font-weight: 700;
  font-size: 13px;
}
```

### Pill (Capsule)

Smaller, fully rounded:

```css
.pill {
  padding: 4px 10px;
  border-radius: 999px;
  font-weight: 800;
  font-size: 11px;
}
```

### Button

The signature interaction: **press-down feedback** via translate + shadow reduction:

```css
.btn {
  background: var(--neon-yellow);
  padding: 10px 18px;
  font-weight: 900;
  border-radius: 12px;
}
.btn:active {
  transform: translate(1px, 1px);
  box-shadow: 1px 1px 0 var(--ink);
}
```

### Avatar

CSS-drawn minimalist face using `radial-gradient`:

```css
.avatar .face {
  background:
    radial-gradient(circle at 30% 35%, white 0 3px, transparent 3px),
    radial-gradient(circle at 70% 35%, white 0 3px, transparent 3px),
    radial-gradient(ellipse at 50% 60%, var(--ink) 0 4px, transparent 5px);
}
```

### Keypoint Card

Content card with a floating label badge:

```css
.keypoint-card__label {
  display: inline-block;
  border: 2px solid var(--ink);
  border-radius: 8px;
  box-shadow: 2px 2px 0 var(--ink);
  padding: 6px 18px;
}
```

---

## 5. Texture System

Four CSS-only background textures, zero image dependencies:

### Halftone

Simulates print halftone dots:

```css
background-image: radial-gradient(
  circle at 1px 1px,
  var(--halftone) 1px,
  transparent 0
);
background-size: 8px 8px;
```

Color variants adjust dot radius and spacing:
- lime: 5px grid, 1.2px dots
- cyan: 9px grid, 1.4px dots
- magenta: 4px grid, 1px dots (densest)
- yellow: 11px grid, 1.5px dots (sparsest)

### Stripe

Diagonal lines at 45° / -45°:

```css
background-image: repeating-linear-gradient(
  45deg,
  rgba(0,0,0,.3) 0 3px,
  transparent 3px 9px
);
```

### Burst

Radial fan pattern:

```css
background-image: repeating-conic-gradient(
  from 0deg at 50% 50%,
  var(--neon-magenta) 0deg 10deg,
  rgba(0,0,0,.18) 10deg 12deg
);
```

### Hatch

Cross-hatch lines (simulates hand-drawn shading):

```css
background-image:
  repeating-linear-gradient(45deg, rgba(10,10,15,.12) 0 1px, transparent 1px 6px),
  repeating-linear-gradient(-45deg, rgba(10,10,15,.12) 0 1px, transparent 1px 6px);
```

---

## 6. Page Background

Three gradient presets, one per theme:

**Default** — colorful with halftone overlay:
```css
background:
  radial-gradient(circle at 1px 1px, var(--halftone) 1px, transparent 0) 0 0 / 14px 14px,
  linear-gradient(180deg, #d4f5ff, #fff0d0 60%, #ffd6f5);
background-attachment: fixed;
```

**Soft** — warm, subtle:
```css
background:
  radial-gradient(... 22px 22px),
  linear-gradient(180deg, #fffaf0, #f1fbff);
```

**Glass** — layered radial glows:
```css
background:
  linear-gradient(90deg, #ffffffc7, #ffffff6b, #fff0 44%),
  radial-gradient(circle at 84% 12%, rgba(184,108,85,.08), transparent 34%),
  radial-gradient(circle at 52% 100%, rgba(138,148,146,.08), transparent 38%),
  linear-gradient(180deg, #f5f2ec, #eef0ed 52%, #f7f4ef);
```

---

## 7. Animation Catalog

| Name | Effect | Duration | Use |
|------|--------|----------|-----|
| fadeUp | ↑12px + fade in | 0.3–0.4s | Element entrance |
| slideInLeft/Right | ←20px + fade in | 0.25s | Directional entrance |
| scale-in | 0.95→1 + fade in | 0.2s | Modal/popover |
| drawer-up | ↑100%→0 | 0.3s | Bottom sheet |
| bounce | ↑25%↔0 | 1s loop | Attention |
| pulse | opacity 1↔0.5 | 2s loop | Breathing |
| spin | 360° rotation | 1s loop | Loading |
| thinking-bounce | ↑3px + opacity | 1s loop | AI thinking |
| ink-pulse | scale 1→1.5 + opacity | 1.4s | Brand effect |
| logo-pop | scale 0→1.15→1 | 0.6s | Logo reveal |

---

## 8. Theme Degradation Strategy

This is the most sophisticated part of Pop-Brutalism.

When switching themes, components **don't just change colors — they change materiality**:

| Component | Default (Neo-Brutalism) | Soft | Glass |
|-----------|------------------------|------|-------|
| Sticker Card | Hard shadow + bold outline | Reduced shadow | Backdrop blur |
| Neon Colors | Full saturation | Slightly muted | Desaturated to brown/gray |
| Shadows | Solid offset `3px 3px 0` | Smaller offset `4px 4px 0` | Soft drop shadow |
| Outlines | `3px solid` | `2.5px solid` | `1px solid rgba(...)` |
| Textures | Full halftone/stripes | Larger dots, lower contrast | No texture |

**The rule**: As you move from Default → Soft → Glass, everything becomes more transparent, more blurred, more muted. The interface transitions from "printed zine" to "frosted glass".

---

## 9. Micro-Rotation

The `--rot` custom property adds slight rotation (typically -2° to 2°) to cards and tags:

```css
transform: rotate(var(--rot, 0deg));
```

This breaks the grid's rigidity and creates a **handmade collage** feeling — like stickers slapped onto a notebook at slightly different angles.

---

## 10. Responsive Strategy

| Breakpoint | Layout |
|------------|--------|
| < 640px | Single column, mobile-first |
| 640–1023px | 2–6 column grid |
| ≥ 1024px | Two-panel: `260px sidebar + 1fr content` |
| ≥ 1280px | Three-panel: `260px + 430px + 1.2fr` |

---

## 11. Brand Mark: Three-Color Offset Star

The logo is a five-pointed star drawn in **three overlapping layers**, each offset by 2px:

| Layer | Color | Offset |
|-------|-------|--------|
| Back | Cyan `#3DD5FF` | (+4, +4) |
| Mid | Magenta `#FF3DF4` | (+2, +2) |
| Front | Ink `#0A0A0F` | (0, 0) |

This creates depth, motion, and POP art energy — recognizable at any size.

---

## Quick Start

```css
/* 1. Import tokens */
:root {
  --ink: #0a0a0f;
  --paper: #faf7ee;
  --neon-yellow: #ffe53d;
  --neon-magenta: #ff3df4;
  --neon-cyan: #3dd5ff;
  --neon-lime: #b6ff3c;
  --shadow-hard: 3px 3px 0 var(--ink);
  --outline: 3px solid var(--ink);
}

/* 2. Apply the formula */
.card {
  background: var(--paper);
  border: var(--outline);
  box-shadow: var(--shadow-hard);
  border-radius: 11px;
  transform: rotate(var(--rot, 0deg));
}

/* 3. Add halftone texture */
.card--textured {
  background-image: radial-gradient(
    circle at 1px 1px, rgba(0,0,0,.1) 1px, transparent 0
  );
  background-size: 8px 8px;
}

/* 4. Add press feedback */
button:active {
  transform: translate(1px, 1px);
  box-shadow: 1px 1px 0 var(--ink);
}
```

---

## License

This design language specification is released under **CC BY 4.0**.
Use it freely in personal and commercial projects.

---

*Reverse-engineered with care from StarAsk's production CSS.*
*Design system showcase: [pop-chroma.vercel.app](https://pop-chroma.vercel.app)*
