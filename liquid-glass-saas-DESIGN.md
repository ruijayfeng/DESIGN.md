# Liquid Glass SaaS DESIGN.md

> A dark SaaS landing page aesthetic built around **liquid glass** glassmorphism, neon-green accents, and cinematic video backgrounds. Originated from the "APEX" revenue growth platform hero.

**Origin**: [motionsites.ai](https://motionsites.ai) — Section #9 "Apex SaaS Hero" / Section #17 "Planet Orbit"
**Showcase**: [liquid-glass-saas.vercel.app](https://liquid-glass-saas-demo-268ykug34-fengk677-2300s-projects.vercel.app)

---

## Core Philosophy

Liquid Glass SaaS lives on **one tension**:

| Axis | Cold | Warm | How |
|------|------|------|-----|
| Background | Deep near-black + purple tint | Warm off-white text | Contrast hierarchy |
| Surface | Barely-visible glass (1% white) | Frosted blur edges | ::before gradient border |
| Accent | Electric green (#87FB89) | Neutral grays (#9A9A9A) | Green for action only |

The result: an interface that feels like **looking through frosted glass at a glowing screen** — premium, mysterious, action-oriented.

---

## 1. Color System

### HSL Tokens (:root)

All colors defined as HSL CSS custom properties following Tailwind CSS variables convention:

| Role | HSL | Hex | Use |
|------|-----|-----|-----|
| `--background` | `260 87% 3%` | `#07050a` | Page background — near-black with faint purple |
| `--foreground` | `40 6% 95%` | `#f0efe9` | Body text — warm off-white, softer than pure white |
| `--hero-heading` | `40 10% 96%` | `#f5f4ed` | Main headline — brightest text on page |
| `--hero-sub` | `40 6% 82%` | `#d6d4c9` | Subheadline — muted warmth |
| `--primary` | `121 95% 76%` | `#87FB89` | **Electric green** — CTA buttons, key accents |
| `--primary-foreground` | `0 0% 5%` | `#0d0d0d` | Text on green buttons |
| `--secondary` | `240 4% 16%` | `#292930` | Card backgrounds, nav elements |
| `--muted` | `240 4% 16%` | `#292930` | Same as secondary, for muted surfaces |
| `--muted-foreground` | `240 5% 65%` | `#a3a3ab` | Secondary body text |
| `--border` | `240 4% 20%` | `#33333a` | Subtle dividers |
| `--ring` | `262 83% 58%` | `#7c3aed` | Focus ring, highlights |
| `--radius` | `0.75rem` | — | Standard border radius (12px) |

### Glass Surface Colors

The liquid-glass effect does not use solid background colors. Instead, it overlays a nearly-invisible layer:

| Property | Value | Effect |
|----------|-------|--------|
| Base fill | `rgba(255,255,255,0.01)` | 1% white — virtually transparent |
| Border highlight (top) | `rgba(255,255,255,0.45)` | Strong light reflection |
| Border highlight (middle) | `rgba(255,255,255,0)` | Transparent gap — creates "glass edge" illusion |
| Border highlight (bottom) | `rgba(255,255,255,0.45)` | Match top reflection |
| Inset shadow | `rgba(255,255,255,0.1)` | Subtle inner glow |

**Key insight**: The glass effect relies entirely on the `::before` pseudo-element's vertical gradient border and a 4px backdrop blur. No solid backgrounds, no drop shadows — pure edge lighting.

---

## 2. Typography

### Single Font Stack

Unlike Pop-Brutalism's four-layer stack, Liquid Glass uses **one clean font** across everything — matching the SaaS product's minimalist branding:

| Layer | Font Stack | Use Case | Weight |
|-------|-----------|----------|--------|
| **All** | `Geist Sans` → `Inter` → `system-ui, sans-serif` | Headlines, body, buttons, labels | 400 / 500 / 600 / 700 |

**Implementation**: `@fontsource/geist-sans` installed, loaded at 400, 500, 600, 700 weights.

**Design intent**:
- Geist Sans is a modern, geometric sans-serif designed by Vercel — neutral enough to not compete with the glass aesthetic
- Tracking is tight (`tracking-tight`) on headings to create a compact, premium feel
- Line height is `1.05` for large headlines — compressed, editorial
- Body text uses `leading-8` — generous for readability over video

---

## 3. The Liquid Glass Formula

Every glass element follows this **exact CSS recipe**:

```css
.liquid-glass {
  /* Barely visible base */
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  
  /* Frosted edge */
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  
  /* No solid border */
  border: none;
  
  /* Subtle inner glow */
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  
  /* Required for gradient border */
  position: relative;
  overflow: hidden;
}

/* Gradient edge — this is what makes it "glass" */
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%,   /* top reflection */
    rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%,     /* gap — creates edge separation */
    rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%,
    rgba(255,255,255,0.45) 100%  /* bottom reflection */
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

### Border Radius Scale

| Token | Value | Use |
|-------|-------|-----|
| Default | `0.75rem` (12px) | Cards, nav container |
| `rounded-3xl` | `1.5rem` (24px) | Navbar pill |
| `rounded-full` | `9999px` | Badge pills, CTA buttons |
| `rounded-xl` | `0.75rem` (12px) | Smaller buttons |
| `rounded-lg` | `0.5rem` (8px) | Icon containers, logo squares |

---

## 4. Component Kit

### Hero CTA Buttons

Two button variants defined via class-variance-authority:

```css
/* Primary — solid green */
.btn-hero {
  background: var(--primary); /* #87FB89 */
  color: var(--primary-foreground); /* #0d0d0d */
  border-radius: 9999px;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: 500;
  transition: background 0.2s;
}
.btn-hero:hover {
  background: hsl(121 95% 76% / 0.9);
}

/* Secondary — glass outline */
.btn-hero-secondary {
  background: transparent;
  border: none;
  color: var(--foreground);
  border-radius: 9999px;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: 400;
}
.btn-hero-secondary:hover {
  background: rgba(255,255,255,0.05);
}
```

### Nav Pill

The top navbar is a horizontal glass container:

```css
.nav-pill {
  max-width: 850px;
  width: 100%;
  border-radius: 1.5rem; /* rounded-3xl */
  padding: 0.5rem;
  /* inherits .liquid-glass base */
}

.nav-link {
  padding: 8px 12px;
  font-size: 16px;
  color: hsl(40 6% 95% / 0.9); /* foreground/90 */
  transition: color 0.2s;
}
.nav-link:hover {
  color: var(--foreground);
}
```

### Announcement Badge

Small pill at the top of the hero:

```css
.badge-pill {
  border-radius: 9999px;
  padding: 4px 12px 4px 20px; /* extra left padding for text */
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  /* inherits .liquid-glass */
}

.badge-chip {
  background: rgba(255,255,255,0.05);
  padding: 2px 12px;
  border-radius: 9999px;
  font-size: 11px;
}
```

### Brand Marquee Item

Each brand in the scrolling logo marquee:

```css
.marquee-brand {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  flex-shrink: 0;
  white-space: nowrap;
}

.marquee-icon {
  width: 24px;
  height: 24px;
  border-radius: 8px;
  /* inherits .liquid-glass */
}

.marquee-letter {
  font-size: 12px;
  font-weight: 700;
  color: hsl(40 6% 95% / 0.7);
}

.marquee-name {
  font-size: 16px;
  font-weight: 600;
  color: var(--foreground);
}
```

---

## 5. Background & Texture System

### Video Background

The entire page is backed by a **full-screen looping video**:

```css
.page-video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}
```

Video is always autoplay, loop, muted, playsInline. Content sits at `z-index: 1` above it.

### Gradient Overlay (Optional)

For contrast when video is too busy:

```css
.video-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    var(--background) 0%,
    transparent 30%,
    transparent 70%,
    var(--background) 100%
  );
  pointer-events: none;
}
```

The vertical gradient fades to solid background at top and bottom, leaving the video visible in the center.

### No Halftone / No Texture

Unlike Pop-Brutalism, Liquid Glass has **zero patterns**. The depth comes entirely from:
1. Video layer underneath
2. Glass surface on top
3. Gradient edge lighting on glass

---

## 6. Animation Catalog

| Name | Effect | Duration | Use |
|------|--------|----------|-----|
| fade-up | `translateY(16px)→0` + opacity `0→1` | 0.6–0.8s | Element entrance (headline, subhead, CTAs) |
| stagger | Same as fade-up, children delayed 0.15s | 0.8s total | Section title + description |
| marquee | `translateX(0%)→translateX(-50%)` | 20s linear infinite | Brand logo loop |
| hover-scale | `scale(1)→1.05` | 0.2s ease | CTA buttons, nav links |
| hover-glass | `background: rgba(255,255,255,0.05)` | 0.2s | Secondary CTA fill on hover |

**Entrance sequence for hero section** (staggered cascade):

1. **0ms**: Badge badge fades in
2. **200ms**: Headline characters animate left-to-right (if using split-text)
3. **400ms**: Subheadline fades up
4. **600ms**: CTA buttons fade up
5. **800ms**: Social proof section fades up

---

## 7. Layout Anatomy

### Three-Section Vertical Stack

| Section | Vertical Position | Content |
|---------|------------------|---------|
| Navbar | Fixed, top, `py-5` | Logo + nav links + Sign Up CTA |
| Hero | `pt-20`, centered | Badge → h1 → sub → 2 CTAs |
| Social Proof | `pt-16 pb-24` | Stats row → spacer → brand marquee |

### Responsive Breakpoints

| Breakpoint | Layout |
|------------|--------|
| `< 640px` (sm) | Single column, full-width nav pill, h1 text-4xl |
| `640–1023px` (md–lg) | h1 text-6xl, nav items visible |
| `≥ 1024px` (xl) | h1 text-7xl, max-w-5xl centered, max nav width 850px |

### Max Widths

| Element | Max Width |
|---------|-----------|
| Navbar container | `850px` |
| Hero heading | `5xl` (80rem / ~1280px) |
| Subheading | `md` (42rem / ~672px) |
| Social proof marquee | `5xl` (80rem) |

---

## 8. Quick Start

### Minimal Copy-Paste

```css
/* 1. Register tokens in :root */
:root {
  --background: hsl(260 87% 3%);
  --foreground: hsl(40 6% 95%);
  --primary: hsl(121 95% 76%);     /* #87FB89 */
  --primary-foreground: hsl(0 0% 5%);
  --secondary: hsl(240 4% 16%);
  --muted-foreground: hsl(240 5% 65%);
  --border: hsl(240 4% 20%);
  --ring: hsl(262 83% 58%);
  --radius: 0.75rem;
}

/* 2. The glass utility */
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}

.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%,
    rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%,
    rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%,
    rgba(255,255,255,0.45) 100%
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}

/* 3. Green CTA button */
.btn-primary {
  background: var(--primary);
  color: var(--primary-foreground);
  border-radius: 9999px;
  padding: 12px 24px;
  font-weight: 500;
}

/* 4. Glass secondary button */
.btn-glass {
  color: var(--foreground);
  border-radius: 9999px;
  padding: 12px 24px;
}
.btn-glass:hover {
  background: rgba(255,255,255,0.05);
}
```

```jsx
// React usage
import './styles.css';

export function Hero() {
  return (
    <section className="relative overflow-hidden" style={{ background: 'var(--background)' }}>
      <video autoPlay loop muted playsInline className="absolute inset-0 w-full h-full object-cover" />
      
      <div className="relative z-10 flex flex-col items-center pt-20 px-4">
        {/* Nav pill */}
        <nav className="liquid-glass rounded-3xl max-w-[850px] w-full py-2 px-3 flex items-center justify-between gap-6">
          <span className="font-semibold text-lg">APEX</span>
          <div className="flex gap-2">
            {['Features', 'Solutions', 'Plans'].map(link => (
              <button key={link} className="text-base text-foreground/90 hover:text-foreground px-3 py-2 transition-colors">{link}</button>
            ))}
          </div>
          <button className="bg-primary text-primary-foreground text-sm px-4 py-2 rounded-xl">Sign Up</button>
        </nav>
        
        {/* Hero content */}
        <div className="flex flex-col items-center mt-20">
          <span className="liquid-glass rounded-full px-3 pr-1 py-1 mb-8 text-xs">
            Nova+ Launched! <span className="bg-white/5 px-3 py-0.5 rounded-full">Explore →</span>
          </span>
          
          <h1 className="text-4xl sm:text-6xl lg:text-7xl font-semibold tracking-tight text-center leading-[1.05] max-w-5xl" style={{ color: 'var(--hero-heading)' }}>
            Accelerate Your<br/>Revenue Growth Now
          </h1>
          
          <p className="text-lg mt-4 max-w-md text-center opacity-80" style={{ color: 'var(--hero-sub)' }}>
            Drive your funnel forward with clever workflows, analytics, and seamless lead management.
          </p>
          
          <div className="flex items-center gap-4 mt-8">
            <button className="btn-primary">Start Free Right Now</button>
            <button className="btn-glass">Schedule a Consult</button>
          </div>
        </div>
      </div>
    </section>
  );
}
```

---

## 9. Brand Mark

The logo mark is a **gradient square with a crosshair SVG** — a circle with four radiating lines (N, S, E, W), all in white strokes. It sits inside a `rounded-lg` container with `bg-gradient-to-b from-secondary to-muted`.

Brand wordmark uses the single font (Geist Sans), text-xl, font-semibold, tracking-tight.

---

*Reverse-engineered from motionsites.ai Sections #9 (Apex SaaS Hero) and #17 (Planet Orbit).*
