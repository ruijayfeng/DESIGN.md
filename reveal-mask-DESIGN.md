# Reveal-Mask DESIGN.md

> An interactive design system built around mouse-tracking mask reveal effects for before/after comparisons.

**Origin**: Makeup before/after demonstration
**Showcase**: [makeup-reveal.vercel.app](https://makeup-reveal.vercel.app)

---

## Core Philosophy

Reveal-Mask is built on **three principles**:

| Principle | Expression | Technical Implementation |
|-----------|-----------|-------------------------|
| Minimal | Pure black background, no decoration | `background: #0a0a0a` |
| Interactive | Mouse movement reveals hidden content | CSS `mask-image` + JS `--mx/--my` |
| Elegant | Ultra-light typography, generous spacing | `font-weight: 300`, `letter-spacing: 0.15em` |

The result: an interface that feels like a **spotlight in darkness** — the cursor becomes a flashlight revealing hidden beauty.

---

## 1. Color System

### Minimal Palette

Reveal-Mask uses an extremely restrained color palette:

| Role | Value | Usage |
|------|-------|-------|
| Background | `#0a0a0a` | Page background, pure black with subtle warmth |
| Text Primary | `#ffffff` | Headlines, main content |
| Text Secondary | `rgba(255,255,255,0.5)` | Subtitles, descriptions |
| Text Tertiary | `rgba(255,255,255,0.35)` | Instructions, hints |
| Cursor Ring | `rgba(255,255,255,0.4)` | Custom cursor border |
| Shadow | `rgba(0,0,0,0.6)` | Card elevation |

**Design intent**: The near-black background creates maximum contrast for the reveal effect. White text at various opacities creates visual hierarchy without adding color complexity.

---

## 2. Typography

### Single Font Family

| Property | Value | Purpose |
|----------|-------|---------|
| Font Family | `'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif` | Clean, universal CJK support |
| Weight Light | `300` | Headlines — elegant, airy feel |
| Weight Regular | `400` | Body text |
| Weight Medium | `500` | Emphasis (rarely used) |

### Responsive Font Sizing

```css
/* Headlines scale with viewport */
font-size: clamp(28px, 5vw, 48px);

/* Body text scales smoothly */
font-size: clamp(13px, 2vw, 16px);
```

**Letter spacing strategy**:
- Headlines: `0.15em` — wide spacing for luxury feel
- Body: `0.05em` — subtle breathing room
- Instructions: `0.05em` — matches body

---

## 3. The Mask Formula

The core CSS pattern that powers the reveal effect:

```css
.reveal-layer {
  /* Circle mask centered at mouse position */
  -webkit-mask-image: radial-gradient(
    circle 120px at var(--mx, -100%) var(--my, -100%),
    black 100%,    /* Fully visible at center */
    transparent 100% /* Fully transparent at edge */
  );
  mask-image: radial-gradient(
    circle 120px at var(--mx, -100%) var(--my, -100%),
    black 100%,
    transparent 100%
  );
}
```

### JavaScript Position Tracking

```javascript
// Convert mouse position to percentage
const px = ((e.clientX - rect.left) / rect.width) * 100;
const py = ((e.clientY - rect.top) / rect.height) * 100;

// Update CSS custom properties
element.style.setProperty('--mx', px + '%');
element.style.setProperty('--my', py + '%');
```

### Mask Size Variants

| Device | Radius | Rationale |
|--------|--------|-----------|
| Desktop | `120px` | Comfortable hover area |
| Mobile | `80px` | Smaller for thumb-sized interaction |

**Key insight**: The mask starts at `-100%` position (off-screen) so the reveal layer is completely hidden until the user interacts.

---

## 4. Component Architecture

### Reveal Container

```css
.reveal-wrap {
  position: relative;
  width: 90vw;
  max-width: 900px;
  aspect-ratio: 1672 / 941;  /* Fixed image ratio */
  cursor: none;               /* Hide default cursor */
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 20px 80px rgba(0,0,0,0.6);
}
```

### Layer Stack

```
┌─────────────────────────────┐
│   After Layer (z-index: 2)  │  ← Masked, revealed on hover
├─────────────────────────────┤
│   Before Layer (z-index: 1) │  ← Always visible (default state)
├─────────────────────────────┤
│   Container (.reveal-wrap)  │
└─────────────────────────────┘
```

### Custom Cursor

```css
.cursor-ring {
  position: fixed;
  width: 240px;              /* 2× mask radius */
  height: 240px;
  border: 1.5px solid rgba(255,255,255,0.4);
  border-radius: 50%;
  pointer-events: none;
  mix-blend-mode: difference; /* Inverts on light/dark areas */
  transform: translate(-50%, -50%);
}
```

**Design intent**: The cursor ring is exactly 2× the mask radius, creating a visual frame around the reveal area. `mix-blend-mode: difference` ensures visibility on both light and dark image areas.

---

## 5. Animation System

### Entrance Animation

```css
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Staggered entrance */
.header    { animation: fadeUp 0.8s ease-out 0.2s forwards; }
.reveal    { animation: fadeUp 0.8s ease-out 0.5s forwards; }
.instruction { animation: fadeUp 0.8s ease-out 0.8s forwards; }
```

### Cursor Visibility

```css
.cursor-ring {
  opacity: 0;
  transition: opacity 0.3s;
}
.cursor-ring.visible {
  opacity: 1;
}
```

**Timing strategy**: 300ms stagger between header → content → instruction creates a cinematic reveal sequence.

---

## 6. Responsive Strategy

### Mobile-First Approach

```css
/* Default: mobile */
.reveal-wrap {
  width: 90vw;
  cursor: default;
}

/* Desktop enhancements */
@media (hover: hover) {
  .reveal-wrap { cursor: none; }
  .cursor-ring { display: block; }
}

/* Touch devices */
@media (hover: none) {
  .cursor-ring { display: none; }
  .reveal-after {
    mask-image: radial-gradient(circle 80px ...);
  }
}
```

### Touch Events

```javascript
// Touch support (passive: false required for preventDefault)
wrap.addEventListener('touchmove', (e) => {
  e.preventDefault();  // Prevent scroll while revealing
  const touch = e.touches[0];
  // ... same position calculation as mouse
}, { passive: false });
```

---

## 7. Performance Considerations

### Hardware Acceleration

The mask position updates via CSS custom properties (`--mx`, `--my`), which triggers only compositing — no layout or paint:

```css
/* This is GPU-accelerated */
mask-image: radial-gradient(circle at var(--mx) var(--my), ...);
```

### Image Loading Strategy

```html
<!-- Critical images load eagerly -->
<img src="before.jpg" loading="eager">
<img src="after.jpg" loading="eager">
```

**Key insight**: Both images must load before interaction feels smooth. Use `loading="eager"` and consider `fetchpriority="high"` for the before image.

---

## 8. Extension Points

### Adding More Reveal Layers

The system supports unlimited layers. Example: add a "detail" layer:

```css
.reveal-detail {
  z-index: 3;
  mask-image: radial-gradient(circle 60px at var(--mx) var(--my), ...);
}
```

### Alternative Mask Shapes

```css
/* Square reveal */
mask-image: linear-gradient(
  45deg,
  black var(--mx),
  transparent var(--mx)
);

/* Star burst */
mask-image: conic-gradient(
  from 0deg at var(--mx) var(--my),
  black 0deg, transparent 30deg,
  black 60deg, transparent 90deg
  /* ... repeat */
);
```

### Opacity Transition

For softer reveal, add a gradient falloff:

```css
mask-image: radial-gradient(
  circle 120px at var(--mx) var(--my),
  black 60%,      /* Fully visible center */
  transparent 100% /* Fade to transparent */
);
```

---

## 9. Content Guidelines

### Image Requirements

| Requirement | Specification | Rationale |
|-------------|---------------|-----------|
| Aspect Ratio | `1672:941` (≈16:9) | Cinematic, works on all screens |
| Composition | Identical framing | Mask reveal must align perfectly |
| Lighting | Same light setup | Consistent feel across reveal |
| Resolution | ≥ 1672px wide | Sharp on retina displays |

### Use Cases

| Category | Before | After | Notes |
|----------|--------|-------|-------|
| Beauty | Bare face | Makeup | Original use case |
| Renovation | Old room | New room | Same angle required |
| Photography | RAW | Edited | Same composition |
| Design | Wireframe | Final UI | Same layout |

---

## Quick Start

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .reveal-wrap {
      position: relative;
      aspect-ratio: 16/9;
      cursor: none;
    }
    .layer-before, .layer-after {
      position: absolute;
      inset: 0;
    }
    .layer-before { z-index: 1; }
    .layer-after {
      z-index: 2;
      mask-image: radial-gradient(
        circle 100px at var(--mx, -100%) var(--my, -100%),
        black 100%, transparent 100%
      );
    }
    img { width: 100%; height: 100%; object-fit: cover; }
  </style>
</head>
<body>
  <div class="reveal-wrap" id="reveal">
    <div class="layer-before"><img src="before.jpg"></div>
    <div class="layer-after"><img src="after.jpg"></div>
  </div>
  <script>
    const wrap = document.getElementById('reveal');
    const after = wrap.querySelector('.layer-after');
    wrap.addEventListener('mousemove', (e) => {
      const rect = wrap.getBoundingClientRect();
      const px = ((e.clientX - rect.left) / rect.width) * 100;
      const py = ((e.clientY - rect.top) / rect.height) * 100;
      after.style.setProperty('--mx', px + '%');
      after.style.setProperty('--my', py + '%');
    });
  </script>
</body>
</html>
```

---

## License

This design system documentation is released under **CC BY 4.0**.
