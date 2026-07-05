# Raycast-Glass DESIGN.md

> A premium dark-glass design system with macOS-native aesthetics, featuring frosted glass effects, precise spacing, and fluid micro-interactions.

**Origin**: Reverse-engineered from [raycast.com](https://www.raycast.com)
**Showcase**: Raycast's official website

---

## Core Philosophy

Raycast-Glass is built on **four pillars**:

| Pillar | Expression | Technical Implementation |
|--------|-----------|-------------------------|
| **Dark Luxury** | Deep blacks with subtle gradients | `linear-gradient(137deg, #111214, #0c0d0f)` |
| **Frosted Glass** | Translucent layers with blur | `backdrop-filter: blur(36px)` + `rgba(255,255,255,.1)` |
| **macOS Native** | System fonts, native controls | `-apple-system`, `SF Pro` aesthetics |
| **Micro-interactions** | Subtle, purposeful motion | `fadeIn`, `slideUp`, `blink` animations |

The result: an interface that feels like a **premium macOS app rendered on the web** — polished, performant, and platform-native.

---

## 1. Color System

### Background Palette

The dark theme uses carefully layered backgrounds:

| Role | Value | Usage |
|------|-------|-------|
| Base Dark | `#0a0a0f` | Page background |
| Card Gradient | `linear-gradient(137deg, #111214 4.87%, #0c0d0f 75.88%)` | Elevated surfaces |
| Glass Surface | `rgba(255,255,255,.05)` | Transparent panels |
| Glass Hover | `rgba(255,255,255,.1)` | Interactive states |
| Overlay | `rgba(0,0,0,.6)` | Modal backdrops |

### Text Hierarchy

| Role | Variable | Value |
|------|----------|-------|
| Loud (headlines) | `--Text-Loud` | `#ffffff` |
| Default (body) | `--Text-Default` | `var(--grey-200)` |
| Muted (secondary) | `--Text-Muted` | `var(--grey-300)` |
| Faint (disabled) | `--Text-Faint` | `var(--grey-400)` |
| Tertiary (hints) | `--tertiaryText` | `rgba(255,255,255,.4)` |

### Accent Colors

| Name | Value | Usage |
|------|-------|-------|
| Raycast Red | `#ff6363` | Brand, CTAs, icons |
| Success Green | `#51cf66` | Positive states |
| Warning Orange | `#ff9217` | Alerts |
| Info Blue | `#56c2ff` | Links, highlights |
| Purple | `#d8acff` | AI features |

### Grey Scale

```
--grey-50:   Lightest (rarely used in dark theme)
--grey-100:  Subtle borders
--grey-200:  Default text
--grey-300:  Muted text
--grey-400:  Faint text
--grey-500:  Disabled elements
--grey-600:  Borders, dividers
--grey-700:  Card backgrounds
--grey-800:  Elevated surfaces
--grey-900:  Deep backgrounds
```

---

## 2. Typography

### Font Stack

```css
:root {
  --font-inter: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-geist-mono: 'Geist Mono', 'SF Mono', 'Fira Code', monospace;
  --monospace-font: var(--font-geist-mono);
}
```

### Type Scale

| Element | Size | Weight | Letter Spacing |
|---------|------|--------|----------------|
| Hero Title | `clamp(36px, 5vw, 64px)` | 600 | `-0.02em` |
| Section Title | `clamp(28px, 4vw, 48px)` | 600 | `-0.01em` |
| Card Title | `20px` | 500 | `0` |
| Body | `15px` | 400 | `0` |
| Small | `13px` | 400 | `0.01em` |
| Caption | `11px` | 500 | `0.02em` |

**Design intent**: Inter provides excellent readability on screens with its tall x-height and open apertures. The negative letter-spacing on headlines creates a tight, premium feel.

---

## 3. Spacing System

### 8px Grid

Raycast uses a consistent 8px-based spacing scale:

```css
:root {
  --spacing-0-5: 2px;    /* Micro gaps */
  --spacing-1: 4px;      /* Tight spacing */
  --spacing-1-5: 6px;    /* Compact elements */
  --spacing-2: 8px;      /* Base unit */
  --spacing-2-5: 10px;   /* Form elements */
  --spacing-3: 12px;     /* Standard padding */
  --spacing-4: 16px;     /* Card padding */
  --spacing-5: 20px;     /* Section gaps */
  --spacing-6: 24px;     /* Large gaps */
  --spacing-7: 28px;     /* Major sections */
  --spacing-8: 32px;     /* Section padding */
  --spacing-9: 36px;     /* Large sections */
  --spacing-10: 40px;    /* Hero sections */
  --spacing-12: 48px;    /* Page margins */
  --spacing-13: 52px;    /* Navbar height */
}
```

### Usage Patterns

| Context | Spacing |
|---------|---------|
| Icon to text | `--spacing-2` (8px) |
| Card padding | `--spacing-4` (16px) |
| Section gap | `--spacing-8` (32px) |
| Hero padding | `--spacing-12` (48px) |

---

## 4. Glass Morphism System

### The Glass Recipe

```css
.glass-surface {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(36px);
  -webkit-backdrop-filter: blur(36px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: var(--rounding-md);
}
```

### Blur Scale

| Level | Value | Usage |
|-------|-------|-------|
| Subtle | `blur(2px)` | Soft backgrounds |
| Light | `blur(5px)` | Cards |
| Medium | `blur(10px)` | Panels |
| Heavy | `blur(20px)` | Modals |
| Ultra | `blur(36px)` | Navigation |
| Maximum | `blur(48px)` | Overlays |

### Glass Layers

```
┌─────────────────────────────────┐
│  Overlay (blur 48px)            │  z-index: 50
├─────────────────────────────────┤
│  Modal (blur 36px)              │  z-index: 40
├─────────────────────────────────┤
│  Navigation (blur 20px)         │  z-index: 30
├─────────────────────────────────┤
│  Card (blur 10px)               │  z-index: 10
├─────────────────────────────────┤
│  Background (no blur)           │  z-index: 0
└─────────────────────────────────┘
```

---

## 5. Border Radius System

### Radius Scale

```css
:root {
  --rounding-none: 0px;
  --rounding-xs: 4px;     /* Badges, small elements */
  --rounding-sm: 6px;     /* Buttons, inputs */
  --rounding-md: 8px;     /* Cards, standard */
  --rounding-normal: 10px; /* Large cards */
  --rounding-lg: 12px;    /* Panels */
  --rounding-xl: 16px;    /* Hero elements */
}
```

### Usage

| Element | Radius |
|---------|--------|
| Button | `--rounding-sm` (6px) |
| Input | `--rounding-sm` (6px) |
| Card | `--rounding-md` (8px) |
| Modal | `--rounding-lg` (12px) |
| Avatar | `50%` (circle) |
| Pill | `100px` (fully rounded) |

---

## 6. Shadow System

### Shadow Layers

Raycast uses multi-layered shadows for depth:

```css
/* Card shadow */
box-shadow: 
  0 4px 40px 8px rgba(0, 0, 0, 0.4),  /* Diffuse */
  0 0 0 0.5px rgba(0, 0, 0, 0.8),      /* Border */
  inset 0 0.5px 0 0 rgba(255, 255, 255, 0.3); /* Top highlight */

/* Inner glow */
box-shadow: 
  inset 0 1px 0 0 rgba(255, 255, 255, 0.1);

/* Elevated surface */
box-shadow: 
  0 4px 16px 0 rgba(0, 0, 0, 0.32);
```

### Shadow Patterns

| Context | Effect |
|---------|--------|
| Card | Outer shadow + inner highlight |
| Button | Inset top highlight |
| Modal | Heavy outer shadow |
| Floating | Soft ambient shadow |

---

## 7. Animation Catalog

### Timing Functions

```css
:root {
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### Standard Animations

| Name | Duration | Usage |
|------|----------|-------|
| `fadeIn` | 300ms | Page load, content appear |
| `fadeInUp` | 400ms | Hero elements, cards |
| `slideUp` | 200ms | Tooltips, dropdowns |
| `slideDown` | 200ms | Modals, panels |
| `scaleIn` | 150ms | Buttons, icons |
| `blink` | 1s infinite | Cursors, loading |

### Keyframes

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideDownAndFade {
  from {
    opacity: 0;
    transform: translateY(-4px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

## 8. Navbar Design

### Sticky Glass Navbar

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: var(--navbar-height, 64px);
  background: rgba(10, 10, 15, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  z-index: 100;
}

.navbar-content {
  max-width: var(--container-width, 1200px);
  margin: 0 auto;
  padding: 0 var(--spacing-5);
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
```

### Navbar Scroll Effect

```javascript
// Navbar becomes more opaque on scroll
window.addEventListener('scroll', () => {
  const scrolled = window.scrollY > 0;
  navbar.style.background = scrolled 
    ? 'rgba(10, 10, 15, 0.95)' 
    : 'rgba(10, 10, 15, 0.8)';
});
```

---

## 9. Card Component

### Standard Card

```css
.card {
  background: var(--Card-BG, linear-gradient(137deg, #111214 4.87%, #0c0d0f 75.88%));
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: var(--rounding-md, 8px);
  padding: var(--spacing-4, 16px);
  transition: all 0.2s var(--ease-out);
}

.card:hover {
  border-color: rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 16px 0 rgba(0, 0, 0, 0.32);
  transform: translateY(-2px);
}
```

### Card Variants

| Variant | Background | Usage |
|---------|------------|-------|
| Default | Dark gradient | Standard cards |
| Glass | `rgba(255,255,255,.05)` + blur | Floating panels |
| Solid | `var(--grey-800)` | Content blocks |
| Bordered | Transparent + border | Subtle cards |

---

## 10. Button System

### Primary Button

```css
.button-primary {
  background: var(--red-dark, #ff6363);
  color: white;
  border: none;
  border-radius: var(--rounding-sm, 6px);
  padding: var(--spacing-2-5) var(--spacing-4);
  font-weight: 500;
  font-size: 14px;
  transition: all 0.15s var(--ease-out);
  box-shadow: inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
}

.button-primary:hover {
  background: #ff7b7b;
  transform: translateY(-1px);
  box-shadow: 
    inset 0 1px 0 0 rgba(255, 255, 255, 0.2),
    0 4px 12px rgba(255, 99, 99, 0.3);
}
```

### Button Variants

| Variant | Background | Border | Usage |
|---------|------------|--------|-------|
| Primary | `#ff6363` | none | CTAs |
| Secondary | `rgba(255,255,255,.1)` | 1px solid | Secondary actions |
| Ghost | transparent | none | Tertiary actions |
| Outline | transparent | 1px solid | Subtle CTAs |

---

## 11. Responsive Strategy

### Breakpoints

```css
/* Mobile first */
@media (min-width: 480px) { /* Small phones */ }
@media (min-width: 768px) { /* Tablets */ }
@media (min-width: 1024px) { /* Small desktop */ }
@media (min-width: 1280px) { /* Large desktop */ }
```

### Container System

```css
.container {
  width: 100%;
  max-width: var(--container-width, 1200px);
  margin: 0 auto;
  padding: 0 var(--spacing-5);
}

/* Responsive padding */
@media (max-width: 768px) {
  .container {
    padding: 0 var(--spacing-4);
  }
}
```

---

## 12. Performance Optimizations

### GPU Acceleration

```css
/* Promote to own layer */
.animated-element {
  will-change: transform, opacity;
  transform: translateZ(0);
}

/* Use transform for animations */
.slide-in {
  transform: translateY(20px);
  opacity: 0;
  transition: transform 0.3s var(--ease-out), opacity 0.3s;
}
```

### Blur Optimization

```css
/* Limit blur radius for performance */
.glass-panel {
  backdrop-filter: blur(20px); /* Don't exceed 40px */
  -webkit-backdrop-filter: blur(20px);
}

/* Disable blur on low-end devices */
@media (prefers-reduced-motion: reduce) {
  .glass-panel {
    backdrop-filter: none;
    background: rgba(10, 10, 15, 0.95);
  }
}
```

---

## Quick Start

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    :root {
      --bg: #0a0a0f;
      --card-bg: linear-gradient(137deg, #111214 4.87%, #0c0d0f 75.88%);
      --text: #fff;
      --text-muted: rgba(255,255,255,.6);
      --accent: #ff6363;
      --glass: rgba(255,255,255,.05);
      --glass-border: rgba(255,255,255,.1);
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Inter', -apple-system, sans-serif;
    }

    .navbar {
      position: fixed;
      top: 0;
      width: 100%;
      background: rgba(10, 10, 15, 0.8);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    }

    .card {
      background: var(--card-bg);
      border: 1px solid var(--glass-border);
      border-radius: 8px;
      padding: 16px;
      transition: all 0.2s ease;
    }

    .card:hover {
      border-color: rgba(255, 255, 255, 0.15);
      transform: translateY(-2px);
      box-shadow: 0 4px 16px rgba(0, 0, 0, 0.32);
    }

    .button {
      background: var(--accent);
      color: white;
      border: none;
      border-radius: 6px;
      padding: 10px 20px;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.15s ease;
    }

    .button:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 12px rgba(255, 99, 99, 0.3);
    }
  </style>
</head>
<body>
  <nav class="navbar">
    <div class="logo">Raycast</div>
    <button class="button">Download</button>
  </nav>

  <main>
    <div class="card">
      <h2>Feature Card</h2>
      <p>Glass morphism with hover effects</p>
    </div>
  </main>
</body>
</html>
```

---

## License

This design system documentation is released under **CC BY 4.0**.
