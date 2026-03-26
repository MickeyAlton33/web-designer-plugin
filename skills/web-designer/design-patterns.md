# Design Patterns Library

Battle-tested CSS and layout patterns extracted from 38 award-winning websites. These are not theoretical -- they are actual techniques used by SVZ Design, Chiara Luzzana, Michael Kors Collection, April Ford, VOUS Church, Superlist, Hardgraft, Daylight, and others recognized as the best-designed sites of 2025-2026.

## Layout Patterns

### 1. Full-Bleed Alternating Sections
Create visual rhythm by alternating between full-width and contained sections.

```css
.section-full {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  padding: var(--space-3xl) 0;
}
.section-contained {
  max-width: 75rem;
  margin: 0 auto;
  padding: var(--space-3xl) var(--space-m);
}
```

### 2. The Museum Frame Modal
Instead of true fullscreen, leave a thin border of background visible. Creates a sense of framing and sophistication (from Michael Kors Collection).

```css
.modal-frame {
  width: calc(100vw - 2.5rem);
  max-height: calc(100vh - 2.5rem);
  margin: 1.25rem auto;
  overflow: hidden;
}
```

### 3. Asymmetric Grid
Break the uniform grid with varied column spans.

```css
.grid-asymmetric {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: var(--space-m);
}
.grid-asymmetric > :nth-child(3n+1) { grid-column: span 7; }
.grid-asymmetric > :nth-child(3n+2) { grid-column: span 5; }
.grid-asymmetric > :nth-child(3n+3) { grid-column: span 12; }
```

### 4. Offset Two-Column
Content and image offset vertically for visual tension.

```css
.offset-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-xl);
  align-items: start;
}
.offset-grid > :nth-child(even) {
  transform: translateY(var(--space-2xl));
}
```

### 5. Single-Column Focused
For long-form content or when typography is the hero. Generous measure for readability.

```css
.content-column {
  max-width: 42rem; /* ~65-75 characters per line */
  margin: 0 auto;
  padding: var(--space-3xl) var(--space-m);
}
```

### 6. Horizontal Scroll Section
Break vertical monotony with a horizontal scroll showcase (from VOUS Church, Superlist).

```css
.horizontal-scroll {
  display: flex;
  gap: var(--space-m);
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  -webkit-overflow-scrolling: touch;
  cursor: grab;
  padding: var(--space-m);
}
.horizontal-scroll::-webkit-scrollbar { display: none; }
.horizontal-scroll > * {
  flex: 0 0 clamp(280px, 35vw, 450px);
  scroll-snap-align: start;
}
.horizontal-scroll:active { cursor: grabbing; }
```

## Card Patterns

### 7. The Hovering Card
Subtle lift on hover with fluid border-radius.

```css
.card {
  border-radius: clamp(0.5rem, 1vw, 1rem);
  transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1),
              box-shadow 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.card:hover {
  transform: translateY(-0.5rem);
  box-shadow: 0 2rem 4rem -1rem rgba(0, 0, 0, 0.15);
}
```

### 8. The 3D Tilt Card (from SVZ Design)
Cards rotate on X/Y axes based on cursor position. Requires JS.

```css
.card-3d {
  perspective: 1000px;
  transform-style: preserve-3d;
}
.card-3d-inner {
  transition: transform 0.15s ease-out;
  will-change: transform;
}
```
```js
// Apply to card container
card.addEventListener('mousemove', (e) => {
  const rect = card.getBoundingClientRect();
  const x = (e.clientX - rect.left) / rect.width - 0.5;
  const y = (e.clientY - rect.top) / rect.height - 0.5;
  inner.style.transform = `rotateY(${x * 15}deg) rotateX(${-y * 15}deg)`;
});
card.addEventListener('mouseleave', () => {
  inner.style.transform = 'rotateY(0) rotateX(0)';
});
```

### 9. The Frosted Glass Card (from SVZ Design)
Glass morphism done right -- subtle blur, not overdone.

```css
.card-glass {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: clamp(0.5rem, 1vw, 1rem);
}
```

### 10. Product Cards with Unique Backgrounds (from Magic Spoon, Snacklins)
Each product gets its own background color, creating a vibrant grid.

```css
.product-card {
  padding: var(--space-l);
  border-radius: clamp(0.75rem, 1.5vw, 1.5rem);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.product-card:nth-child(1) { background: #fef3e2; }
.product-card:nth-child(2) { background: #e8f4f8; }
.product-card:nth-child(3) { background: #f3e8f9; }
.product-card:nth-child(4) { background: #e8f8e9; }
```

## Navigation Patterns

### 11. The Directional Underline (from Chiara Luzzana)
Underline enters from left on hover, exits to right on unhover.

```css
.nav-link {
  position: relative;
  text-decoration: none;
}
.nav-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 100%;
  height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: bottom right;
  transition: transform 0.35s ease;
}
.nav-link:hover::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}
```

### 12. The Text-Slide Button (from April Ford)
On hover, text slides up and is replaced by duplicate text from below.

```css
.btn-slide {
  overflow: hidden;
  position: relative;
}
.btn-slide span {
  display: block;
  transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.btn-slide::after {
  content: attr(data-text);
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  text-align: center;
  transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.btn-slide:hover span { transform: translateY(-100%); }
.btn-slide:hover::after { transform: translateY(-100%); }
```

### 13. Frosted Navigation Bar (from Michael Kors)
```css
.nav-frosted {
  position: fixed;
  top: 0;
  width: 100%;
  backdrop-filter: blur(0.625rem);
  -webkit-backdrop-filter: blur(0.625rem);
  background: rgba(255, 255, 255, 0.8);
  z-index: 100;
}
/* Dark variant */
.nav-frosted--dark {
  background: rgba(0, 0, 0, 0.6);
  color: white;
}
```

## Section Patterns

### 14. The Scroll-Snap Showcase
Full-viewport sections that snap into place, creating a "slide" experience.

```css
.snap-container {
  height: 100vh;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
}
.snap-section {
  height: 100vh;
  scroll-snap-align: start;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### 15. The Alternating Dark/Light Rhythm
Create visual cadence by alternating section backgrounds.

```css
.section { padding: var(--space-3xl) var(--space-m); }
.section--dark {
  background: var(--color-surface-dark);
  color: var(--color-text-on-dark);
}
.section--light {
  background: var(--color-surface-light);
  color: var(--color-text-primary);
}
.section--accent {
  background: var(--color-brand);
  color: var(--color-text-on-brand);
}
```

### 16. The Split Hero
Hero section with content on one side and media on the other, breaking from center-aligned convention.

```css
.hero-split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 100vh;
  align-items: center;
}
.hero-split__content {
  padding: var(--space-2xl);
}
.hero-split__media {
  height: 100%;
  overflow: hidden;
}
.hero-split__media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
@media (max-width: 768px) {
  .hero-split {
    grid-template-columns: 1fr;
    min-height: auto;
  }
}
```

## Text Effects

### 17. Outlined / Stroked Text (from VOUS Church, Chiara Luzzana)
Hollow text that lets the background show through.

```css
.text-outlined {
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke-width: 1.5px;
  -webkit-text-stroke-color: currentColor;
  font-weight: 700;
}
@media (max-width: 480px) {
  .text-outlined {
    -webkit-text-stroke-width: 0.8px;
  }
}
```

### 18. Mix-Blend Legible Text (from April Ford)
Text that inverts against any background, always readable.

```css
.text-blend {
  mix-blend-mode: difference;
  color: white;
  position: relative;
  z-index: 2;
}
```

### 19. The Text Shadow Reveal (from SVZ Design)
Text appears to slide up from behind a colored band during scroll.

```css
.text-reveal {
  overflow: hidden;
}
.text-reveal span {
  display: inline-block;
  transform: translateY(100%);
  transition: transform 0.8s cubic-bezier(0.23, 1, 0.32, 1);
}
.text-reveal.visible span {
  transform: translateY(0);
}
```

## Utility Patterns

### 20. Hidden Scrollbar (cross-browser)
```css
.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.no-scrollbar::-webkit-scrollbar { display: none; }
```

### 21. Non-Interactive Decorative Layer
```css
.decorative {
  pointer-events: none;
  user-select: none;
  -webkit-user-select: none;
}
```

### 22. Scroll-Lock Without Layout Shift
```js
function lockScroll() {
  const scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;
  document.body.style.paddingRight = scrollbarWidth + 'px';
  document.body.style.overflow = 'hidden';
}
function unlockScroll() {
  document.body.style.paddingRight = '';
  document.body.style.overflow = '';
}
```

### 23. Fluid Border Radius (from SVZ Design)
Corners that scale proportionally with the viewport.

```css
.fluid-radius {
  border-radius: clamp(0.5rem, 1vw, 1.5rem);
}
```

### 24. Reduced Motion Respect
Always wrap animations with motion preference queries.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

## Advanced Patterns (from award-winning sites)

### 25. Two-Tone Split Headings (from Superlist)
Key message in white, supporting detail in muted gray within the same heading.

```css
.heading-bright { color: #ffffff; }
.heading-muted { color: #696F81; }
/* Usage: <h2><span class="heading-bright">Bold claim.</span> <span class="heading-muted">Supporting detail here.</span></h2> */
```

### 26. Wide-Gamut P3 Accent Colors (from Superlist)
Use Display P3 color space for more vivid accents on modern screens, with sRGB fallback.

```css
.cta {
  background: rgb(255, 74, 54); /* sRGB fallback */
  background: color(display-p3 0.97 0.31 0.22); /* P3 wide-gamut */
}
```

### 27. Inset Light Highlight on Buttons (from Superlist)
A half-pixel white inset shadow simulates physical light reflection on glossy surfaces.

```css
.btn-glossy {
  box-shadow:
    rgba(0, 0, 0, 0.1) 0px 1px 1px 0px,
    rgba(0, 0, 0, 0.05) 0px 2px 4px 0px,
    rgba(255, 255, 255, 0.45) 0px 0.5px 0px 0px inset;
}
```

### 28. Torn Paper / Organic Edge Divider (from De La Calle)
Break geometric monotony with an organic edge between sections.

```css
.section-organic-edge {
  position: relative;
}
.section-organic-edge::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  right: 0;
  height: 80px;
  background: url('data:image/svg+xml,...') repeat-x bottom;
  background-size: 100% 100%;
  pointer-events: none;
}
```

### 29. Sharp-Corner Brutalist Cards (from De La Calle)
Zero border-radius + visible borders for a bold, editorial/zine-inspired feel.

```css
.card-brutalist {
  border: 2px solid var(--color-accent);
  border-radius: 0;
  background: transparent;
}
.btn-brutalist {
  border-radius: 0;
  border: 2px solid currentColor;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}
```

### 30. Giant Compressed Hero Text (from DONUTS)
Treat display text as a graphic element, not a heading.

```css
.hero-giant {
  font-size: clamp(5rem, 16vw, 15rem);
  font-weight: 800;
  letter-spacing: -0.045em;
  line-height: 0.8;
  text-transform: uppercase;
}
```

### 31. Floating Overlapping Product Images (from DONUTS)
Product images break section boundaries for a magazine-like depth effect.

```css
.section-overlap {
  position: relative;
  overflow: visible; /* allows children to overlap into adjacent sections */
}
.floating-product {
  position: absolute;
  z-index: 10;
  top: -80px;
  right: -40px;
  pointer-events: none;
}
```

### 32. Clip-Path Page Transitions (from 207ouest)
Full-screen wipe transitions between pages using clip-path.

```css
.page-wipe {
  position: fixed;
  inset: 0;
  z-index: 10000;
  background: var(--color-accent);
  transition: clip-path 0.4s cubic-bezier(0.215, 0.61, 0.355, 1);
}
```

### 33. Staggered Menu Cascade (from 207ouest)
Menu items enter with incrementally delayed transforms -- 25ms between each.

```css
.menu-item {
  transform: translateY(1rem);
  opacity: 0;
  transition: transform 0.4s cubic-bezier(0.215, 0.61, 0.355, 1),
              opacity 0.4s ease;
}
.menu-open .menu-item:nth-child(1) { transition-delay: 0s; }
.menu-open .menu-item:nth-child(2) { transition-delay: 0.025s; }
.menu-open .menu-item:nth-child(3) { transition-delay: 0.05s; }
.menu-open .menu-item:nth-child(4) { transition-delay: 0.075s; }
.menu-open .menu-item:nth-child(5) { transition-delay: 0.1s; }
.menu-open .menu-item { transform: translateY(0); opacity: 1; }
```

### 34. 3D Physical Button System (from Pierre-Louis Labonne)
Buttons with visible depth that depress on click.

```css
.btn-3d {
  position: relative;
  transform: translateY(0);
  box-shadow: 0 0.5em 0 var(--btn-shadow-color);
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.btn-3d:hover {
  transform: translateY(0.25em);
  box-shadow: 0 0.25em 0 var(--btn-shadow-color);
}
.btn-3d:active {
  transform: translateY(0.5em);
  box-shadow: none;
}
```

### 35. Sticky-Scroll Scene Architecture (from The Goonies)
Create cinematic scroll sequences where content transforms within a fixed frame.

```css
.scroll-scene {
  height: 200vh; /* scroll runway */
  position: relative;
}
.scroll-scene__sticky {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
}
/* Content inside is animated based on scroll position via JS */
```

### 36. Infinite Logo Ticker with Fade Masks (from Superlist)
Seamlessly scrolling logo bar with faded edges.

```css
.logo-ticker {
  overflow: hidden;
  mask-image: linear-gradient(90deg, transparent 0%, black 10%, black 90%, transparent 100%);
  -webkit-mask-image: linear-gradient(90deg, transparent 0%, black 10%, black 90%, transparent 100%);
}
.logo-ticker__track {
  display: flex;
  animation: ticker 30s linear infinite;
  width: max-content;
}
@keyframes ticker {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}
/* Duplicate content inside track for seamless loop */
```

### 37. Asymmetric Section Spacing (from Hardgraft)
Heavier bottom padding creates visual "weight" and a settled, grounded feel.

```css
.section-weighted {
  padding-top: var(--space-l);
  padding-bottom: var(--space-2xl); /* 2:1 bottom-heavy ratio */
}
```

### 38. Viewport-Relative Spacing Scale (from Daylight)
Spacing that breathes proportionally with the viewport.

```css
:root {
  --space-vw-xs: 1vw;
  --space-vw-s: 2vw;
  --space-vw-m: 4vw;
  --space-vw-l: 6vw;
  --space-vw-xl: 8vw;
}
```

### 39. Noise/Grain Texture Overlay
Adds analog depth and warmth to flat backgrounds.

```css
.grain-overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.05'/%3E%3C/svg%3E");
  pointer-events: none;
  opacity: 0.4;
  mix-blend-mode: overlay;
}
```

---

## 3D & Immersive Patterns

These techniques add physical depth and dimensionality. Use them intentionally -- 3D should serve the content, not distract from it.

### 40. CSS 3D Card Tilt on Hover (from SVZ Design)
Cards rotate in 3D space following the cursor, creating a physical, tactile feel.

```css
.card-3d-container {
  perspective: 1000px;
}
.card-3d {
  transition: transform 0.15s ease-out;
  transform-style: preserve-3d;
  will-change: transform;
}
```
```js
document.querySelectorAll('.card-3d-container').forEach(container => {
  const card = container.querySelector('.card-3d');
  container.addEventListener('mousemove', (e) => {
    const rect = container.getBoundingClientRect();
    const x = (e.clientX - rect.left) / rect.width - 0.5;
    const y = (e.clientY - rect.top) / rect.height - 0.5;
    card.style.transform = `rotateY(${x * 20}deg) rotateX(${-y * 20}deg)`;
  });
  container.addEventListener('mouseleave', () => {
    card.style.transform = 'rotateY(0) rotateX(0)';
  });
});
```

### 41. 3D Perspective Text Reveal (from Daylight Computer)
Text enters from 3D space -- letters rotate into view with perspective depth.

```css
.perspective-container {
  perspective: 2000px;
}
.char-3d {
  display: inline-block;
  transform: rotateX(-90deg);
  transform-origin: bottom center;
  opacity: 0;
  transition: transform 0.8s cubic-bezier(0.23, 1, 0.32, 1),
              opacity 0.6s ease;
}
.char-3d.visible {
  transform: rotateX(0);
  opacity: 1;
}
/* Stagger each character */
.char-3d:nth-child(1) { transition-delay: 0ms; }
.char-3d:nth-child(2) { transition-delay: 40ms; }
.char-3d:nth-child(3) { transition-delay: 80ms; }
/* ... */
```

### 42. Isometric Grid / 3D Product Showcase
Present products or cards on a 3D-tilted plane for a showroom feel.

```css
.isometric-grid {
  transform: rotateX(55deg) rotateZ(-45deg);
  transform-style: preserve-3d;
}
.isometric-grid > * {
  transform: translateZ(0);
  transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.isometric-grid > *:hover {
  transform: translateZ(3rem);
  box-shadow: 0 2rem 4rem rgba(0, 0, 0, 0.3);
}
```

### 43. CSS 3D Flip Card
Two-sided card that flips on hover to reveal different content.

```css
.flip-card {
  perspective: 1000px;
  width: 300px;
  height: 400px;
}
.flip-card__inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  transform-style: preserve-3d;
}
.flip-card:hover .flip-card__inner {
  transform: rotateY(180deg);
}
.flip-card__front,
.flip-card__back {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  border-radius: clamp(0.5rem, 1vw, 1rem);
}
.flip-card__back {
  transform: rotateY(180deg);
}
```

### 44. 3D Layered Parallax Depth (from SVZ, The Goonies)
Multiple layers at different Z-depths create a true parallax diorama effect.

```css
.parallax-scene {
  perspective: 1200px;
  height: 100vh;
  overflow: hidden;
  position: relative;
}
.parallax-layer {
  position: absolute;
  inset: -20%;
  will-change: transform;
}
.parallax-layer--back {
  transform: translateZ(-300px) scale(1.3);
}
.parallax-layer--mid {
  transform: translateZ(-150px) scale(1.15);
}
.parallax-layer--front {
  transform: translateZ(0);
}
```
```js
// Mouse-driven parallax
document.querySelector('.parallax-scene').addEventListener('mousemove', (e) => {
  const x = (e.clientX / window.innerWidth - 0.5) * 2;
  const y = (e.clientY / window.innerHeight - 0.5) * 2;
  document.querySelectorAll('.parallax-layer').forEach(layer => {
    const depth = parseFloat(layer.dataset.depth || 1);
    layer.style.transform = `translate(${x * depth * 20}px, ${y * depth * 20}px)`;
  });
});
```

### 45. 3D Button Press with Depth Shadow (from Pierre-Louis Labonne)
Physical buttons with visible thickness that depress when clicked.

```css
.btn-physical {
  --shadow-color: color-mix(in srgb, var(--btn-color) 70%, black);
  background: var(--btn-color);
  border: none;
  border-radius: 0.5em;
  padding: 0.75em 1.5em;
  transform: translateY(0);
  box-shadow: 0 0.4em 0 var(--shadow-color);
  transition: transform 0.1s ease, box-shadow 0.1s ease;
  cursor: pointer;
}
.btn-physical:hover {
  transform: translateY(0.2em);
  box-shadow: 0 0.2em 0 var(--shadow-color);
}
.btn-physical:active {
  transform: translateY(0.4em);
  box-shadow: none;
  filter: brightness(0.9);
}
```

### 46. CSS 3D Rotating Showcase
A rotating carousel of items in 3D space.

```css
.showcase-3d {
  perspective: 1200px;
  width: 300px;
  height: 400px;
  margin: 0 auto;
}
.showcase-3d__track {
  width: 100%;
  height: 100%;
  position: relative;
  transform-style: preserve-3d;
  animation: rotate3d 20s linear infinite;
}
.showcase-3d__item {
  position: absolute;
  width: 250px;
  height: 350px;
  backface-visibility: hidden;
}
.showcase-3d__item:nth-child(1) { transform: rotateY(0deg) translateZ(350px); }
.showcase-3d__item:nth-child(2) { transform: rotateY(60deg) translateZ(350px); }
.showcase-3d__item:nth-child(3) { transform: rotateY(120deg) translateZ(350px); }
.showcase-3d__item:nth-child(4) { transform: rotateY(180deg) translateZ(350px); }
.showcase-3d__item:nth-child(5) { transform: rotateY(240deg) translateZ(350px); }
.showcase-3d__item:nth-child(6) { transform: rotateY(300deg) translateZ(350px); }

@keyframes rotate3d {
  from { transform: rotateY(0deg); }
  to { transform: rotateY(360deg); }
}
```

### 47. Frosted Glass with 3D Depth (from SVZ, Ready)
Glass cards that float above the background with blur and subtle 3D transform.

```css
.glass-3d {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: clamp(0.5rem, 1vw, 1rem);
  box-shadow:
    0 1.5rem 3rem -0.75rem rgba(0, 0, 0, 0.25),
    inset 0 0.5px 0 rgba(255, 255, 255, 0.1);
  transform: translateZ(0);
  transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1),
              box-shadow 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.glass-3d:hover {
  transform: translateY(-4px) translateZ(0);
  box-shadow:
    0 2.5rem 5rem -1rem rgba(0, 0, 0, 0.3),
    inset 0 0.5px 0 rgba(255, 255, 255, 0.15);
}
```

### 48. Ambient 3D Glow / Radiance (from Superlist)
A subtle radial glow behind hero elements creating atmospheric depth.

```css
.hero-glow {
  position: absolute;
  top: -200px;
  left: 50%;
  transform: translateX(-50%);
  width: 120%;
  height: 600px;
  background: radial-gradient(
    ellipse at center,
    rgba(var(--accent-rgb), 0.15) 0%,
    transparent 60%
  );
  pointer-events: none;
  z-index: -1;
}
```

### When to Use 3D

| Scenario | Technique | Why |
|---|---|---|
| Product showcase | 3D card tilt, rotating carousel | Makes products feel tangible |
| Portfolio | Parallax layers, perspective text | Creates immersion and drama |
| Landing page hero | Ambient glow, 3D text reveal | Draws attention without distraction |
| Interactive cards | Flip cards, glass-3D hover | Rewards exploration |
| Playful/creative brand | Physical buttons, isometric grid | Adds personality and delight |
| Luxury/editorial | Subtle tilt only, parallax depth | Restrained depth signals premium |

**3D Don'ts:**
- Don't use 3D transforms on mobile -- performance varies wildly
- Don't combine multiple 3D effects in the same viewport -- pick one
- Don't use 3D on text-heavy content -- it hurts readability
- Always include `@media (prefers-reduced-motion: reduce)` fallbacks
- Wrap 3D hover effects in `@media (hover: hover)` to prevent sticky states on touch
