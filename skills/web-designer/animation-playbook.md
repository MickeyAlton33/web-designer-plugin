# Animation Playbook

Motion design patterns extracted from award-winning websites. Every animation here has a specific job -- none are decorative.

## Principles

### 1. Every Animation Needs a Job
- **ENTER**: Revealing content as it enters the viewport
- **STATE**: Indicating a change (hover, active, selected, loading)
- **CONTINUITY**: Connecting two views or states together
- **DELIGHT**: Rewarding interaction (use sparingly)

If an animation doesn't serve one of these four purposes, remove it.

### 2. Easing Is Everything
The difference between cheap and premium motion is the easing curve.

```css
/* NEVER use these */
transition: all 0.3s ease;          /* Generic, lifeless */
transition: all 0.3s linear;        /* Robotic */

/* USE these instead */
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);       /* Smooth deceleration -- best for entrances */
--ease-in-out: cubic-bezier(0.65, 0.01, 0.05, 0.99); /* Weighty, intentional -- SVZ signature */
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);  /* Slight overshoot -- playful */
--ease-snap: cubic-bezier(0.85, 0, 0.15, 1);       /* Quick start, smooth end -- UI state changes */
```

### 3. Duration Guidelines
| Type | Duration | Example |
|---|---|---|
| Micro-interaction | 150-250ms | Button hover, checkbox toggle |
| State change | 300-500ms | Menu open, panel expand |
| Entrance animation | 600-1000ms | Content reveal on scroll |
| Page transition | 800-1200ms | Route change, overlay |
| Slow/luxurious | 1200-2000ms | Hero parallax, editorial scroll |

### 4. Stagger Creates Rhythm
When multiple elements animate, stagger their timing.

```css
.stagger > * {
  opacity: 0;
  transform: translateY(2rem);
  animation: fadeUp 0.8s var(--ease-out) forwards;
}
.stagger > *:nth-child(1) { animation-delay: 0ms; }
.stagger > *:nth-child(2) { animation-delay: 80ms; }
.stagger > *:nth-child(3) { animation-delay: 160ms; }
.stagger > *:nth-child(4) { animation-delay: 240ms; }

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

## Entrance Animations

### Fade Up (The Standard)
The workhorse entrance. Subtle, reliable, professional.

```css
.reveal {
  opacity: 0;
  transform: translateY(3rem);
  transition: opacity 0.8s var(--ease-out),
              transform 0.8s var(--ease-out);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

### Clip-Path Reveal (from SVZ Design)
Content reveals via an expanding clip-path -- more dramatic than a fade.

```css
.clip-reveal {
  clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0 100%);
  transition: clip-path 1s cubic-bezier(0.23, 1, 0.32, 1);
}
.clip-reveal.visible {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```

**Variants:**
```css
/* Reveal from left */
.clip-left { clip-path: inset(0 100% 0 0); }
.clip-left.visible { clip-path: inset(0 0 0 0); }

/* Reveal from center */
.clip-center { clip-path: inset(0 50% 0 50%); }
.clip-center.visible { clip-path: inset(0 0 0 0); }

/* Circle reveal */
.clip-circle { clip-path: circle(0% at 50% 50%); }
.clip-circle.visible { clip-path: circle(75% at 50% 50%); }
```

### Word-by-Word Text Reveal (from SVZ Design)
Split text into words and stagger their entrance.

```css
.word-reveal {
  overflow: hidden;
}
.word-reveal .word {
  display: inline-block;
  transform: translateY(100%);
  transition: transform 0.6s var(--ease-out);
}
.word-reveal.visible .word {
  transform: translateY(0);
}
/* Stagger via CSS custom property */
.word-reveal.visible .word:nth-child(1) { transition-delay: 0ms; }
.word-reveal.visible .word:nth-child(2) { transition-delay: 50ms; }
.word-reveal.visible .word:nth-child(3) { transition-delay: 100ms; }
.word-reveal.visible .word:nth-child(4) { transition-delay: 150ms; }
.word-reveal.visible .word:nth-child(5) { transition-delay: 200ms; }
```

```js
// Auto-wrap words for the animation
document.querySelectorAll('.word-reveal').forEach(el => {
  el.innerHTML = el.textContent.split(' ')
    .map(word => `<span class="word">${word}&nbsp;</span>`)
    .join('');
});
```

### Scale Reveal (from April Ford)
Element scales in from one direction using transform-origin shift.

```css
.scale-reveal {
  transform: scaleX(0);
  transform-origin: 100% 50%;
  transition: transform 0.6s var(--ease-out);
}
.scale-reveal.visible {
  transform: scaleX(1);
  transform-origin: 0% 50%;
}
```

---

## Hover Interactions

### The Directional Underline (from Chiara Luzzana)
```css
.link-directional {
  position: relative;
  text-decoration: none;
}
.link-directional::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 100%;
  height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.35s ease;
}
.link-directional:hover::after {
  transform: scaleX(1);
  transform-origin: left;
}
```

### The Text Swap (from April Ford)
```css
.btn-swap {
  position: relative;
  overflow: hidden;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.btn-swap .label,
.btn-swap .label-hover {
  transition: transform 0.4s var(--ease-out);
}
.btn-swap .label-hover {
  position: absolute;
  transform: translateY(100%);
}
.btn-swap:hover .label {
  transform: translateY(-100%);
}
.btn-swap:hover .label-hover {
  transform: translateY(0);
}
```

### The Background Fill
Button background fills from one side on hover.

```css
.btn-fill {
  position: relative;
  overflow: hidden;
  z-index: 1;
  border: 1px solid currentColor;
  background: transparent;
  transition: color 0.4s var(--ease-out);
}
.btn-fill::before {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-text);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.4s var(--ease-out);
  z-index: -1;
}
.btn-fill:hover {
  color: var(--color-bg);
}
.btn-fill:hover::before {
  transform: scaleX(1);
}
```

### The Card Lift
Subtle elevation change with shadow progression.

```css
.card-interactive {
  transition: transform 0.4s var(--ease-out),
              box-shadow 0.4s var(--ease-out);
}
.card-interactive:hover {
  transform: translateY(-4px);
  box-shadow: 0 1.5rem 3rem -0.75rem rgba(0, 0, 0, 0.12);
}
.card-interactive:active {
  transform: translateY(-2px);
  box-shadow: 0 0.75rem 1.5rem -0.5rem rgba(0, 0, 0, 0.1);
}
```

### The Image Zoom (Contained)
Image zooms inside its container on hover.

```css
.image-zoom {
  overflow: hidden;
  border-radius: clamp(0.5rem, 1vw, 1rem);
}
.image-zoom img {
  transition: transform 0.6s var(--ease-out);
  will-change: transform;
}
.image-zoom:hover img {
  transform: scale(1.05);
}
```

---

## Scroll-Linked Animations

### Intersection Observer (Vanilla JS)
The foundation for scroll-triggered animations without a library.

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target); // animate once
    }
  });
}, {
  threshold: 0.15,     // trigger when 15% visible
  rootMargin: '0px 0px -50px 0px'  // slight offset from bottom
});

document.querySelectorAll('.reveal, .clip-reveal, .word-reveal, .scale-reveal, .stagger')
  .forEach(el => observer.observe(el));
```

### CSS-Only Scroll Animation (Modern browsers)
Using `animation-timeline: view()` for scroll-linked animations without JS.

```css
@supports (animation-timeline: view()) {
  .scroll-fade {
    animation: scrollReveal linear both;
    animation-timeline: view();
    animation-range: entry 0% entry 100%;
  }
  @keyframes scrollReveal {
    from {
      opacity: 0;
      transform: translateY(3rem);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
}
```

### Parallax Layer (CSS transforms)
Background moves at a different speed than foreground content.

```css
.parallax-container {
  overflow: hidden;
  position: relative;
}
.parallax-bg {
  position: absolute;
  inset: -20% 0;
  will-change: transform;
}
```
```js
// Simple parallax with requestAnimationFrame
const parallaxElements = document.querySelectorAll('.parallax-bg');
function updateParallax() {
  parallaxElements.forEach(el => {
    const rect = el.parentElement.getBoundingClientRect();
    const scrollProgress = rect.top / window.innerHeight;
    el.style.transform = `translateY(${scrollProgress * 60}px)`;
  });
  requestAnimationFrame(updateParallax);
}
requestAnimationFrame(updateParallax);
```

---

## Page Transitions

### The Color Flash (from Chiara Luzzana)
A full-screen color overlay wipes in, page changes behind it, then wipes out.

```css
.page-transition {
  position: fixed;
  inset: 0;
  background: var(--color-accent);
  z-index: 9999;
  transform: scaleY(0);
  transform-origin: bottom;
  pointer-events: none;
}
.page-transition.entering {
  animation: wipeIn 0.6s var(--ease-snap) forwards;
}
.page-transition.exiting {
  animation: wipeOut 0.6s var(--ease-snap) forwards;
  transform-origin: top;
}
@keyframes wipeIn {
  to { transform: scaleY(1); }
}
@keyframes wipeOut {
  from { transform: scaleY(1); }
  to { transform: scaleY(0); }
}
```

### The Fade Through
Simpler transition -- content fades out, new content fades in.

```css
.page-content {
  transition: opacity 0.3s ease;
}
.page-content.exiting {
  opacity: 0;
}
```

---

## Loading Animations

### Counter Loader (from April Ford)
A percentage counter that only plays on first visit.

```js
// Cookie-gated loader
if (!sessionStorage.getItem('loaded')) {
  const counter = document.querySelector('.loader-count');
  let progress = 0;
  const interval = setInterval(() => {
    progress += Math.random() * 15;
    if (progress >= 100) {
      progress = 100;
      clearInterval(interval);
      document.querySelector('.loader').classList.add('done');
      sessionStorage.setItem('loaded', 'true');
    }
    counter.textContent = Math.floor(progress);
  }, 50);
} else {
  document.querySelector('.loader')?.remove();
}
```

### Skeleton Screen
More useful than a spinner -- shows the shape of content before it loads.

```css
.skeleton {
  background: linear-gradient(
    90deg,
    var(--color-surface) 25%,
    var(--color-surface-hover) 50%,
    var(--color-surface) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
  border-radius: 0.25rem;
}
@keyframes shimmer {
  from { background-position: 200% 0; }
  to { background-position: -200% 0; }
}
```

---

## Micro-Interactions

### The Pulse Ring (from April Ford)
A radar-ping ripple around an element.

```css
.pulse-ring {
  position: relative;
}
.pulse-ring::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 50%;
  animation: pulse 2s ease-out infinite;
}
@keyframes pulse {
  0% { box-shadow: 0 0 0 0 rgba(var(--accent-rgb), 0.4); }
  70% { box-shadow: 0 0 0 15px rgba(var(--accent-rgb), 0); }
  100% { box-shadow: 0 0 0 0 rgba(var(--accent-rgb), 0); }
}
```

### The Toggle Morph
Hamburger icon morphs to X.

```css
.burger-line {
  display: block;
  width: 24px;
  height: 2px;
  background: currentColor;
  transition: transform 0.3s var(--ease-out),
              opacity 0.3s var(--ease-out);
}
.burger.open .burger-line:nth-child(1) {
  transform: translateY(8px) rotate(45deg);
}
.burger.open .burger-line:nth-child(2) {
  opacity: 0;
}
.burger.open .burger-line:nth-child(3) {
  transform: translateY(-8px) rotate(-45deg);
}
```

---

## Performance Rules

1. **Only animate `transform` and `opacity`.** These are GPU-composited. Animating `width`, `height`, `top`, `left`, `margin`, or `padding` triggers layout recalculation and will jank.

2. **Use `will-change` sparingly.** Only on elements that are ABOUT to animate, not on everything.

3. **Intersection Observer for lazy triggers.** Don't run scroll handlers on every frame. Let the browser tell you when elements are visible.

4. **`translate3d(0,0,0)` promotes to GPU layer.** Use it when you need smooth compositing but `will-change` is too aggressive.

5. **Always respect `prefers-reduced-motion`:**
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

6. **Debounce scroll/resize handlers.** If you must use them instead of Intersection Observer:
```js
let ticking = false;
window.addEventListener('scroll', () => {
  if (!ticking) {
    requestAnimationFrame(() => {
      // your scroll logic
      ticking = false;
    });
    ticking = true;
  }
});
```
