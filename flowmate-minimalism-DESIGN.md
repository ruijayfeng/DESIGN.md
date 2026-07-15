# FlowMate Minimalism DESIGN.md

> A clean, editorial SaaS aesthetic built on **off-white backgrounds**, **serif display typography** (PPMondwest), and a **fixed sidebar layout**. Originated from an AI workflow automation platform landing page.

**Origin**: [motionsites.ai](https://motionsites.ai) — Section #282 "FlowMate Landing"
**Showcase**: [flowmate-minimalism.vercel.app](https://flowmate-minimalism-demo-i5i9dx8kb-fengk677-2300s-projects.vercel.app)

---

## Core Philosophy

FlowMate Minimalism is defined by **one tension**:

| Axis | Warm | Cool | How |
|------|------|------|-----|
| Texture | Pure solid colors | No gradients, no shadows | Flat surfaces only |
| Typography | Serif display (PPMondwest) | Sans-serif system fallback | Font layering |
| Layout | Fixed sidebar (240px) | Fluid content area | CSS grid / flex |
| Interaction | Spring animations | Hover color shifts only | Framer Motion |

The result: an interface that feels like **reading a premium editorial magazine** — calm, spacious, typographically driven. No visual noise.

---

## 1. Color System

### Off-White Palette (HSL / RGB)

Unlike dark-themed systems, FlowMate lives in **near-white territory**. Every color is a muted gray or near-gray — no pure blacks, no saturated hues:

| Role | Value | Hex | Use |
|------|-------|-----|-----|
| `--background` | `#fefffc` | `#fefffc` | Page background — off-white with warm tint |
| `--text-primary` | `#2c2c2c` | `#2c2c2c` | Headlines, active nav items |
| `--text-secondary` | `#444141` | `#444141` | Body paragraphs, descriptions |
| `--text-tertiary` | `#646464` | `#646464` | Labels, less important text |
| `--text-muted` | `#b4b8b4` | `#b4b8b4` | Inactive nav, placeholder text |
| `--border-light` | `#dde3dd` | `#dde3dd` | Sidebar border, subtle dividers |
| `--border-medium` | `#dee2de` | `#dee2de` | Card borders, section separators |
| `--border-default` | `#e8e8e8` | `#e8e8e8` | Horizontal section dividers (`border-t`) |
| `--hover-bg` | `#eef1ed` | `#eef1ed` | Active nav item bg, hover surfaces |
| `--button-black` | `#000000` | `#000000` | Primary CTA button |
| `--button-hover` | `#2c2c2c` | `#2c2c2c` | CTA hover state |

### Color Usage Rules

1. **No saturated colors anywhere** — everything is a gray or near-gray
2. **Text hierarchy uses opacity, not color changes** — primary → secondary → tertiary → muted
3. **Borders use green-tinted grays** (`#dde3dd`, `#dee2de`) — subtle, not neutral gray
4. **Button is the only solid black** on the page — maximum visual weight for action

### Sidebar Specific Colors

| Element | Background | Text |
|---------|-----------|------|
| Active nav item | `#eef1ed` | `#2c2c2c` (primary) |
| Inactive nav item | transparent | `#b4b8b4` (muted) |
| Sidebar bg | transparent | inherits text-primary |
| Sidebar border | — | `2px solid #dde3dd` |

---

## 2. Typography

### Single Serif Font + System Fallback

FlowMate uses **one custom serif font** as the display hero, paired with system fonts for body:

| Layer | Font Stack | Use Case | Size Range | Weight |
|-------|-----------|----------|------------|--------|
| **Display** | `PPMondwest` → `Georgia` → `serif` | Headlines, brand wordmark | 32px → 50px → 70px | Medium (500) |
| **Body** | System sans-serif (Inter, SF Pro, etc.) | Paragraphs, descriptions, labels | 14px – 18px | Regular (400) |
| **Nav / Small** | System sans-serif | Nav links, buttons, badges | 13px – 16px | Medium (500) |

### Custom Font Import

```css
/* PPMondwest — loaded as a local file from the original source */
@font-face {
  font-family: 'PPMondwest';
  src: url('https://www.generalintelligencecompany.com/_next/static/media/17330fd087386262-s.p.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
  font-kerning: normal;
}

/* Apply globally */
body {
  font-kerning: 'none';
  letter-spacing: '-0.04em';
}
```

**Note**: `fontKerning: 'none'` and `letterSpacing: '-0.04em'` are set globally — this tight tracking is characteristic of the editorial aesthetic.

### Display Heading Scale

| Breakpoint | Font Size | Line Height | Max Width |
|------------|-----------|-------------|-----------|
| Mobile (<768px) | 32px | 0.95 | 100% |
| Tablet (≥768px) | 50px | 0.95 | 100% |
| Desktop (≥1024px) | 70px | 0.95 | 700px |

**Design intent**: PPMondwest's serif weight at 70px creates a **magazine cover** feel. The tight line height (0.95) makes multi-line headlines feel compact and intentional. The max-width constraint prevents the text from stretching across the entire viewport on ultra-wide screens.

---

## 3. The Sidebar-Content Formula

FlowMate's signature layout is a **fixed sidebar + fluid content area**:

```css
/* Desktop layout (1024px+) */
.app-layout {
  display: flex;
}

.sidebar {
  position: fixed;
  left: 0;
  top: 0;
  width: 240px;
  height: 100vh;
  border-right: 2px solid var(--border-light);
  /* No background needed — transparent */
}

.content-area {
  margin-left: 240px;
  flex: 1;
  min-height: 100vh;
}

/* Navbar sits inside content area, offset by sidebar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  margin-left: 240px;
  background: rgba(254, 255, 252, 0.9);
  backdrop-filter: blur(4px);
}
```

### Mobile / Tablet Breakpoint

Below 1024px, the sidebar disappears and the navbar becomes full-width:

```css
@media (max-width: 1023px) {
  .sidebar { display: none; }
  .content-area { margin-left: 0; }
  .navbar { margin-left: 0; }
}
```

---

## 4. Component Kit

### Sidebar Navigation

```css
.sidebar-nav {
  padding: 24px 16px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.sidebar-item {
  padding: 10px 16px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  transition: background 0.2s, color 0.2s;
  cursor: pointer;
}

/* Active state */
.sidebar-item.active {
  background: var(--hover-bg);
  color: var(--text-primary);
}

/* Inactive state */
.sidebar-item:not(.active) {
  color: var(--text-muted);
}

.sidebar-item:not(.active):hover {
  color: var(--text-tertiary);
  background: rgba(0,0,0,0.03);
}
```

### Glassmorphic Overlay Card (Video Section)

The signature "glass" element in FlowMate is a **heavy glass overlay** on top of the background video:

```css
.glass-overlay-card {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  min-width: 480px;
  max-width: 600px;
  
  /* Heavy frosted glass */
  backdrop-filter: blur(16px);
  background-image: linear-gradient(
    in oklab,
    rgba(255, 255, 255, 0.35) 0px,
    rgba(255, 255, 255, 0.12) 100px
  );
  
  /* Soft border */
  border: 6px solid rgba(255, 255, 255, 0.2);
  
  /* Subtle shadow + inner glow */
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.5);
  
  border-radius: 20px;
  padding: 20px 24px;
}
```

**Key insight**: This glass effect is **heavier** than the Liquid Glass SaaS version — 16px blur vs 4px, 6px border width vs 1.4px, solid color background vs near-transparent. It's meant to float **on top of video**, not over solid backgrounds.

### Feature Cards

Six cards in a responsive grid, each with a title, description, and icon row:

```css
.feature-card {
  border: 2px solid var(--border-medium);
  border-radius: 16px; /* rounded-2xl */
  padding: 24px;
  transition: border-color 0.2s;
}

.feature-card:hover {
  border-color: #b8beb8; /* hover border gets darker */
}

.feature-title {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 8px;
}

.feature-desc {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.5;
  margin-bottom: 16px;
}

.feature-icons {
  display: flex;
  gap: 8px;
}

.feature-icon {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: #f0f0f0;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### CTA Buttons

Two button styles, both fully rounded:

```css
.btn-ghost {
  background: white;
  border: 2px solid var(--border-light);
  border-radius: 9999px;
  padding: 10px 20px;
  font-size: 14px;
  font-weight: 500;
}

.btn-solid {
  background: var(--button-black);
  color: white;
  border: none;
  border-radius: 9999px;
  padding: 10px 20px;
  font-size: 14px;
  font-weight: 500;
  transition: background 0.2s;
}

.btn-solid:hover {
  background: var(--button-hover);
}
```

---

## 5. Layout Anatomy

### Page Sections (Top to Bottom)

| Section | Padding | Description |
|---------|---------|-------------|
| Navbar | Fixed, `left-0 lg:left-[240px]` | Brand wordmark + login/sign-up buttons |
| Hero | `pt-12–20 pb-12` | h1 + subtitle + intro video CTA |
| Video | Full width | Background video + glass overlay card |
| Features | `border-t border-[#e8e8e8]` | 6 cards in 3-col grid |
| Cards Carousel | `border-t border-[#e8e8e8]` | Auto-rotating carousel |

### Card Carousel

5 cards showing in groups of 3, auto-rotating every 4 seconds:

```css
.carousel-card {
  height: 500px;
  border-radius: 16px;
  overflow: hidden;
  position: relative;
}

.carousel-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-card .gradient-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(0deg, rgba(0,0,0,0.6) 0%, transparent 50%);
}

.carousel-card:hover img {
  transform: scale(1.05);
}
```

### Grid System

| Breakpoint | Feature Cards | Carousel |
|------------|--------------|----------|
| Mobile (<768px) | 1 column | 1 card visible |
| Tablet (≥768px) | 2 columns | 2 cards visible |
| Desktop (≥1024px) | 3 columns | 3 cards visible |

---

## 6. Animation Catalog

| Name | Effect | Trigger | Use |
|------|--------|---------|-----|
| TextFade | `translateY(18px)→0` + opacity `0→1` | Scroll into view (IntersectionObserver) | Headlines, section titles |
| Spring (video) | `translateY(18px)→0` + opacity `0→1` | Scroll into view, spring easing | Glass overlay card |
| Carousel slide | `translateX(±20px) + scale 0.95→1` | Auto (4s) or manual nav | Feature cards carousel |
| Nav active indicator | Smooth scroll with IntersectionObserver | Scroll | Sidebar highlight tracking |

### TextFade Configuration

```tsx
// Default variants
const variants = {
  hidden: { opacity: 0, y: 18 },
  visible: { opacity: 1, y: 0 }
};

// Props
interface TextFadeProps {
  direction: 'up' | 'down';  // default: 'up'
  stagger: number;            // default: 0.15 (seconds)
  viewport?: object;          // IntersectionObserver config
}
```

---

## 7. Responsive Strategy

| Breakpoint | Sidebar | Navbar | Hero Heading | Feature Grid |
|------------|---------|--------|--------------|--------------|
| `< 768px` (mobile) | Hidden | Full-width, fixed top | 32px | 1 column |
| `768–1023px` (tablet) | Hidden | Full-width, fixed top | 50px | 2 columns |
| `≥ 1024px` (desktop) | Fixed 240px | Offset 240px | 70px | 3 columns |

**Navigation behavior**:
- Desktop: Fixed sidebar with vertical nav items (Home, Video, Features, Cards)
- Mobile/Tablet: Fixed top navbar with "Log in" + "Sign up" buttons

---

## 8. Quick Start

### Minimal Copy-Paste

```css
/* 1. Token setup */
:root {
  --background: #fefffc;
  --text-primary: #2c2c2c;
  --text-secondary: #444141;
  --text-tertiary: #646464;
  --text-muted: #b4b8b4;
  --border-light: #dde3dd;
  --border-medium: #dee2de;
  --border-default: #e8e8e8;
  --hover-bg: #eef1ed;
  --button-black: #000000;
}

/* 2. Sidebar layout */
.sidebar {
  position: fixed;
  left: 0; top: 0;
  width: 240px; height: 100vh;
  border-right: 2px solid var(--border-light);
}

.content { margin-left: 240px; }

@media (max-width: 1023px) {
  .sidebar { display: none; }
  .content { margin-left: 0; }
}

/* 3. Glass overlay card (for video sections) */
.glass-card {
  backdrop-filter: blur(16px);
  background-image: linear-gradient(in oklab, rgba(255,255,255,0.35) 0px, rgba(255,255,255,0.12) 100px);
  border: 6px solid rgba(255,255,255,0.2);
  box-shadow: 0 8px 32px rgba(0,0,0,0.12), inset 0 1px 0 rgba(255,255,255,0.5);
  border-radius: 20px;
}

/* 4. Feature card */
.feature-card {
  border: 2px solid var(--border-medium);
  border-radius: 16px;
  padding: 24px;
  transition: border-color 0.2s;
}
.feature-card:hover { border-color: #b8beb8; }

/* 5. CTA buttons */
.btn-primary {
  background: var(--button-black);
  color: white;
  border-radius: 9999px;
  padding: 10px 20px;
}
.btn-secondary {
  background: white;
  border: 2px solid var(--border-light);
  border-radius: 9999px;
  padding: 10px 20px;
}
```

```jsx
// React — Hero section
export function Hero() {
  return (
    <section className="pt-20 pb-12" style={{ background: 'var(--background)' }}>
      <h1 className="text-32 sm:text-50 lg:text-70" style={{
        fontFamily: 'PPMondwest, Georgia, serif',
        lineHeight: 0.95,
        maxWidth: '700px',
        color: 'var(--text-primary)',
        letterSpacing: '-0.04em',
        fontKerning: 'none',
      }}>
        Transform your workflow using plain English
      </h1>
      
      <p className="mt-6 max-w-620px" style={{
        color: 'var(--text-secondary)',
        fontSize: '18px',
        lineHeight: 1.5,
      }}>
        FlowMate connects to your current apps, builds smart workflows, 
        and manages operations.
      </p>
      
      <button className="btn-primary mt-8">View our intro video</button>
    </section>
  );
}
```

---

## 9. Design Principles

### What FlowMate Minimalism Avoids

| Pattern | Why Avoid | Alternative |
|---------|-----------|-------------|
| Gradients | Too decorative for editorial aesthetic | Solid colors only |
| Shadows | Too "app-like", not magazine-like | Border-only depth |
| Saturated colors | Distracts from typography | Gray hierarchy only |
| Rounded cards with shadows | Too skeuomorphic | 2px border cards |
| Drop shadows on everything | Visual noise | Selective shadow on glass card only |
| Light/dark mode toggle | Single aesthetic | Light mode only |

### What Makes It Premium

1. **Typography-first** — The serif display at 70px is the hero, not any image or icon
2. **Spacious padding** — Generous whitespace around every element
3. **Subtle color shifts** — Hover effects are color-only, no scale/morph
4. **Heavy glass on video** — The 16px-blur glass card is the only "wow" element
5. **Consistent border weight** — Everything uses 2px borders, nothing heavier

---

*Reverse-engineered from motionsites.ai Section #282 (FlowMate Landing).*
