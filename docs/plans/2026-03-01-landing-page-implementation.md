# Soterra Labs Landing Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a minimalist landing page with a grey world map background, floating white blocks with bobbing animation, and deploy to Cloudflare Pages.

**Architecture:** Static HTML page with SCSS-compiled CSS. Sass `@for` loops generate randomized floating block positions at compile time. SVG world map embedded inline. Deployed via Wrangler CLI to Cloudflare Pages.

**Tech Stack:** HTML, SCSS/Sass, SVG, Cloudflare Pages, Wrangler CLI

---

### Task 1: Initialize Project Structure

**Files:**
- Create: `package.json`
- Create: `wrangler.toml`
- Create: `src/styles/main.scss`
- Move: `index.html` → `src/index.html`

**Step 1: Create package.json**

```json
{
  "name": "soterralabs-landing",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "build:css": "sass src/styles/main.scss dist/styles.css --style=compressed",
    "build": "npm run build:css && mkdir -p dist && cp src/index.html dist/",
    "dev": "sass src/styles/main.scss dist/styles.css --watch",
    "deploy": "npm run build && wrangler pages deploy dist --project-name=soterralabs-landing"
  },
  "devDependencies": {
    "sass": "^1.71.0",
    "wrangler": "^3.28.0"
  }
}
```

**Step 2: Create wrangler.toml**

```toml
name = "soterralabs-landing"
compatibility_date = "2024-01-01"
```

**Step 3: Create directory structure and move index.html**

Run:
```bash
mkdir -p src/styles dist
mv index.html src/index.html
```

**Step 4: Create placeholder main.scss**

```scss
// Soterra Labs Landing Page Styles
// Placeholder - will be populated in Task 3
```

**Step 5: Commit**

```bash
git add package.json wrangler.toml src/
git commit -m "chore: initialize project structure with Sass and Wrangler config"
```

---

### Task 2: Install Dependencies

**Step 1: Install npm packages**

Run:
```bash
npm install
```

Expected: `node_modules/` created, `package-lock.json` generated

**Step 2: Verify sass works**

Run:
```bash
npx sass --version
```

Expected: Version number like `1.71.0`

**Step 3: Verify wrangler works**

Run:
```bash
npx wrangler --version
```

Expected: Version number like `3.28.0`

**Step 4: Add node_modules to gitignore**

Create `.gitignore`:
```
node_modules/
dist/
.wrangler/
```

**Step 5: Commit**

```bash
git add .gitignore package-lock.json
git commit -m "chore: install dependencies and add gitignore"
```

---

### Task 3: Create World Map SVG Asset

**Files:**
- Create: `src/assets/world-map.svg`

**Step 1: Create assets directory**

Run:
```bash
mkdir -p src/assets
```

**Step 2: Create simplified world map SVG**

Create `src/assets/world-map.svg` with a simplified world map silhouette. Use a standard simplified world map path (continents only, no borders).

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMid slice">
  <path fill="currentColor" d="M165,125 Q180,100 220,105 T280,95 Q320,90 350,100 T400,95 Q430,100 450,120 T480,115 Q500,105 520,110 T550,100 L560,95 Q580,90 600,95 T640,90 Q660,95 680,100 L700,105 Q720,115 740,110 T780,120 Q800,130 820,125 L830,130 Q845,140 850,155 T840,180 Q830,200 810,210 T780,230 Q760,245 740,240 T700,250 Q680,260 660,255 T620,265 Q600,275 580,270 T540,280 Q520,290 500,285 T460,295 Q440,305 420,300 T380,310 Q360,315 340,310 T300,315 Q280,310 260,305 T220,310 Q200,305 180,295 T150,285 Q130,275 120,260 T115,235 Q110,215 115,195 T125,165 Q135,145 150,135 T165,125 Z M420,320 Q450,315 480,325 T540,320 Q570,330 590,345 T600,375 Q595,400 575,415 T530,425 Q500,420 475,410 T440,395 Q420,380 415,360 T420,320 Z M700,260 Q730,255 760,265 T810,275 Q840,290 855,315 T860,355 Q850,385 825,405 T775,420 Q745,415 720,400 T690,370 Q680,340 685,310 T700,260 Z M150,320 Q180,310 210,320 T260,330 Q285,345 295,370 T290,410 Q275,435 245,450 T190,455 Q160,445 140,425 T125,385 Q120,355 130,335 T150,320 Z"/>
</svg>
```

Note: This is a simplified placeholder. For production, source a proper simplified world map SVG from a free resource like Natural Earth or SimpleMaps.

**Step 3: Commit**

```bash
git add src/assets/
git commit -m "feat: add world map SVG asset"
```

---

### Task 4: Implement SCSS with Floating Blocks Generator

**Files:**
- Modify: `src/styles/main.scss`

**Step 1: Write SCSS variables and base styles**

```scss
// Variables
$bg-gradient-start: #ffffff;
$bg-gradient-mid: #f5f5f5;
$bg-gradient-end: #e8e8e8;
$map-color: rgba(120, 120, 120, 0.25);
$block-color: #ffffff;
$text-primary: #1a1a1a;
$text-secondary: #3a3a3a;

// Block generation config
$block-count: 12;
$block-min-size: 20px;
$block-max-size: 80px;

// Reset
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

// Body
body {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, $bg-gradient-start 0%, $bg-gradient-mid 50%, $bg-gradient-end 100%);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  overflow: hidden;
  position: relative;
}
```

**Step 2: Add world map background styles**

```scss
// World map background
.world-map {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;

  svg {
    width: 100%;
    height: 100%;
    color: $map-color;
  }
}
```

**Step 3: Add floating block animation**

```scss
// Floating animation
@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

// Blocks container
.floating-blocks {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  pointer-events: none;
}

// Individual block base
.block {
  position: absolute;
  background: $block-color;
  border-radius: 6px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  animation: float ease-in-out infinite;
}
```

**Step 4: Add Sass @for loop to generate randomized blocks**

```scss
// Generate randomized blocks
@for $i from 1 through $block-count {
  .block-#{$i} {
    // Random size between min and max
    $size: random($block-max-size - $block-min-size) + $block-min-size;
    width: #{$size}px;
    height: #{$size}px;

    // Random position (avoiding edges)
    top: #{random(80) + 5}%;
    left: #{random(85) + 5}%;

    // Random animation duration (3-6s) and delay (0-5s)
    animation-duration: #{random(3) + 3}s;
    animation-delay: #{random(5)}s;

    // Slight opacity variation
    opacity: #{0.7 + random(3) * 0.1};
  }
}
```

**Step 5: Add content styles**

```scss
// Content container
.container {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 2rem;
}

// Typography
.greeting {
  font-size: clamp(2rem, 8vw, 4.5rem);
  font-weight: 300;
  color: $text-primary;
  letter-spacing: 0.02em;
  margin-bottom: 0.2em;
}

.love {
  font-size: clamp(1.2rem, 4vw, 2.5rem);
  font-weight: 400;
  color: $text-secondary;
  letter-spacing: 0.05em;
  margin-bottom: 4rem;
}

// Contact section
.contact {
  margin-top: 2rem;

  p {
    font-size: clamp(0.85rem, 2vw, 1rem);
    font-weight: 400;
    color: $text-secondary;
    letter-spacing: 0.03em;
    margin: 0.5em 0;
  }

  a {
    color: $text-secondary;
    text-decoration: none;
    transition: color 0.3s ease;

    &:hover {
      color: $text-primary;
    }
  }
}
```

**Step 6: Verify SCSS compiles**

Run:
```bash
npm run build:css
```

Expected: `dist/styles.css` created without errors

**Step 7: Commit**

```bash
git add src/styles/main.scss
git commit -m "feat: implement SCSS with floating blocks generator"
```

---

### Task 5: Update HTML Structure

**Files:**
- Modify: `src/index.html`

**Step 1: Update index.html with new structure**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Soterra Labs</title>
    <meta name="description" content="Soterra Labs - Software & Hardware Research">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- World Map Background -->
    <div class="world-map">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMid slice">
            <path fill="currentColor" d="M165,125 Q180,100 220,105 T280,95 Q320,90 350,100 T400,95 Q430,100 450,120 T480,115 Q500,105 520,110 T550,100 L560,95 Q580,90 600,95 T640,90 Q660,95 680,100 L700,105 Q720,115 740,110 T780,120 Q800,130 820,125 L830,130 Q845,140 850,155 T840,180 Q830,200 810,210 T780,230 Q760,245 740,240 T700,250 Q680,260 660,255 T620,265 Q600,275 580,270 T540,280 Q520,290 500,285 T460,295 Q440,305 420,300 T380,310 Q360,315 340,310 T300,315 Q280,310 260,305 T220,310 Q200,305 180,295 T150,285 Q130,275 120,260 T115,235 Q110,215 115,195 T125,165 Q135,145 150,135 T165,125 Z M420,320 Q450,315 480,325 T540,320 Q570,330 590,345 T600,375 Q595,400 575,415 T530,425 Q500,420 475,410 T440,395 Q420,380 415,360 T420,320 Z M700,260 Q730,255 760,265 T810,275 Q840,290 855,315 T860,355 Q850,385 825,405 T775,420 Q745,415 720,400 T690,370 Q680,340 685,310 T700,260 Z M150,320 Q180,310 210,320 T260,330 Q285,345 295,370 T290,410 Q275,435 245,450 T190,455 Q160,445 140,425 T125,385 Q120,355 130,335 T150,320 Z"/>
        </svg>
    </div>

    <!-- Floating Blocks -->
    <div class="floating-blocks">
        <div class="block block-1"></div>
        <div class="block block-2"></div>
        <div class="block block-3"></div>
        <div class="block block-4"></div>
        <div class="block block-5"></div>
        <div class="block block-6"></div>
        <div class="block block-7"></div>
        <div class="block block-8"></div>
        <div class="block block-9"></div>
        <div class="block block-10"></div>
        <div class="block block-11"></div>
        <div class="block block-12"></div>
    </div>

    <!-- Content -->
    <div class="container">
        <h1 class="greeting">Welcome to Soterra Labs</h1>
        <p class="love">I love you</p>

        <div class="contact">
            <p>Kosovo</p>
            <p><a href="mailto:inquiries@soterralabs.co">inquiries@soterralabs.co</a></p>
        </div>
    </div>
</body>
</html>
```

**Step 2: Run full build**

Run:
```bash
npm run build
```

Expected: `dist/` contains `index.html` and `styles.css`

**Step 3: Verify HTML in browser (optional)**

Run:
```bash
open dist/index.html
```

Or serve locally if needed.

**Step 4: Commit**

```bash
git add src/index.html
git commit -m "feat: update HTML with world map and floating blocks structure"
```

---

### Task 6: Source Better World Map SVG (Optional Enhancement)

**Context:** The placeholder SVG is simplified. For a more realistic map, source a proper SVG.

**Step 1: Find a suitable world map**

Options:
- Natural Earth simplified world: https://www.naturalearthdata.com/
- SimpleMaps world: https://simplemaps.com/resources/svg-world
- Or use an SVG optimizer on a detailed map

**Step 2: Replace SVG path in both files**

Update the `<path>` in:
- `src/assets/world-map.svg`
- `src/index.html`

**Step 3: Test build and visual**

Run:
```bash
npm run build
```

**Step 4: Commit if changed**

```bash
git add src/
git commit -m "feat: update world map SVG with improved silhouette"
```

---

### Task 7: Deploy to Cloudflare Pages

**Step 1: Login to Cloudflare (if not already)**

Run:
```bash
npx wrangler login
```

Expected: Browser opens for authentication

**Step 2: Deploy to Cloudflare Pages**

Run:
```bash
npm run deploy
```

Expected: Output shows deployment URL like `https://soterralabs-landing.pages.dev`

**Step 3: Verify live site**

Open the deployment URL in browser. Verify:
- World map visible as grey background
- White blocks floating with animation
- Text centered and readable in dark charcoal
- Contact info visible
- Responsive on mobile

**Step 4: Commit any final adjustments**

```bash
git add .
git commit -m "chore: finalize for production deployment"
```

---

## Verification Checklist

- [ ] `npm run build` completes without errors
- [ ] `dist/` contains `index.html` and `styles.css`
- [ ] Floating blocks animate with staggered timing
- [ ] World map visible as subtle grey background
- [ ] Text is dark charcoal and readable
- [ ] Page is responsive
- [ ] Deployed to Cloudflare Pages successfully
