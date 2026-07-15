# Liquid Glass SaaS Design System

## Overview

A futuristic SaaS landing page design language featuring **liquid glass effects** over deep purple-black backgrounds with electric green accents. Originated from a SaaS hero section prototype designed for "APEX" revenue growth platform.

Core philosophy: Create depth and premium feel through layered glassmorphism, gradient borders, and high-contrast neon accents against near-black backgrounds.

## Color Tokens

```css
:root {
  /* Background */
  --bg-primary: hsl(260 87% 3%);      /* Near-black with slight purple */
  --bg-secondary: hsl(240 4% 16%);    /* Dark surface */
  --bg-tertiary: hsl(240 4% 20%);     /* Borders */

  /* Text */
  --text-primary: hsl(40 6% 95%);     /* Warm off-white */
  --text-heading: hsl(40 10% 96%);    /* Brightest text */
  --text-sub: hsl(40 6% 82%);         /* Secondary text */
  --text-muted: hsl(240 4% 16%);      /* Muted text */

  /* Accent */
  --accent-primary: hsl(121 95% 76%); /* Electric green #87FB89 */
  --accent-text: hsl(0 0% 5%);        /* Dark text on green buttons */
}

/* Dark mode only (no toggle) */
[data-theme="dark"] {
  background: var(--bg-primary);
  color: var(--text-primary);
}
```

## Typography

```css
/* Primary font */
@import url('https://fonts.googleapis.com/css2?family=Geist+Sans:wght@400;500;600;700&display=swap');

:root {
  --font-sans: 'Geist Sans', system-ui, sans-serif;
  --font-serif: 'Playfair Display', serif; /* For decorative headings only */
  --font-mono: 'Space Grotesk', monospace; /* For code/technical content */
}

body {
  font-family: var(--font-sans);
  font-weight: 400;
  line-height: 1.6;
  letter-spacing: 0.02em;
}

h1, h2, h3 {
  font-family: var(--font-sans);
  font-weight: 600;
  letter-spacing: -0.01em;
  line-height: 1.05;
}

h1 { font-size: clamp(2.8rem, 8vw, 6rem); }
h2 { font-size: clamp(2rem, 6vw, 4rem); }
h3 { font-size: clamp(1.2rem, 4vw, 2.5rem); }

/* Special formatting */
.eyebrow {
  font-size: 0.75rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: hsl(40 6% 82% / 0.6);
}
```

## Component Styles

### 1. Liquid Glass Pill (Primary UI Element)

```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(4px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  overflow: hidden;
  position: relative;
}

/* Vertical gradient border using pseudo-element */
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  padding: 1.4px;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.45) 0%,
    rgba(255, 255, 255, 0.15) 20%,
    rgba(255, 255, 255, 0) 40%,
    rgba(255, 255, 255, 0) 60%,
    rgba(255, 255, 255, 0.15) 80%,
    rgba(255, 255, 255, 0.45) 100%
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}

/* Button variant */
.liquid-glass-btn {
  border-radius: 9999px; /* rounded-full */
  padding: 12px 24px;
  color: var(--text-primary);
  transition: all 0.3s ease;
}

.liquid-glass-btn:hover {
  background: rgba(255, 255, 255, 0.05);
}
```

### 2. Electric Green Button

```css
.btn-primary {
  background: var(--accent-primary);
  color: var(--accent-text);
  font-weight: 500;
  border-radius: 12px;
  padding: 16px 32px;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  background: hsl(121 95% 66%); /* Slightly darker green */
  transform: translateY(-1px);
}

.btn-primary:focus-visible {
  outline: 2px solid var(--accent-primary);
  outline-offset: 2px;
}
```

### 3. Announcement Badge

```css
.announcement-badge {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 8px 16px;
  border-radius: 9999px;
  font-size: 0.875rem;
  font-weight: 500;
}

.announcement-badge .chip {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 4px 12px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 9999px;
  font-size: 0.75rem;
}
```

## Textures / Patterns

### Glass Morphism Effect
```css
.glass-card {
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.05) 0%,
    rgba(255, 255, 255, 0.01) 100%
  );
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
}
```

### Gradient Border Effect
```css
.gradient-border {
  position: relative;
  border-radius: 12px;
}

.gradient-border::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 12px;
  padding: 1px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.4),
    rgba(135, 251, 137, 0.2),
    rgba(255, 255, 255, 0.1)
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
}
```

## Animation / Motion

### Fade Up Entry Animation
```css
@keyframes fade-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-up {
  animation: fade-up 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* Staggered delays */
.fade-up-delay-1 { animation-delay: 0.1s; }
.fade-up-delay-2 { animation-delay: 0.2s; }
.fade-up-delay-3 { animation-delay: 0.3s; }
```

### Marquee Scroll Animation
```css
@keyframes marquee-scroll {
  0% { transform: translateX(0%); }
  100% { transform: translateX(-50%); }
}

.marquee-scroll {
  animation: marquee-scroll 20s linear infinite;
  display: flex;
  gap: 32px;
}
```

## Theme Variants

This design is **dark mode only** — no toggle. The near-black background with purple tint creates the primary brand experience.

## Quick Start

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Liquid Glass SaaS</title>
  <style>
    :root {
      --bg-primary: hsl(260 87% 3%);
      --text-primary: hsl(40 6% 95%);
      --accent-primary: hsl(121 95% 76%);
      --font-sans: 'Inter', system-ui, sans-serif;
    }

    body {
      background: var(--bg-primary);
      color: var(--text-primary);
      font-family: var(--font-sans);
      margin: 0;
    }

    .liquid-glass {
      background: rgba(255, 255, 255, 0.01);
      backdrop-filter: blur(4px);
      border-radius: 12px;
      padding: 24px;
      position: relative;
    }

    .liquid-glass::before {
      content: '';
      position: absolute;
      inset: 0;
      border-radius: 12px;
      padding: 1.4px;
      background: linear-gradient(
        180deg,
        rgba(255,255,255,0.45) 0%,
        rgba(255,255,255,0) 50%,
        rgba(255,255,255,0.45) 100%
      );
      -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
      -webkit-mask-composite: xor;
      mask-composite: exclude;
      pointer-events: none;
    }

    .btn-accent {
      background: var(--accent-primary);
      color: black;
      padding: 12px 24px;
      border-radius: 8px;
      font-weight: 600;
      text-decoration: none;
      display: inline-block;
    }
  </style>
</head>
<body>
  <div class="liquid-glass">
    <h1>Accelerate Your Growth</h1>
    <p>Drive your funnel forward with clever workflows.</p>
    <a href="#" class="btn-accent">Get Started</a>
  </div>
</body>
</html>
```
