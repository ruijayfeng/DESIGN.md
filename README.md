# Pop-Brutalism DESIGN.md

<br>

<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=ZCOOL+KuaiLe&size=28&duration=3000&pause=1000&color=FFE53D&center=true&vCenter=true&multiline=true&repeat=true&width=500&height=80&lines=Pop-Brutalism;A+Design+Language+Spec)](https://git.io/typing-svg)

<br>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-ff3df4.svg?style=for-the-badge&logo=creativecommons&logoColor=white)](https://creativecommons.org/licenses/by/4.0/)
[![GitHub stars](https://img.shields.io/github/stars/ruijayfeng/DESIGN.md?style=for-the-badge&color=ffe53d&logo=github&logoColor=black)](https://github.com/ruijayfeng/DESIGN.md/stargazers)
[![GitHub last commit](https://img.shields.io/github/last-commit/ruijayfeng/DESIGN.md?style=for-the-badge&color=3dd5ff&logo=github&logoColor=black)](https://github.com/ruijayfeng/DESIGN.md/commits)

<br>

**A design language that fuses Neo-Brutalism's raw physicality with POP art's chromatic energy.**

<br>

[![capsule render](https://capsule-render.vercel.app/api?animation=fadeIn&color=gradient&customColorList=0a0a0f,ff3df4,3dd5ff&section=header&text=Pop-Brutalism&fontSize=50&fontColor=ffe53d&desc=A+design+language+spec&descSize=16&descAlignY=65&type=wave)](https://github.com/kyechan99/capsule-render)

</div>

<br>

## 🎨 What is Pop-Brutalism?

A design system distilled from production CSS — combining:

- **Neo-Brutalism**'s hard shadows, bold outlines, and press-down buttons
- **POP art**'s halftone textures, neon palette, and chromatic energy
- **Paper craft**'s micro-rotations and handmade collage feeling

<br>

<div align="center">

| Layer | Ink | Paper | Neon |
|-------|-----|-------|------|
| **Default** | `#0a0a0f` | `#faf7ee` | Full saturation |
| **Soft** | `#141414` | `#fffefa` | Muted |
| **Glass** | `#2f2e2b` | `rgba(255,255,255,.58)` | Desaturated |

</div>

<br>

## 📐 Core Formula

<br>

```
 Every Pop-Brutalism component:
 ┌─────────────────────────────────────────┐
 │  background:    var(--paper)            │  ← paper base
 │  border:        var(--outline)          │  ← bold outline
 │  box-shadow:    var(--shadow-hard)      │  ← hard offset
 │  border-radius: var(--radius-card)      │  ← rounded
 │  transform:     rotate(var(--rot, 0deg))│  ← micro-rotation
 └─────────────────────────────────────────┘
```

<br>

## 🧩 Components

<br>

<div align="center">

| Component | Purpose | Signature |
|-----------|---------|-----------|
| **Sticker Card** | Content blocks | Hard shadow + color variants |
| **Chip** | Inline tags | `8px 14px` padding, bold |
| **Pill** | Capsule labels | `999px` border-radius |
| **Button** | Actions | Press-down translate feedback |
| **Avatar** | User identity | CSS-drawn minimalist face |
| **Keypoint Card** | Feature highlights | Floating label badge |

</div>

<br>

## 🖌️ Textures (Pure CSS, Zero Images)

<br>

<div align="center">

| Texture | CSS Technique | Result |
|---------|--------------|--------|
| **Halftone** | `radial-gradient` dots | Print effect |
| **Stripe** | `repeating-linear-gradient` 45° | Diagonal lines |
| **Burst** | `repeating-conic-gradient` | Radial fans |
| **Hatch** | Dual 45° cross lines | Hand-drawn shading |

</div>

<br>

## 🔤 Typography Stack

<br>

```
 Display  →  Bowlby One  →  ZCOOL KuaiLe  →  Noto Sans SC
 Cute     →  ZCOOL KuaiLe  →  Bowlby One  →  Noto Sans SC
 Data     →  JetBrains Mono  →  SF Mono  →  Consolas
 Body     →  Noto Sans SC  →  PingFang SC  →  system-ui
```

<br>

## 📂 Files in This Repo

<br>

| File | Description |
|------|-------------|
| [`pop-brutalism-DESIGN.md`](./pop-brutalism-DESIGN.md) | Full spec: colors, components, textures, animations |
| *more coming soon* | Other design languages |

<br>

## 🔗 Links

<br>

<div align="center">

[![Showcase](https://img.shields.io/badge/🎨_Showcase-pop--chroma.vercel.app-0a0a0f?style=for-the-badge&logo=vercel&logoColor=white)](https://pop-chroma.vercel.app)
[![Origin](https://img.shields.io/badge/⭐_Origin-app.ziwei.pro-C74B2A?style=for-the-badge&logo=googlechrome&logoColor=white)](https://app.ziwei.pro)

</div>

<br>

## 📜 License

<br>

This design language specification is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
Use it freely in personal and commercial projects.

<br>

---

<div align="center">

<sub>Reverse-engineered with care from production CSS.</sub>

</div>
