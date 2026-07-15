# FlowMate Minimalism Design System

## Overview

A premium, minimalist landing page design language featuring **extreme whitespace**, serif typography, and a fixed sidebar navigation pattern. Originated from an AI workflow automation platform prototype called "FlowMate".

Core philosophy: Create trust and authority through restraint — generous spacing, sophisticated serif fonts, muted color palette, and a clean two-column layout reminiscent of high-end consultancy brands.

## Color Tokens

```css
:root {
  /* Backgrounds */
  --bg-page: #fefffc;              /* Near-white warm background */
  --bg-sidebar: #ffffff;            /* Pure white sidebar */
  --bg-card: #ffffff;               /* Card backgrounds */
  --bg-hover: #eef1ed;              /* Hover states */

  /* Text */
  --text-primary: #2c2c2c;          /* Dark gray, never pure black */
  --text-secondary: #444141;        /* Secondary content */
  --text-tertiary: #646464;         /* Labels, metadata */
  --text-muted: #b4b8b4;            /* Placeholders, disabled */

  /* Borders */
  --border-light: #dde3dd;          /* Light borders */
  --border-medium: #dee2de;         /* Medium borders */
  --border-strong: #e8e8e8;         /* Strong borders */

  /* Interactive */
  --btn-primary: #000000;           /* Black primary button */
  --btn-primary-hover: #2c2c2c;     /* Dark gray on hover */
}

/* Light mode only */
body {
  background: var(--bg-page);
  color: var(--text-primary);
}
```

## Typography

```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital,wght@0,400;0,700;1,400&display=swap');

:root {
  /* Primary serif font for headings */
  --font-display: 'PPMondwest', 'Instrument Serif', 'Playfair Display', serif;
  
  /* System font fallback for body */
  --font-body: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

body {
  font-family: var(--font-body);
  font-weight: 400;
  line-height: 1.6;
}

h1, h2, h3, h4 {
  font-family: var(--font-display);
  font-weight: 400;
  letter-spacing: -0.04em;      /* Tight tracking for premium feel */
  line-height: 1.1;
}

h1 { font-size: clamp(3rem, 6vw, 5rem); }
h2 { font-size: clamp(2rem, 4vw, 3.5rem); }
h3 { font-size: clamp(1.5rem, 3vw, 2.5rem); }

/* Kerning for headings */
.heading-kerning {
  font-kerning: none;
  letter-spacing: -0.04em;
}

/* Body text */
.text-body {
  font-size: 1rem;
  line-height: 1.75;
  color: var(--text-secondary);
}

/* Small labels */
.text-small {
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-muted);
}
```

## Component Styles

### 1. Sidebar Navigation

```css
.sidebar {
  position: fixed;
  left: 0;
  top: 0;
  width: 240px;
  height: 100vh;
  background: var(--bg-sidebar);
  border-right: 2px solid var(--border-light);
  padding: 32px 24px;
  z-index: 100;
}

.sidebar-logo {
  display: block;
  margin-bottom: 48px;
}

.sidebar-nav {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.sidebar-nav a {
  display: block;
  padding: 12px 16px;
  color: var(--text-secondary);
  text-decoration: none;
  border-radius: 8px;
  transition: all 0.2s ease;
  font-weight: 500;
}

.sidebar-nav a:hover {
  background: var(--bg-hover);
  color: var(--text-primary);
}

.sidebar-nav a.active {
  background: var(--bg-hover);
  color: var(--text-primary);
  font-weight: 600;
}
```

### 2. Main Content Area

```css
.main-content {
  margin-left: 240px;
  padding: 80px 48px;
  min-height: 100vh;
}

.hero-section {
  max-width: 720px;
  margin-bottom: 120px;
}

.hero-section h1 {
  margin-bottom: 24px;
  color: var(--text-primary);
}

.hero-section .subtitle {
  font-size: 1.25rem;
  color: var(--text-secondary);
  margin-bottom: 40px;
  line-height: 1.7;
}
```

### 3. Primary Button

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 16px 32px;
  background: var(--btn-primary);
  color: #ffffff;
  font-weight: 600;
  font-size: 1rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
}

.btn-primary:hover {
  background: var(--btn-primary-hover);
  transform: translateY(-1px);
}

.btn-primary:focus-visible {
  outline: 2px solid var(--text-primary);
  outline-offset: 2px;
}

/* Secondary variant */
.btn-secondary {
  background: transparent;
  color: var(--text-primary);
  border: 1px solid var(--border-medium);
}

.btn-secondary:hover {
  background: var(--bg-hover);
}
```

## Textures / Patterns

This design relies on **negative space** rather than decorative textures. The primary visual interest comes from:

1. Typography contrast (serif vs sans-serif)
2. Generous whitespace
3. Subtle hover states
4. Clean grid alignment

No additional patterns or decorative elements are used.

## Animation / Motion

### Subtle Entry Animations

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

.animate-fade-up {
  animation: fade-up 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.animate-fade-up-delay-1 { animation-delay: 0.1s; }
.animate-fade-up-delay-2 { animation-delay: 0.2s; }
.animate-fade-up-delay-3 { animation-delay: 0.3s; }
```

### Hover Transitions

```css
/* All interactive elements get smooth transitions */
a, button, .card {
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}
```

## Theme Variants

This design is **light mode only** — no toggle. The warm near-white background creates a premium, approachable feel suitable for B2B SaaS and consultancy brands.

## Quick Start

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FlowMate Minimalism</title>
  <style>
    :root {
      --bg-page: #fefffc;
      --text-primary: #2c2c2c;
      --text-secondary: #444141;
      --font-display: 'Playfair Display', serif;
      --font-body: system-ui, sans-serif;
      --border-light: #dde3dd;
    }

    body {
      background: var(--bg-page);
      color: var(--text-primary);
      font-family: var(--font-body);
      margin: 0;
    }

    .sidebar {
      position: fixed;
      left: 0;
      top: 0;
      width: 240px;
      height: 100vh;
      border-right: 2px solid var(--border-light);
      padding: 32px;
    }

    .main-content {
      margin-left: 240px;
      padding: 80px 48px;
    }

    h1 {
      font-family: var(--font-display);
      letter-spacing: -0.04em;
      line-height: 1.1;
    }

    .btn-primary {
      display: inline-block;
      padding: 16px 32px;
      background: #000;
      color: #fff;
      font-weight: 600;
      border-radius: 8px;
      text-decoration: none;
      transition: background 0.2s;
    }

    .btn-primary:hover {
      background: #2c2c2c;
    }
  </style>
</head>
<body>
  <aside class="sidebar">
    <h3>FlowMate</h3>
  </aside>
  <main class="main-content">
    <h1>AI workflow automation, simplified.</h1>
    <p style="color: var(--text-secondary); margin-bottom: 32px;">
      Build complex workflows without code.
    </p>
    <a href="#" class="btn-primary">Get Started</a>
  </main>
</body>
</html>
```
