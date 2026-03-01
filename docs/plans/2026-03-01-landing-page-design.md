# Soterra Labs Landing Page Design

## Overview

A minimalist landing page for Soterra Labs, a software & hardware research lab. Features a grey world map background with abstract floating white blocks and centered text content.

## Visual Design

### Layout
- Full viewport grey world map as background
- Centered text overlay
- Contact information at bottom

### Color Palette
| Element | Color |
|---------|-------|
| Background | Light grey gradient (`#ffffff` → `#f5f5f5` → `#e8e8e8`) |
| World map | Grey at ~25% opacity (`rgba(120, 120, 120, 0.25)`) |
| Floating blocks | White (`#ffffff`) with subtle shadow |
| Primary text | Dark charcoal (`#1a1a1a`) |
| Secondary text | Lighter charcoal (`#3a3a3a`) |

### Typography
- Font: Inter (Google Fonts)
- "Welcome to Soterra Labs" — large, font-weight 300-400
- "I love you" — medium, font-weight 400
- Contact info — small, subtle

### Floating Blocks
- Count: 10-15 blocks
- Sizes: 20px to 80px (randomized)
- Positions: scattered across viewport (randomized top/left percentages)
- Border-radius: 4-8px for softer look

### Animation
```scss
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
```
- Easing: ease-in-out
- Duration: 3s to 6s per block (randomized)
- Delay: 0s to 5s per block (staggered for organic feel)

## Technical Approach

### Implementation: Pure CSS/SVG with Sass
- SVG world map silhouette embedded in HTML
- Floating blocks as absolutely positioned `<div>` elements
- Sass `@for` loops with `random()` function to generate block positions/sizes/delays at compile time
- CSS `@keyframes` for bobbing animation

### Project Structure
```
soterralabs-landing/
├── src/
│   ├── index.html
│   └── styles/
│       └── main.scss
├── dist/
├── package.json
└── wrangler.toml
```

### Build Process
```json
{
  "scripts": {
    "build:css": "sass src/styles/main.scss dist/styles.css",
    "build": "npm run build:css && cp src/index.html dist/",
    "deploy": "wrangler pages deploy dist"
  }
}
```

### Dependencies
- `sass` (dev dependency) — SCSS compilation
- `wrangler` (dev dependency) — Cloudflare Pages deployment

## Deployment

- Platform: Cloudflare Pages
- Tool: Wrangler CLI
- Command: `wrangler pages deploy dist`

## Content

- Heading: "Welcome to Soterra Labs"
- Subheading: "I love you" (Idiocracy reference)
- Location: Kosovo
- Contact: inquiries@soterralabs.co
