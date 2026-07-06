# Komorebi DESIGN.md

> 木漏れ日设计语言 - 用光影的缓慢变化营造自然、宁静、沉浸式的电影感体验

**Origin**: Reverse-engineered from [perfectdays-movie.jp](https://perfectdays-movie.jp/en/)
**Showcase**: [copy-perfectdays.vercel.app](https://copy-perfectdays.vercel.app)

---

## Core Philosophy

1. **自然主义** - 模拟阳光透过树叶的光影效果（木漏れ日）
2. **极简主义** - 黑白为主，极少色彩，大量留白
3. **沉浸式体验** - 小说式滚动，缓慢动画节奏
4. **情感化设计** - 通过光影和节奏传达宁静氛围

---

## 1. Color System

| Role | Value | Usage |
|------|-------|-------|
| Primary | `#000000` | 背景、主文字 |
| Secondary | `#FFFFFF` | 文字、光影粒子 |
| Accent | `#32E85A` | 交互反馈、按钮高亮 |
| Neutral 100 | `#D9D9D9` | 次要文字 |
| Neutral 200 | `#B3B3B3` | 辅助元素 |
| Neutral 300 | `#808080` | 禁用状态 |

### Transparency Scale

```css
:root {
  --opacity-ghost: 0.024;
  --opacity-whisper: 0.05;
  --opacity-subtle: 0.1;
  --opacity-light: 0.2;
  --opacity-medium: 0.3;
  --opacity-heavy: 0.4;
  --opacity-half: 0.5;
  --opacity-strong: 0.6;
  --opacity-solid: 0.7;
}
```

---

## 2. Typography

| Element | Font | Fallback |
|---------|------|----------|
| English Primary | Helvetica Now Text | Helvetica, Neue Haas Grotesk, sans-serif |
| English Medium | HelveticaNowText-Medium | Helvetica, sans-serif |
| Japanese Title | Koburina Gothic | Noto Sans JP, sans-serif |
| Japanese Body | Tsukushi Mincho | Yu Mincho, serif |
| Display | Domaine Text Regular | Times New Roman, serif |

### Letter Spacing

- Headings: `0.5em` (cinematic feel)
- Body: `0.3em` (readability)
- Navigation: `0.1em` (compact)

---

## 3. Spacing System

```css
:root {
  --space-xs: 8px;
  --space-sm: 16px;
  --space-md: 32px;
  --space-lg: 64px;
  --space-xl: 128px;
  --space-2xl: 256px;
}
```

**Layout Pattern**: Full-screen sections (`100vh`) with generous whitespace.

---

## 4. Animation System

### Easing Curves

```css
:root {
  --ease-bounce: cubic-bezier(0.455, 0.03, 0.515, 0.955);
  --ease-emphasize: cubic-bezier(0.165, 0.84, 0.44, 1);
  --ease-smooth: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-natural: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  --ease-quick: cubic-bezier(0.55, 0.085, 0.68, 0.53);
}
```

### Duration Scale

```css
:root {
  --duration-instant: 0.1s;
  --duration-fast: 0.3s;
  --duration-normal: 0.6s;
  --duration-slow: 1.2s;
  --duration-dramatic: 2.4s;
  --duration-cinematic: 8.1s;
}
```

### Komorebi Animation

```css
@keyframes komorebiOpacity {
  0% { opacity: 0.3; }
  50% { opacity: 0.7; }
  100% { opacity: 0.3; }
}

/* 193 independent animations with varying durations: 300ms - 1500ms */
```

---

## 5. Component Patterns

### Full-Screen Section

```html
<section class="section" style="height: 100vh; display: flex; align-items: center; justify-content: center;">
  <h1 class="title">PERFECT DAYS</h1>
</section>
```

### Komorebi Text Effect

```html
<span class="komorebi" data-auto-show>
  <span class="komorebi_item">P</span>
  <span class="komorebi_item">E</span>
  <span class="komorebi_item">R</span>
  <span class="komorebi_item">F</span>
  <span class="komorebi_item">E</span>
  <span class="komorebi_item">C</span>
  <span class="komorebi_item">T</span>
</span>
```

### Hover Effect

```css
.komorebi_hover {
  transition: opacity 0.2s ease-in-out;
}

.komorebi_hover:hover {
  opacity: 0.7;
}
```

---

## 6. Quick Start

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Komorebi Design</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      background: #000;
      color: #fff;
      font-family: 'Helvetica Neue', Arial, sans-serif;
      overflow: hidden;
    }
    
    .section {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    h1 {
      font-size: 4rem;
      font-weight: 300;
      letter-spacing: 0.5em;
      text-transform: uppercase;
    }
    
    .komorebi_item {
      display: inline-block;
      animation: komorebiOpacity 1.5s ease-in-out infinite;
      animation-delay: calc(var(--index) * 0.1s);
    }
    
    @keyframes komorebiOpacity {
      0%, 100% { opacity: 0.3; }
      50% { opacity: 0.7; }
    }
  </style>
</head>
<body>
  <section class="section">
    <h1>
      <span class="komorebi_item" style="--index: 0">P</span>
      <span class="komorebi_item" style="--index: 1">E</span>
      <span class="komorebi_item" style="--index: 2">R</span>
      <span class="komorebi_item" style="--index: 3">F</span>
      <span class="komorebi_item" style="--index: 4">E</span>
      <span class="komorebi_item" style="--index: 5">C</span>
      <span class="komorebi_item" style="--index: 6">T</span>
    </h1>
  </section>
</body>
</html>
```

---

## 7. Use Cases

### Ideal For
- 电影/艺术网站
- 摄影作品集
- 品牌故事页
- 高端产品展示

### Not Ideal For
- 信息密集型网站
- 工具类应用
- 电商网站
- 新闻资讯

---

## License

CC BY 4.0

---

*Design system extracted from Perfect Days official movie site (2024)*
*Created by Wim Wenders and Koji Yakusho*
