# Cosmic Minimalism Design System

## Overview

A stark, high-contrast portfolio design language featuring **pure black and white** with cool blue accent gradients. Originated from a single-page dark portfolio landing page prototype.

Core philosophy: Maximum impact through minimalism — pure monochrome palette, dramatic font pairing (serif display + sans-serif body), and restrained use of cool blue gradients for interactive states.

## Color Tokens

```css
:root {
  /* Backgrounds */
  --bg-primary: hsl(0 0% 4%);     /* Near-pure black */
  --bg-secondary: hsl(0 0% 8%);    /* Slightly lighter black for surfaces */

  /* Text */
  --text-primary: hsl(0 0% 96%);   /* Near-pure white */
  --text-muted: hsl(0 0% 53%);     /* Medium gray for secondary text */

  /* Borders */
  --stroke: hsl(0 0% 12%);         /* Very subtle borders */

  /* Accent */
  --accent: hsl(0 0% 96%);         /* White accent */
  --accent-gradient-start: #89AACC; /* Cool blue */
  --accent-gradient-end: #4E85BF;   /* Darker cool blue */
}

/* Dark mode only */
body {
  background: var(--bg-primary);
  color: var(--text-primary);
}
```

## Typography

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital,wght@0,400;1,400&display=swap');

:root {
  /* Body text */
  --font-body: 'Inter', system-ui, sans-serif;
  
  /* Display/heading text */
  --font-display: 'Instrument Serif', 'Playfair Display', serif;
}

body {
  font-family: var(--font-body);
  font-weight: 400;
  line-height: 1.6;
}

h1, h2, h3 {
  font-family: var(--font-display);
  font-weight: 400;
  line-height: 1.02;
  letter-spacing: -0.02em;
}

h1 { font-size: clamp(3rem, 8vw, 6rem); }
h2 { font-size: clamp(2rem, 5vw, 4rem); }
h3 { font-size: clamp(1.5rem, 3vw, 2.5rem); }

/* Subtle italic for emphasis */
.display-italic {
  font-style: italic;
  font-family: var(--font-display);
}
```

## Component Styles

### 1. Loading Screen

```css
.loading-screen {
  position: fixed;
  inset: 0;
  background: var(--bg-primary);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
}

.loading-text {
  font-size: 0.75rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.loading-progress {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  width: 200px;
  height: 2px;
  background: var(--stroke);
  border-radius: 1px;
  overflow: hidden;
}

.loading-progress::after {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 0%;
  background: linear-gradient(90deg, var(--accent-gradient-start), var(--accent-gradient-end));
  animation: progress-fill 2.7s ease-in-out forwards;
}

@keyframes progress-fill {
  0% { width: 0%; }
  100% { width: 100%; }
}
```

### 2. Accent Gradient Ring (Logo/Interactive Element)

```css
.accent-gradient {
  background: linear-gradient(90deg, var(--accent-gradient-start), var(--accent-gradient-end));
}

.logo-ring {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  border: 2px solid transparent;
  background: linear-gradient(var(--bg-primary), var(--bg-primary)) padding-box,
              linear-gradient(90deg, var(--accent-gradient-start), var(--accent-gradient-end)) border-box;
  transition: all 0.3s ease;
}

.logo-ring:hover {
  transform: scale(1.05);
}
```

### 3. Primary Button

```css
.btn-accent {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 16px 32px;
  background: var(--text-primary);
  color: var(--bg-primary);
  font-weight: 600;
  font-size: 1rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
}

.btn-accent:hover {
  background: linear-gradient(90deg, var(--accent-gradient-start), var(--accent-gradient-end));
  transform: translateY(-1px);
}

/* Ghost variant */
.btn-ghost {
  background: transparent;
  color: var(--text-primary);
  border: 1px solid var(--stroke);
}

.btn-ghost:hover {
  border-color: var(--text-primary);
}
```

## Textures / Patterns

### Animated Gradient Border

```css
@keyframes gradient-shift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.gradient-border {
  position: relative;
  border-radius: 12px;
  padding: 1px;
  background: linear-gradient(
    90deg,
    var(--accent-gradient-start),
    var(--accent-gradient-end),
    var(--accent-gradient-start)
  );
  background-size: 200% 100%;
  animation: gradient-shift 6s ease infinite;
}

.gradient-border-inner {
  background: var(--bg-primary);
  border-radius: 11px;
  padding: 24px;
}
```

### Scroll Down Indicator

```css
@keyframes scroll-down {
  0% {
    transform: translateY(-100%);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: translateY(200%);
    opacity: 0;
  }
}

.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  width: 24px;
  height: 40px;
  border: 2px solid var(--text-muted);
  border-radius: 12px;
}

.scroll-indicator::before {
  content: '';
  position: absolute;
  top: 8px;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  height: 8px;
  background: var(--text-muted);
  border-radius: 2px;
  animation: scroll-down 1.5s ease-in-out infinite;
}
```

## Animation / Motion

### Fade Up Entry

```css
@keyframes role-fade-in {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.role-fade-in {
  animation: role-fade-in 0.4s ease-out forwards;
}

.role-fade-in-delay-1 { animation-delay: 0.1s; }
.role-fade-in-delay-2 { animation-delay: 0.2s; }
.role-fade-in-delay-3 { animation-delay: 0.3s; }
```

### Exit Animations (for modals/screens)

```css
@keyframes fade-out {
  from { opacity: 1; }
  to { opacity: 0; }
}

.fade-out {
  animation: fade-out 0.6s ease-in forwards;
}
```

## Theme Variants

This design is **dark mode only** — no toggle. The pure black background creates maximum contrast for portfolio content.

## Quick Start

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cosmic Minimalism</title>
  <style>
    :root {
      --bg-primary: hsl(0 0% 4%);
      --text-primary: hsl(0 0% 96%);
      --text-muted: hsl(0 0% 53%);
      --stroke: hsl(0 0% 12%);
      --accent-gradient-start: #89AACC;
      --accent-gradient-end: #4E85BF;
    }

    body {
      background: var(--bg-primary);
      color: var(--text-primary);
      margin: 0;
      font-family: system-ui, sans-serif;
    }

    .hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 48px 24px;
    }

    .hero h1 {
      font-size: clamp(3rem, 8vw, 6rem);
      font-family: 'Georgia', serif;
      letter-spacing: -0.02em;
      line-height: 1.02;
      margin-bottom: 24px;
    }

    .btn-accent {
      padding: 16px 32px;
      background: var(--text-primary);
      color: var(--bg-primary);
      font-weight: 600;
      border-radius: 8px;
      text-decoration: none;
      transition: all 0.2s;
    }

    .btn-accent:hover {
      background: linear-gradient(90deg, var(--accent-gradient-start), var(--accent-gradient-end));
      transform: translateY(-1px);
    }
  </style>
</head>
<body>
  <section class="hero">
    <h1>Cosmic<br>Minimalism</h1>
    <a href="#" class="btn-accent">View Portfolio</a>
  </section>
</body>
</html>
```
