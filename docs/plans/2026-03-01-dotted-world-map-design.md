# Dotted World Map Design

## Overview

Replace the placeholder abstract SVG with a dotted/stippled world map featuring sparse dots and a subtle pulse animation.

## Visual Design

### Style
- **Type:** Dotted/stippled map — world represented by circles
- **Aesthetic:** Modern tech feel, minimalist
- **Density:** Sparse — fewer, larger dots for an airy feel that doesn't compete with content

### Dot Specifications
| Property | Value |
|----------|-------|
| Total dots | ~100-120 |
| Radius | 3-5px (slight variation) |
| Color | `rgba(120, 120, 120, 0.25)` (current `$map-color`) |
| Spacing | ~30-50px between dots |

### Continent Distribution
| Continent | Approximate Dots |
|-----------|------------------|
| North America | ~20 |
| South America | ~12 |
| Europe | ~10 |
| Africa | ~18 |
| Asia | ~30 |
| Australia | ~8 |
| Antarctica (hint) | ~5 |

## Animation

### Pulse Effect
```scss
@keyframes pulse {
  0%, 100% { opacity: 0.25; }
  50% { opacity: 0.4; }
}
```

### Properties
- **Duration:** 4-6 seconds (slow, ambient)
- **Easing:** ease-in-out
- **Staggered delays:** 5 wave groups with 1s offset each
- **Effect:** Opacity only (no transform/scale)

### Wave Classes
- `.dot-wave-1` — delay: 0s
- `.dot-wave-2` — delay: 1s
- `.dot-wave-3` — delay: 2s
- `.dot-wave-4` — delay: 3s
- `.dot-wave-5` — delay: 4s

Dots distributed across waves by geographic region for a rippling effect.

## Technical Approach

### Implementation
- Pure SVG with `<circle>` elements
- CSS `@keyframes` animation
- No JavaScript required

### Files to Modify
- `src/index.html` — Replace SVG path with circle elements
- `src/styles/main.scss` — Add pulse animation and wave classes

### SVG Structure
```svg
<svg viewBox="0 0 1000 500" preserveAspectRatio="xMidYMid slice">
  <circle class="dot dot-wave-1" cx="150" cy="120" r="4" fill="currentColor"/>
  <circle class="dot dot-wave-2" cx="180" cy="135" r="3" fill="currentColor"/>
  <!-- ~120 total circles -->
</svg>
```

### Performance
- CSS animations GPU-accelerated (opacity only)
- Lightweight SVG (~8-12KB)
- No JS dependencies
- Works on all modern browsers

## Integration

- Keeps existing `$map-color` variable
- Same inline SVG approach
- No changes to build process or deployment
- Floating blocks and content styling unchanged
