# Portfolio Cosmic DESIGN.md

> A dark portfolio aesthetic combining **pure monochrome** with **cool blue accent gradients**, serif display typography, and scroll-driven parallax effects. Originated from a personal portfolio landing page for "Michael Smith."

**Origin**: [motionsites.ai](https://motionsites.ai) — Section #302 "Portfolio Cosmic"
**Showcase**: [portfolio-cosmic.vercel.app](https://portfolio-cosmic.vercel.app)

---

## Core Philosophy

Portfolio Cosmic is built on **three tensions**:

| Axis | Restrained | Bold | How |
|------|-----------|------|-----|
| Palette | Pure black + white | Cool blue gradient (#89AACC → #4E85BF) | Accent-only gradient |
| Typography | Monospace Inter (body) | Italic Instrument Serif (display) | Two font roles |
| Motion | Static bento grid | GSAP scroll parallax | Scroll-triggered reveals |

The result: a portfolio site that feels like **a high-end creative director's personal page** — minimal but with moments of cinematic depth.

---

## 1. Color System

### Monochrome Base (HSL)

The entire page uses a **pure black-to-white monochrome** foundation — no warm tones, no colors except for one cool blue gradient used as accent:

| Role | HSL | Hex | Use |
|------|-----|-----|-----|
| `--bg` | `0 0% 4%` | `#0a0a0a` | Page background — near-pure black |
| `--surface` | `0 0% 8%` | `#141414` | Card backgrounds, pills |
| `--text` | `0 0% 96%` | `#f2f2f2` | Primary text — off-white |
| `--muted` | `0 0% 53%` | `#878787` | Secondary text, labels, eyebrows |
| `--stroke` | `0 0% 12%` | `#1f1f1f` | Borders, dividers, progress bars |
| `--accent` | `0 0% 96%` | `#f2f2f2` | Same as text — for text-on-accent |

### Accent Gradient

The **only color** on the entire page — a cool blue gradient used sparingly:

| Usage | Gradient |
|-------|----------|
| Logo ring | `linear-gradient(90deg, #89AACC 0%, #4E85BF 100%)` |
| Hover borders | Same gradient applied as ring/border |
| Progress bar | Same gradient as inner fill |
| Button hover ring | Same gradient as outer glow |
| Hover pill label | Same gradient as animated border |

**CSS utility**:

```css
.accent-gradient {
  background: linear-gradient(90deg, #89AACC 0%, #4E85BF 100%);
}
```

### Why Cool Blue?

The blue (#89AACC → #4E85BF) is deliberately chosen because:
1. It's a **desaturated, muted blue** — not a loud primary blue
2. It complements the cold black/white foundation
3. It evokes "cosmic" / space / depth without being garish
4. Used only on **interactive elements** — borders, rings, progress bars — never on text or backgrounds

### Loading Screen Progress Bar Glow

```css
.progress-glow {
  box-shadow: 0 0 8px rgba(137, 170, 204, 0.35);
}
```

---

## 2. Typography

### Two-Font Stack

Portfolio Cosmic uses exactly **two fonts** in two distinct roles:

| Role | Font Stack | Weights | Use Case | Style |
|------|-----------|---------|----------|-------|
| **Display** | `Instrument Serif` → `Georgia` → `serif` | 400 italic | Headlines, name, loading words, italic accent words | Italic |
| **Body** | `Inter` → `system-ui, sans-serif` | 300–700 | Body text, labels, nav, descriptions, stats | Regular / Medium |

### Font Import

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Instrument+Serif:ital@1&display=swap');

:root {
  --font-display: 'Instrument Serif', serif;
  --font-body: 'Inter', sans-serif;
}
```

**Note**: Instrument Serif is loaded as *italic only* (ital@1) — it's only used in italic form. This creates a deliberate contrast with the geometric Inter.

### Heading Scale

| Element | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| Loading screen words | `text-4xl` | `text-6xl` | `text-7xl` |
| Hero name | `text-6xl` | `text-8xl` | `text-9xl` |
| Section headings | `text-2xl` | `text-3xl` | `text-4xl` |
| Eyebrow labels | `text-xs` | `text-xs` | `text-xs` |

### Type Hierarchy

```
Eyebrow:    text-xs, uppercase, tracking-[0.3em], muted color
Headline:   text-6xl to text-9xl, font-display italic, tight tracking
Body:       text-sm to text-base, Inter regular, muted color
Role tag:   font-display italic, animated (fades in/out)
```

### Key Tracking Values

| Element | Tracking |
|---------|----------|
| Eyebrow / labels | `tracking-[0.3em]` (wide, editorial) |
| Headlines | `tracking-tight` (compact, modern) |
| Body | default (Inter's natural spacing) |
| Scroll indicator | `tracking-[0.2em]` |

---

## 3. The Surface-Card Formula

All cards and interactive elements follow the **same material**:

```css
.cosmic-card {
  background: var(--surface);       /* #141414 — dark gray */
  border: 1px solid var(--stroke);  /* #1f1f1f — almost black */
  border-radius: 1.5rem;            /* rounded-3xl — fully rounded */
  overflow: hidden;
  transition: all 0.3s ease;
}

.cosmic-card:hover {
  background: rgba(10, 10, 10, 0.7);
  backdrop-filter: blur(12px);
}
```

### Hover Accent Border

When a card is hovered, an **animated gradient border** appears:

```css
.cosmic-card::after {
  content: '';
  position: absolute;
  inset: -2px;
  border-radius: inherit;
  background: linear-gradient(90deg, #89AACC, #4E85BF);
  opacity: 0;
  transition: opacity 0.3s;
  z-index: -1;
}

.cosmic-card:hover::after {
  opacity: 1;
  animation: gradient-shift 6s ease infinite;
  background-position: 0% 50%;
}

@keyframes gradient-shift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

---

## 4. Component Kit

### Loading Screen

Full-screen overlay shown during initial load (2700ms):

```css
.loading-screen {
  position: fixed;
  inset: 0;
  z-index: 9999;
  background: var(--bg);
}
```

| Element | Style |
|---------|-------|
| Top-left label | `text-xs text-muted uppercase tracking-[0.3em]` — "Portfolio" |
| Center words | Cycling text: "Design" → "Create" → "Inspire" (900ms each), font-display italic |
| Bottom counter | `text-6xl to text-9xl font-display tabular-nums` — counts 000→100 |
| Progress bar | `h-[3px] bg-stroke/50`, inner div with accent-gradient, `scaleX(count/100)` |

### Floating Nav Pill

A floating capsule at the top center of the page:

```css
.nav-pill {
  display: inline-flex;
  align-items: center;
  border-radius: 9999px;
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.1);
  background: var(--surface);
  padding: 8px 12px;
  transition: box-shadow 0.3s;
}

/* When scrolled: add shadow */
.nav-pill.scrolled {
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
```

| Element | Style |
|---------|-------|
| Logo circle | 9×9 circle, accent gradient border, inner bg-bg, "JA" monogram |
| Nav links | `rounded-full px-3 sm:px-4 py-1.5 sm:py-2 text-xs sm:text-sm` |
| Active link | `text-text bg-stroke/50` |
| Inactive link | `text-muted hover:text-text hover:bg-stroke/50` |
| "Say hi" button | Same as nav links, shows accent gradient border ring on hover |

### Hero Buttons

```css
/* Solid button — white bg → black bg on hover */
.btn-solid {
  border-radius: 9999px;
  padding: 14px 28px;
  font-size: 14px;
  background: var(--text);
  color: var(--bg);
  transition: all 0.3s;
}
.btn-solid:hover {
  background: var(--bg);
  color: var(--text);
  box-shadow: 0 0 0 2px linear-gradient(90deg, #89AACC, #4E85BF);
}

/* Outlined button — border → gradient ring on hover */
.btn-outline {
  border-radius: 9999px;
  padding: 14px 28px;
  font-size: 14px;
  border: 2px solid var(--stroke);
  background: var(--bg);
  color: var(--text);
  transition: all 0.3s;
}
.btn-outline:hover {
  border-color: transparent;
  box-shadow: 0 0 0 2px linear-gradient(90deg, #89AACC, #4E85BF);
}
```

### Bento Grid Card (Selected Works)

```css
.bento-card {
  background: var(--surface);
  border: 1px solid var(--stroke);
  border-radius: 1.5rem;
  position: relative;
  overflow: hidden;
  aspect-ratio: auto;
}

.bento-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.bento-card:hover img {
  transform: scale(1.05);
}

/* Halftone overlay */
.bento-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: radial-gradient(circle, #000 1px, transparent 1px);
  background-size: 4px 4px;
  opacity: 0.2;
  mix-blend-mode: multiply;
  pointer-events: none;
  z-index: 1;
}

/* Hover overlay */
.bento-card::after {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(10,10,10,0.7);
  backdrop-filter: blur(12px);
  opacity: 0;
  transition: opacity 0.3s;
  z-index: 2;
}

.bento-card:hover::after {
  opacity: 1;
}
```

**Hover label pill** (appears on hover):

```css
.hover-label {
  position: absolute;
  bottom: 20px;
  left: 20px;
  z-index: 3;
  padding: 10px 20px;
  border-radius: 9999px;
  background: white;
  font-size: 13px;
  border: 1px solid linear-gradient(90deg, #89AACC, #4E85BF);
}
```

### Journal Entry Pill

Horizontal pills with title, image thumbnail, read time, date:

```css
.journal-pill {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 16px;
  border-radius: 2.5rem; /* rounded-[40px] on sm */
  background: rgba(20,20,20,0.3);
  border: 1px solid var(--stroke);
  transition: background 0.2s;
}
.journal-pill:hover {
  background: rgba(20,20,20,0.6);
}
```

---

## 5. Layout Anatomy

### Seven Sections (Top to Bottom)

| Section | Background | Key Feature |
|---------|-----------|-------------|
| Loading | `#0a0a0a` (solid) | Counter + cycling words + progress bar |
| Hero | HLS video | Floating nav pill + name + role |
| Selected Works | `#0a0a0a` | Bento grid (4 cards, 7/5/5/7 cols) |
| Journal | `#0a0a0a` | Horizontal pill entries |
| Explorations | `#0a0a0a` | Parallax gallery (300vh scroll) |
| Stats | `#0a0a0a` | 3-column stats (20+, 95+, 200%) |
| Contact | Video (flipped) | Marquee + email CTA |

### Bento Grid Columns

```
┌───────────────┬───────────┬───────────┐
│               │           │           │
│   Automotive  │  Urban    │  Human    │
│   Motion      │  Arch.    │  Persp.   │
│  (7 cols)     │ (5 cols)  │ (5 cols)  │
│               │           │           │
└───────────────┴───────────┴───────────┘
┌───────────────┬───────────────────────────────┐
│               │                               │
│  Brand        │          Identity             │
│  Identity     │         Project               │
│ (7 cols)      │        (7 cols)              │
│               │                               │
└───────────────┴───────────────────────────────┘
```

### Parallax Section (Explorations)

```css
/* 300vh tall section — GSAP ScrollTrigger pins the center */
.explorations-section {
  min-height: 300vh;
  position: relative;
}

.explorations-content {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.explorations-cards {
  position: absolute;
  inset: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px 160px;
  max-width: 1400px;
}

.explorations-card {
  width: 320px;
  aspect-ratio: 1;
}
```

---

## 6. Texture System

### Halftone Overlay (on bento cards)

```css
.halftone-overlay {
  background-image: radial-gradient(
    circle,
    #000000 1px,
    transparent 1px
  );
  background-size: 4px 4px;
  opacity: 0.2;
  mix-blend-mode: multiply;
}
```

### Video Background with Overlay

Hero and contact sections use HLS video (.m3u8) with overlays:

```css
.hero-video-overlay {
  background: rgba(0,0,0,0.2);
  position: absolute;
  inset: 0;
}

.contact-video-flip {
  transform: scaleY(-1);
  position: absolute;
  inset: 0;
}

.contact-video-overlay {
  background: rgba(0,0,0,0.6); /* heavier than hero's 20% */
  position: absolute;
  inset: 0;
}

.bottom-fade {
  height: 192px; /* h-48 */
  background: linear-gradient(to top, var(--bg), transparent);
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
}
```

---

## 7. Animation Catalog

| Name | Effect | Duration | Trigger |
|------|--------|----------|---------|
| **Loading counter** | 000→100 via rAF | 2700ms | On mount |
| **Loading words** | Cycle: Design→Create→Inspire | 900ms each | During load |
| **Loading exit** | fade out | 400ms | After counter hits 100 |
| **Name reveal** | `opacity 0→1, y 50→0` | 1.2s, power3.out | After loading |
| **Blur in** | `opacity 0→1, blur 10px→0, y 20→0` | 1s, stagger 0.1 | After loading |
| **Role fade** | `opacity 0→1, y 8→0` | 0.4s ease-out | Every 2s (auto-cycle) |
| **Scroll reveal** | `opacity 0→1, y 30→0` | 1s, ease [0.25,0.1,0.25,1] | Section enters viewport |
| **Scroll down** | `translateY(-100%)→translateY(200%)` | 1.5s, infinite | Continuous |
| **Gradient shift** | `background-position 0%→100%→0%` | 6s, infinite | Hover on cards |
| **Parallax** | Scroll-driven x/y movement | GSAP ScrollTrigger | Scroll in Explorations section |
| **Marquee** | `xPercent: -50` | 40s, repeat -1 | On Contact section |
| **Button hover** | `scale(1)→1.05` | 0.2s | Interactive |
| **Logo ring hover** | `scale(1)→1.1` | 0.2s | Nav pill logo |

---

## 8. Responsive Strategy

| Breakpoint | Hero Name | Bento Grid | Nav Pill |
|------------|-----------|------------|----------|
| `< 768px` | `text-6xl` | 1 column | Nav links hidden, "Say hi" only |
| `768–1023px` | `text-8xl` | 2 columns | Nav links visible |
| `≥ 1024px` | `text-9xl` | 12-col bento (7/5/5/7) | Full nav with dividers |

### Parallax Cards

| Breakpoint | Card Size | Grid Gap |
|------------|-----------|----------|
| Mobile | Full width | 1 column |
| Tablet | 50% width | 2 columns, gap 48px |
| Desktop | 320px max | 2 columns, gap 160px |

---

## 9. Loading Screen Detail

The loading screen is a signature element — it transforms waiting into a **mini performance**:

```
┌─────────────────────────────────────────────┐
│ Portfolio                     097          │
│                                             │
│       Create                                │
│                                             │
│                     Build the Future →      │
│                                             │
│                                     97      │
└─────────────────────────────────────────────┘
```

| Zone | Content |
|------|---------|
| Top-left | "Portfolio" label, muted, tracking-wide |
| Center | Cycling verb: "Design" → "Create" → "Inspire" (font-display italic, large) |
| Bottom-right | 3-digit counter, font-display, tabular-nums |
| Bottom edge | 3px progress bar with accent-gradient fill, glow shadow |

---

## 10. Quick Start

### Minimal Copy-Paste

```css
/* 1. Token setup */
:root {
  --bg: hsl(0 0% 4%);
  --surface: hsl(0 0% 8%);
  --text: hsl(0 0% 96%);
  --muted: hsl(0 0% 53%);
  --stroke: hsl(0 0% 12%);
  
  --font-display: 'Instrument Serif', serif;
  --font-body: 'Inter', sans-serif;
}

/* 2. Accent gradient */
.accent-gradient {
  background: linear-gradient(90deg, #89AACC 0%, #4E85BF 100%);
}

/* 3. Card base */
.cosmic-card {
  background: var(--surface);
  border: 1px solid var(--stroke);
  border-radius: 1.5rem;
}

/* 4. Nav pill */
.nav-pill {
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.1);
  background: var(--surface);
  border-radius: 9999px;
  padding: 8px 12px;
}

/* 5. Buttons */
.btn-primary {
  border-radius: 9999px;
  padding: 14px 28px;
  background: var(--text);
  color: var(--bg);
}
.btn-outline {
  border-radius: 9999px;
  padding: 14px 28px;
  border: 2px solid var(--stroke);
  background: var(--bg);
  color: var(--text);
}

/* 6. Halftone overlay */
.halftone {
  background-image: radial-gradient(circle, #000 1px, transparent 1px);
  background-size: 4px 4px;
  opacity: 0.2;
  mix-blend-mode: multiply;
}
```

```jsx
// React — Hero section
export function Hero() {
  return (
    <section className="relative min-h-screen overflow-hidden">
      {/* HLS Video background */}
      <video autoPlay muted loop playsInline className="absolute inset-0 w-full h-full object-cover" />
      
      {/* Floating nav pill */}
      <nav className="fixed top-0 left-0 right-0 z-50 flex justify-center pt-4">
        <div className="nav-pill flex items-center gap-3">
          <div className="w-9 h-9 rounded-full border-2 border-accent-gradient flex items-center justify-center"
               style={{ background: 'var(--bg)' }}>
            <span className="font-display italic text-xs text-text">JA</span>
          </div>
          <div className="hidden sm:block w-px h-5 bg-stroke" />
          <div className="flex items-center gap-1 sm:gap-2 text-xs sm:text-sm">
            {['Home', 'Work', 'Resume'].map(link => (
              <button key={link} className={`rounded-full px-3 sm:px-4 py-1.5 sm:py-2 ${
                link === 'Work' ? 'text-text bg-stroke/50' : 'text-muted hover:text-text hover:bg-stroke/50'
              }`}>{link}</button>
            ))}
          </div>
          <div className="hidden sm:block w-px h-5 bg-stroke" />
          <button className="relative rounded-full px-3 sm:px-4 py-1.5 sm:py-2 text-xs sm:text-sm text-muted hover:text-text">
            Say hi ↗
          </button>
        </div>
      </nav>
      
      {/* Hero content */}
      <div className="relative z-10 flex flex-col items-center justify-center min-h-screen px-6">
        <span className="text-xs text-muted uppercase tracking-[0.3em] mb-8">COLLECTION '26</span>
        <h1 className="font-display italic text-6xl md:text-8xl lg:text-9xl leading-[0.9] tracking-tight text-text mb-6">
          Michael Smith
        </h1>
        <p className="text-sm md:text-base text-muted max-w-md mb-12">
          Designing seamless digital interactions by focusing on the unique nuances which bring systems to life.
        </p>
        <div className="flex items-center gap-4">
          <button className="btn-primary hover:scale-105">See Works</button>
          <button className="btn-outline hover:scale-105">Reach out...</button>
        </div>
      </div>
    </section>
  );
}
```

---

## 11. Design Principles

### What Portfolio Cosmic Avoids

| Pattern | Why Avoid | Alternative |
|---------|-----------|-------------|
| Warm colors | Breaks the cold, cinematic mood | Cool blue accent only |
| Light mode | Defeats the "cosmic" darkness | Dark mode only |
| Drop shadows | Too "material design" | Border-only depth |
| Rounded at every scale | Too friendly | Consistent 1.5rem radius |
| Multiple accent colors | Visual chaos | One gradient, used sparingly |
| Heavy animations | Distracts from content | Scroll-driven reveals only |

### What Makes It Premium

1. **Name at massive scale** — 9xl with font-display italic is the centerpiece
2. **Loading screen as performance** — turns waiting into entertainment
3. **Bento grid with halftone** — subtle texture adds depth without color
4. **Gradient borders on hover** — the blue accent rewards interaction
5. **Parallax gallery** — scroll-driven depth creates a "wow" moment
6. **Cycling role tags** — "A Creative lives in Chicago" → "A Fullstack lives in Chicago"

---

*Reverse-engineered from motionsites.ai Section #302 (Portfolio Cosmic).*
