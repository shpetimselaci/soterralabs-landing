# Dotted World Map Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace placeholder SVG with a dotted/stippled world map featuring ~120 circles positioned as continent shapes with a subtle pulse animation.

**Architecture:** Pure SVG with `<circle>` elements inline in HTML. CSS `@keyframes` animation for pulse effect with 5 staggered wave classes. No JavaScript required.

**Tech Stack:** HTML, SCSS/Sass, SVG

---

### Task 1: Add Pulse Animation to SCSS

**Files:**
- Modify: `src/styles/main.scss`

**Step 1: Add pulse keyframes animation**

Add after the existing `@keyframes float` block (~line 60):

```scss
// Dot pulse animation
@keyframes pulse {
  0%, 100% {
    opacity: 0.25;
  }
  50% {
    opacity: 0.4;
  }
}
```

**Step 2: Add dot base styles and wave classes**

Add after the `.world-map` block (~line 50):

```scss
// Dotted map styles
.dot {
  animation: pulse 5s ease-in-out infinite;
}

.dot-wave-1 { animation-delay: 0s; }
.dot-wave-2 { animation-delay: 1s; }
.dot-wave-3 { animation-delay: 2s; }
.dot-wave-4 { animation-delay: 3s; }
.dot-wave-5 { animation-delay: 4s; }
```

**Step 3: Verify SCSS compiles**

Run:
```bash
npm run build:css
```

Expected: No errors, `dist/styles.css` updated

**Step 4: Commit**

```bash
git add src/styles/main.scss
git commit -m "feat: add pulse animation for dotted world map"
```

---

### Task 2: Create Dotted World Map SVG - North America

**Files:**
- Modify: `src/index.html`

**Step 1: Replace opening SVG tag and begin circles**

Replace the entire `<div class="world-map">` section with:

```html
<!-- World Map Background -->
<div class="world-map">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMid slice">
        <!-- North America -->
        <circle class="dot dot-wave-1" cx="150" cy="95" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="175" cy="85" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="200" cy="80" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="225" cy="90" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="195" cy="105" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="170" cy="115" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="145" cy="125" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="165" cy="140" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="190" cy="130" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="215" cy="120" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="240" cy="115" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="220" cy="145" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="195" cy="155" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="170" cy="165" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="200" cy="175" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="225" cy="165" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="250" cy="155" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="235" cy="180" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="210" cy="190" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="245" cy="195" r="3" fill="currentColor"/>
```

Note: SVG is not yet closed - will continue in next tasks.

**Step 2: Verify HTML syntax (partial)**

File will be incomplete but structurally valid so far.

---

### Task 3: Add South America Dots

**Files:**
- Modify: `src/index.html`

**Step 1: Add South America circles**

Continue after North America section:

```html
        <!-- South America -->
        <circle class="dot dot-wave-3" cx="280" cy="250" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="295" cy="270" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="285" cy="295" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="275" cy="320" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="290" cy="340" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="280" cy="365" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="270" cy="385" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="260" cy="405" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="275" cy="425" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="265" cy="445" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="255" cy="460" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="300" cy="310" r="3" fill="currentColor"/>
```

---

### Task 4: Add Europe Dots

**Files:**
- Modify: `src/index.html`

**Step 1: Add Europe circles**

Continue after South America section:

```html
        <!-- Europe -->
        <circle class="dot dot-wave-2" cx="480" cy="95" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="500" cy="85" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="520" cy="90" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="495" cy="110" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="515" cy="105" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="535" cy="100" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="505" cy="125" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="525" cy="120" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="485" cy="130" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="545" cy="115" r="4" fill="currentColor"/>
```

---

### Task 5: Add Africa Dots

**Files:**
- Modify: `src/index.html`

**Step 1: Add Africa circles**

Continue after Europe section:

```html
        <!-- Africa -->
        <circle class="dot dot-wave-1" cx="490" cy="180" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="510" cy="175" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="505" cy="200" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="525" cy="195" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="495" cy="225" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="515" cy="220" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="535" cy="215" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="505" cy="250" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="525" cy="245" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="515" cy="275" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="500" cy="295" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="520" cy="300" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="535" cy="285" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="510" cy="320" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="525" cy="335" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="540" cy="310" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="555" cy="265" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="550" cy="240" r="3" fill="currentColor"/>
```

---

### Task 6: Add Asia Dots

**Files:**
- Modify: `src/index.html`

**Step 1: Add Asia circles**

Continue after Africa section:

```html
        <!-- Asia -->
        <circle class="dot dot-wave-4" cx="580" cy="100" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="610" cy="95" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="640" cy="90" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="670" cy="85" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="700" cy="90" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="730" cy="95" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="760" cy="100" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="790" cy="110" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="600" cy="120" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="630" cy="115" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="660" cy="110" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="690" cy="115" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="720" cy="120" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="750" cy="125" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="620" cy="145" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="650" cy="140" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="680" cy="145" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="710" cy="150" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="740" cy="155" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="770" cy="145" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="640" cy="170" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="670" cy="175" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="700" cy="180" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="730" cy="175" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="760" cy="170" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="660" cy="200" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="690" cy="205" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="720" cy="200" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="800" cy="140" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="820" cy="160" r="3" fill="currentColor"/>
```

---

### Task 7: Add Australia and Antarctica Dots

**Files:**
- Modify: `src/index.html`

**Step 1: Add Australia circles**

Continue after Asia section:

```html
        <!-- Australia -->
        <circle class="dot dot-wave-2" cx="780" cy="320" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="810" cy="315" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="800" cy="340" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-3" cx="830" cy="335" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="820" cy="360" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="790" cy="365" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="835" cy="355" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="850" cy="340" r="3" fill="currentColor"/>
```

**Step 2: Add Antarctica hint circles**

Continue:

```html
        <!-- Antarctica (hint) -->
        <circle class="dot dot-wave-3" cx="400" cy="480" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-5" cx="450" cy="485" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-1" cx="500" cy="480" r="3" fill="currentColor"/>
        <circle class="dot dot-wave-2" cx="550" cy="485" r="4" fill="currentColor"/>
        <circle class="dot dot-wave-4" cx="600" cy="480" r="3" fill="currentColor"/>
    </svg>
</div>
```

---

### Task 8: Build, Test, and Deploy

**Files:**
- No file changes

**Step 1: Run full build**

Run:
```bash
npm run build
```

Expected: Build completes without errors

**Step 2: Visual verification**

Open `dist/index.html` in browser and verify:
- Dots form recognizable continent shapes
- Pulse animation is subtle and staggered
- Dots don't interfere with floating blocks or text
- Works on different viewport sizes

**Step 3: Commit all changes**

Run:
```bash
git add src/index.html
git commit -m "feat: implement dotted world map with pulse animation"
```

**Step 4: Deploy to Cloudflare Pages**

Run:
```bash
export $(grep -v '^#' .env | xargs) && npx wrangler pages deploy dist --project-name=soterralabs-landing --commit-dirty=true
```

Expected: Deployment URL returned

---

## Verification Checklist

- [ ] `npm run build` completes without errors
- [ ] ~100-120 dots visible forming continent shapes
- [ ] Pulse animation runs smoothly with staggered timing
- [ ] Dots are subtle (25-40% opacity range)
- [ ] Floating blocks still animate correctly
- [ ] Text remains readable
- [ ] Responsive on mobile
- [ ] Deployed successfully
