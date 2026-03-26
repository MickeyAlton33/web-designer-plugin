# Color & Typography Guide

## Color Strategy

### The One Rule
**Commit to a constraint.** The most stunning websites use 2-3 colors max in their UI. The content (photography, illustrations, product images) provides the rest. Your UI palette should be a frame, not a painting.

### Palette Archetypes

Choose ONE archetype based on the project's mood. Do not mix archetypes.

#### 1. Monochrome + Single Accent
The most versatile and hardest to mess up. Used by SVZ Design, April Ford, Chiara Luzzana.

```css
:root {
  --color-bg: #0d0d0d;          /* Near-black (NOT pure #000) */
  --color-text: #e5e3dc;        /* Warm off-white (NOT pure #fff) */
  --color-muted: #8c8c8c;       /* Mid-gray for secondary text */
  --color-accent: #ff232e;      /* ONE bold accent -- CTAs, links, highlights */
}
```

**Rules:**
- The accent color appears ONLY on interactive/actionable elements
- Never use the accent as a background color for large areas
- The scarcity of the accent is what makes it powerful

#### 2. Warm Neutrals
Approachable, human, premium. Used by VOUS Church, Hardgraft, Everlane.

```css
:root {
  --color-bg: #faf8f5;          /* Warm cream, NOT cold gray */
  --color-surface: #f2eeea;     /* Slightly darker warm surface */
  --color-text: #1a1a1a;        /* Near-black text */
  --color-muted: #a5a3a6;       /* Warm mid-gray */
  --color-accent: #1a1a1a;      /* Accent IS the text color -- bold by weight, not hue */
}
```

**Rules:**
- Color temperature matters. #f5f5f5 (cold gray) reads as clinical. #faf8f5 (warm cream) reads as inviting.
- Let photography carry the color story
- Use black as the accent through weight and scale, not a separate hue

#### 3. Bold Brand Palette
High-energy, playful, confident. Used by De La Calle, Magic Spoon, Couplet Coffee, Koffiracha.

```css
:root {
  --color-bg: #fef3e2;          /* Warm tinted background */
  --color-primary: #e63946;     /* Dominant brand color */
  --color-secondary: #1d3557;   /* Contrasting secondary */
  --color-text: #1d3557;        /* Text uses the secondary for readability */
  --color-pop: #f4a261;         /* Accent for highlights and CTAs */
}
```

**Rules:**
- Bold palettes need ONE dominant color (60%), one secondary (30%), one pop (10%)
- The 60/30/10 rule prevents visual chaos
- Each color in the palette must have a defined role and stick to it

#### 4. Dark Luxury
Cinematic, immersive, premium. Used by SVZ, Chiara Luzzana, The Goonies.

```css
:root {
  --color-bg: #0d0d0d;          /* Near-black */
  --color-surface: #1a1a1a;     /* Elevated surface */
  --color-surface-hover: #252525; /* Interactive surface */
  --color-text: #ffffff;
  --color-text-muted: rgba(255, 255, 255, 0.5);
  --color-accent: #ff232e;      /* High-saturation accent */
}
```

**Rules:**
- NEVER use pure `#000000` for backgrounds -- `#0d0d0d` or `#0a0a0a` has depth, pure black is flat
- Always enable font smoothing (`-webkit-font-smoothing: antialiased`) on dark backgrounds
- Use `rgba()` white for text hierarchy levels, not separate gray hex values

#### 5. Sophisticated Minimal
Clean but not clinical. Used by Ready, Slite, Calm, Superlist.

```css
:root {
  --color-bg: #ffffff;
  --color-surface: #f7f7f8;
  --color-border: #e5e5e7;
  --color-text: #111111;
  --color-text-secondary: #6b7280;
  --color-accent: #2563eb;      /* A single, confident blue */
}
```

**Rules:**
- The border color does heavy lifting for structure -- use it instead of shadows
- White space is more important than any color choice
- If it looks like a default template, you haven't pushed the typography far enough

### Color Do's and Don'ts

| Do | Don't |
|---|---|
| Use near-blacks (`#0d0d0d`) and warm whites (`#faf8f5`) | Use pure `#000` and `#fff` together (too harsh) |
| Derive your full palette before coding | Pick colors as you go |
| Test text contrast ratios (WCAG AA minimum) | Sacrifice readability for aesthetics |
| Use `rgba()` or `oklch()` for transparent variants | Create 15 different gray hex values |
| Let one color dominate (60/30/10) | Use all colors equally |
| Use CSS custom properties for your palette | Hard-code hex values throughout |

---

## Typography Strategy

### Font Pairing Formulas

These are proven combinations. Use them as starting points, not defaults.

#### Formula 1: Display Serif + Body Sans
Classic editorial. Timeless and versatile.
```css
--font-display: 'Instrument Serif', 'Times New Roman', serif;
--font-body: 'Inter', 'Helvetica Neue', sans-serif;
```
**Best for:** Editorial, luxury, content-heavy sites

#### Formula 2: Geometric Sans + Humanist Sans
Modern, clean, approachable.
```css
--font-display: 'Montserrat', sans-serif;
--font-body: 'Open Sans', sans-serif;
```
**Best for:** SaaS, corporate, professional services

#### Formula 3: Single Family, Multiple Weights
Maximum cohesion. The hierarchy comes from weight and size, not different faces.
```css
--font-primary: 'Satoshi', 'DM Sans', sans-serif;
/* Use weights: 300 for body, 500 for subheadings, 700-900 for display */
```
**Best for:** Minimal design, apps, dashboards

#### Formula 4: Display + Mono
Technical, editorial, distinctive.
```css
--font-display: 'Space Grotesk', sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', monospace;
```
**Best for:** Developer tools, tech brands, creative agencies

#### Formula 5: Bold Display + Neutral Body
When the heading typeface IS the brand.
```css
--font-display: 'Clash Display', 'Cabinet Grotesk', sans-serif;
--font-body: 'General Sans', 'Inter', sans-serif;
```
**Best for:** Portfolios, startups, bold brands

### The Fluid Type System

NEVER use fixed pixel sizes for typography. Always use `clamp()` for fluid scaling.

```css
/* Type scale with 1.25 ratio (Major Third) */
:root {
  --text-xs:  clamp(0.64rem, 0.61rem + 0.15vw, 0.72rem);
  --text-sm:  clamp(0.80rem, 0.75rem + 0.24vw, 0.94rem);
  --text-base: clamp(1.00rem, 0.91rem + 0.43vw, 1.25rem);
  --text-lg:  clamp(1.25rem, 1.11rem + 0.68vw, 1.67rem);
  --text-xl:  clamp(1.56rem, 1.36rem + 1.03vw, 2.22rem);
  --text-2xl: clamp(1.95rem, 1.64rem + 1.56vw, 2.96rem);
  --text-3xl: clamp(2.44rem, 1.97rem + 2.35vw, 3.95rem);
  --text-4xl: clamp(3.05rem, 2.36rem + 3.46vw, 5.26rem);
  --text-5xl: clamp(3.82rem, 2.80rem + 5.09vw, 7.01rem);
}
```

### Typography Techniques From Award-Winning Sites

#### Viewport-Scaled Display Text (from SVZ Design)
```css
.hero-title {
  font-size: calc(0.625rem + 4.5vw);
  letter-spacing: -0.03em;
  line-height: 1.05;
  font-weight: 800;
}
```

#### Outlined/Stroked Headings (from VOUS Church, Chiara Luzzana)
```css
.heading-outlined {
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke: 1.5px currentColor;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.02em;
}
@media (max-width: 480px) {
  .heading-outlined { -webkit-text-stroke-width: 0.8px; }
}
```

#### Editorial Uppercase (from Michael Kors Collection)
```css
.editorial-heading {
  font-family: 'Times New Roman', Times, serif;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  line-height: 1.08;
  font-weight: 400;
}
```

#### Variable Font Weight Animation (from April Ford)
```css
.heading-animated {
  font-variation-settings: "wght" 400;
  transition: font-variation-settings 0.6s ease;
}
.heading-animated:hover {
  font-variation-settings: "wght" 900;
}
```

#### Text-Wrap Balance (modern browsers)
```css
h1, h2, h3 {
  text-wrap: balance;
}
p {
  text-wrap: pretty;
}
```

### Typography Hierarchy Rules

1. **Size ratio between heading levels should be at least 1.25x** (Major Third scale or larger)
2. **Display text gets tight line-height** (1.0-1.1) while body text gets comfortable line-height (1.5-1.7)
3. **Negative letter-spacing on large text** (-0.02em to -0.05em) prevents it from looking loose
4. **Positive letter-spacing on small caps/uppercase** (+0.02em to +0.05em) improves readability
5. **Maximum line length of 65-75 characters** for body text (`max-width: 42rem`)
6. **Font weight creates hierarchy** as effectively as font size -- a 300-weight body next to an 800-weight heading creates dramatic contrast at the same size
7. **Always test with real content.** "Lorem ipsum" hides hierarchy problems.

### Font Loading Best Practice
```html
<!-- Preload critical fonts -->
<link rel="preload" href="/fonts/display.woff2" as="font" type="font/woff2" crossorigin>

<!-- Font-display: swap prevents invisible text -->
<style>
@font-face {
  font-family: 'Display Font';
  src: url('/fonts/display.woff2') format('woff2');
  font-display: swap;
  font-weight: 100 900; /* Variable font range */
}
</style>
```
