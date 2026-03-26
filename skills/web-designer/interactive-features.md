# Interactive Features Playbook

Advanced interaction patterns discovered through live browser analysis of award-winning sites. These go beyond CSS animations into truly interactive, stateful experiences.

## Sound Design for the Web

Sound is the most underused design dimension on the web. When done right, it transforms a visual experience into a sensory one.

### Audio Feedback System (from Pierre-Louis Labonne)
Pierre-Louis uses **69 audio elements** with 3 distinct sound types triggered by CSS class:

```js
// Sound system: play audio on interaction via class detection
const sounds = {
  click: new Audio('click.mp3'),
  punch: new Audio('punch.mp3'),
  toggle: new Audio('toggle.mp3')
};

// Pre-load and set volume
Object.values(sounds).forEach(s => { s.volume = 0.3; s.load(); });

// Attach to elements by class
document.querySelectorAll('.is--click-sound').forEach(el => {
  el.addEventListener('click', () => sounds.click.cloneNode().play());
});
document.querySelectorAll('.is--punch-sound').forEach(el => {
  el.addEventListener('click', () => sounds.punch.cloneNode().play());
});
document.querySelectorAll('.is--toggl-sound').forEach(el => {
  el.addEventListener('click', () => sounds.toggle.cloneNode().play());
});
```

**Rules:**
- Always provide a visible mute/unmute toggle
- Default to muted -- never autoplay audio
- Keep sounds short (<200ms for clicks, <500ms for transitions)
- Use `cloneNode().play()` to allow overlapping sounds
- Fade audio with GSAP: `gsap.to(audio, { volume: 0, duration: 0.5 })`

### Sound Wave Visualizer (from Chiara Luzzana)
A canvas-drawn sine wave that responds to audio playback state.

```js
const canvas = document.querySelector('.visualizer');
const ctx = canvas.getContext('2d');
let amplitude = 3; // resting state

function drawWave() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.beginPath();
  ctx.strokeStyle = '#e5e3dc';
  ctx.lineWidth = 1;

  for (let x = 0; x < canvas.width; x++) {
    const y = canvas.height / 2 +
      Math.sin(x * 0.02 + Date.now() * 0.003) * amplitude +
      Math.sin(x * 0.01 + Date.now() * 0.002) * amplitude * 0.5;
    x === 0 ? ctx.moveTo(x, y) : ctx.lineTo(x, y);
  }
  ctx.stroke();
  requestAnimationFrame(drawWave);
}
drawWave();

// When audio plays, tween amplitude up
function activateWave() {
  gsap.to(window, { duration: 0.5, amplitude: 30, onUpdate: () => {} });
}
```

---

## Canvas-Driven UI Elements

These sites use `<canvas>` not for decoration but as primary UI components.

### Simplex Noise Organic Blob (from Chiara Luzzana)
The burger menu icon is a canvas-drawn circle deformed by simplex noise, creating a living, breathing blob. Chiara's site uses **5 canvas elements** including this blob, the custom cursor, and sound visualizers.

```js
// Organic blob using simplex noise
const noise = new SimplexNoise();
const points = 8;
const radius = 30;

function drawBlob(ctx, time) {
  ctx.beginPath();
  for (let i = 0; i <= points; i++) {
    const angle = (i / points) * Math.PI * 2;
    const noiseVal = noise.noise2D(
      Math.cos(angle) * 1.5,
      Math.sin(angle) * 1.5 + time * 0.5
    );
    const r = radius + noiseVal * 10;
    const x = Math.cos(angle) * r;
    const y = Math.sin(angle) * r;
    i === 0 ? ctx.moveTo(x, y) : ctx.quadraticCurveTo(
      /* control point interpolation */
      x + Math.cos(angle) * 5,
      y + Math.sin(angle) * 5,
      x, y
    );
  }
  ctx.closePath();
  ctx.fill();
}
```

### Custom Canvas Cursor (from Chiara Luzzana)
The cursor is the highest z-index element (z: 2000+), drawn on its own canvas that follows mouse position with easing.

```js
const cursorCanvas = document.createElement('canvas');
cursorCanvas.style.cssText = `
  position: fixed; inset: 0; z-index: 2000;
  pointer-events: none; width: 100vw; height: 100vh;
`;
document.body.appendChild(cursorCanvas);

let mouseX = 0, mouseY = 0, curX = 0, curY = 0;
document.addEventListener('mousemove', e => { mouseX = e.clientX; mouseY = e.clientY; });

function drawCursor() {
  curX += (mouseX - curX) * 0.15; // eased follow
  curY += (mouseY - curY) * 0.15;
  const ctx = cursorCanvas.getContext('2d');
  ctx.clearRect(0, 0, cursorCanvas.width, cursorCanvas.height);
  ctx.beginPath();
  ctx.arc(curX, curY, 8, 0, Math.PI * 2);
  ctx.fillStyle = '#e5e3dc';
  ctx.fill();
  requestAnimationFrame(drawCursor);
}
drawCursor();

// Hide default cursor
document.body.style.cursor = 'none';
```

---

## Stateful Interactive Components

### The Device Dashboard (from Pierre-Louis Labonne)
Pierre-Louis's site has **19 Webflow IX2 interactions** creating a full device metaphor:

- **Screen content swap:** Colored buttons change what's displayed on the "screen" with a static/glitch transition between states
- **Crank mechanism:** A rotatable knob element that users can physically turn to reveal content
- **Face customizer:** An interactive avatar/face that responds to punch interactions
- **Easter eggs:** Hidden interactions (avocado facts, etc.) that reward exploration
- **LED status indicators:** Blinking dots that indicate system state

**Key pattern -- class-based state management:**
```js
// State management via CSS classes, not JS state
document.querySelectorAll('.device-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    // Remove active from all
    document.querySelectorAll('.screen-content').forEach(s => s.classList.remove('is--active'));
    // Activate matching screen
    const target = btn.dataset.screen;
    document.querySelector(`[data-content="${target}"]`).classList.add('is--active');
    // Glitch transition
    document.querySelector('.screen__grain').classList.add('is--glitch');
    setTimeout(() => document.querySelector('.screen__grain').classList.remove('is--glitch'), 200);
  });
});
```

### CRT Screen Grain Effect (from Pierre-Louis Labonne)
A rapid 10-step background-position animation on a noise PNG creates analog screen texture.

```css
.screen-grain {
  position: absolute;
  inset: 0;
  background: url('noise.png') repeat;
  opacity: 0.08;
  pointer-events: none;
  animation: grain 0.2s steps(10) infinite;
}
@keyframes grain {
  0% { background-position: 0% 0%; }
  10% { background-position: -35% -40%; }
  20% { background-position: 37% -55%; }
  30% { background-position: -48% 23%; }
  40% { background-position: 56% -30%; }
  50% { background-position: -22% 47%; }
  60% { background-position: 34% -62%; }
  70% { background-position: -67% 15%; }
  80% { background-position: 43% -38%; }
  90% { background-position: -15% 52%; }
  100% { background-position: 0% 0%; }
}
```

---

## Advanced Scroll Systems

### GSAP + ScrollTrigger + Lenis Stack (from SVZ Design)
SVZ runs **37 active GSAP tweens** with **5 ScrollTrigger** instances and Lenis smooth scrolling. This is the gold standard animation stack.

```js
// The full stack setup
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
import SplitType from 'split-type';
import Lenis from '@studio-freight/lenis';

gsap.registerPlugin(ScrollTrigger);

// Smooth scrolling with custom easing
const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  smoothWheel: true
});
function raf(time) { lenis.raf(time); requestAnimationFrame(raf); }
requestAnimationFrame(raf);
// Sync Lenis with ScrollTrigger
lenis.on('scroll', ScrollTrigger.update);

// Word-by-word reveal with SplitType
const headings = document.querySelectorAll('.reveal-heading');
headings.forEach(heading => {
  const split = new SplitType(heading, { types: 'words' });
  gsap.from(split.words, {
    y: '100%',
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out',
    stagger: 0.05,
    scrollTrigger: {
      trigger: heading,
      start: 'top 85%'
    }
  });
});

// Scrub-based parallax (tied to scroll position with smoothing)
gsap.to('.parallax-image', {
  y: '-30%',
  ease: 'none',
  scrollTrigger: {
    trigger: '.parallax-section',
    start: 'top bottom',
    end: 'bottom top',
    scrub: 2  // 2-second smoothing lag
  }
});
```

### Lottie Animations in Scroll Context (from SVZ Design)
SVZ uses **4 Lottie animations** with clip-path reveals controlled by ScrollTrigger. Lottie provides vector animations exported from After Effects.

```html
<lottie-player src="animation.json" background="transparent" speed="1" loop autoplay></lottie-player>
```

### Sticky-Scroll Scene Architecture (from The Goonies)
The Goonies uses **4 scroll containers** with **4 sticky containers** and **103 IX2 interactions**. Each "scene" is a tall scroll runway with a viewport-height sticky child:

```css
/* The scroll runway creates scroll distance */
.scroll-container { height: 300vh; position: relative; }

/* The sticky child stays pinned while parent scrolls */
.sticky-container { position: sticky; top: 0; height: 100vh; overflow: hidden; }
```

Content inside transforms based on scroll progress:
```js
// Calculate scroll progress within a scene
const container = document.querySelector('.scroll-container');
const progress = (window.scrollY - container.offsetTop) / (container.scrollHeight - window.innerHeight);
// Use progress (0-1) to drive transforms, opacity, clip-path
```

---

## Page Transition Systems

### Clip-Path + Transform Wipe (from 207ouest)
207ouest uses a dual-layer transition system at z-index 10000:
- `site-loader`: Full-viewport overlay for initial load (lavender background with SVG wordmark)
- `site-transition`: Same overlay for page-to-page navigation

```js
// Intercept internal link clicks
document.querySelectorAll('a[href^="/"]').forEach(link => {
  link.addEventListener('click', (e) => {
    e.preventDefault();
    const target = link.href;
    const overlay = document.querySelector('.site-transition');

    // Wipe in
    overlay.style.clipPath = 'inset(0 0 100% 0)';
    overlay.style.display = 'block';
    requestAnimationFrame(() => {
      overlay.style.transition = 'clip-path 0.4s cubic-bezier(0.215, 0.61, 0.355, 1)';
      overlay.style.clipPath = 'inset(0 0 0 0)';
    });

    // Navigate after wipe covers screen
    setTimeout(() => { window.location.href = target; }, 450);
  });
});
```

### Magenta Color Flash (from Chiara Luzzana)
A single high-saturation accent (#FFAAFF) used ONLY for the page transition overlay. The flash of magenta between pages is a sensory punctuation mark.

---

## Unique Interactive Patterns

### Per-Letter Rainbow Coloring (from Superlist)
52 individually colored `<span>` elements using Display P3 wide-gamut colors:

```js
const colors = [
  'color(display-p3 0.97 0.31 0.22)',  // red
  'color(display-p3 0.56 0.53 0.98)',  // purple
  'color(display-p3 0.97 0.40 0.86)',  // pink
  'color(display-p3 0.97 0.31 0.22)',  // red
];
const word = 'Superlist';
const container = document.querySelector('.rainbow-word');
container.innerHTML = word.split('').map((char, i) =>
  `<span style="color: ${colors[i % colors.length]}">${char}</span>`
).join('');
```

### Floating Section-Breaking Images (from DONUTS)
42 IX2 interactions drive product images that overlap between sections. The key CSS: parent sections have `overflow: visible` and child images use `position: absolute` with z-indices up to 9,999,999.

### Sticker Pulse Animation (from De La Calle)
A CSS keyframe called `stickerPulse` creates a breathing scale effect on badge elements, combined with continuous `spin` rotation and a `shopify-rotator` for product image carousels. De La Calle also uses **137 SVGs** and **7 clip-path** elements for its torn paper edges.

### Framer Motion at Scale (from Superlist)
Superlist has **261 Framer motion elements** with `data-framer-appear-id` attributes driving scroll-triggered entrance animations -- the most animation-dense site in our research.

---

## When to Use These Patterns

| Pattern | Best For | Complexity |
|---|---|---|
| Sound feedback | Portfolios, interactive experiences, games | Medium (needs mute toggle) |
| Canvas blob/cursor | Creative portfolios, art sites | High |
| CRT grain effect | Retro themes, device metaphors | Low (pure CSS) |
| GSAP+Lenis+SplitType | Any site needing premium scroll | Medium |
| Sticky-scroll scenes | Storytelling, narratives, showcases | Medium |
| Page transitions | Multi-page sites, SPAs | Medium |
| Rainbow text | Brand identity, playful products | Low |
| Floating images | E-commerce, food brands, maximalist | Low-Medium |

## Performance Considerations

- **Canvas cursors**: Only on desktop (`@media (hover: hover)`). Kill on mobile.
- **Sound**: Lazy-load audio files. Use Web Audio API for precise timing.
- **GSAP + ScrollTrigger**: Use `scrub` with a value (e.g., 2) for smooth interpolation rather than direct scroll binding.
- **Lottie**: Use `loading="lazy"` and only play when in viewport via Intersection Observer.
- **Multiple canvases**: Each canvas is a separate compositing layer. Limit to 3-4 max.
- **Always test on low-end devices** before shipping canvas-heavy experiences.
