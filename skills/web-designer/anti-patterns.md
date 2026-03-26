# Anti-Patterns: The AI Aesthetic and How to Kill It

This document exists because AI code generators have converged on a recognizable visual language that screams "a machine made this." This guide teaches you to identify and avoid it.

## The AI Look: A Field Guide

### 1. The Gradient Background
**What AI does:** `background: linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
Every AI landing page has a blue-to-purple gradient. It's the beige of AI design.

**What a designer does:**
- Solid color backgrounds with texture (grain, noise, subtle pattern)
- Photography or illustration as the hero, not a gradient
- If using a gradient, make it unexpected: warm tones, radial instead of linear, very subtle
- `background: #0d0d0d` (a dark palette with typography as the hero)

```css
/* Instead of a gradient, try grain texture */
.hero {
  background: var(--color-bg);
  position: relative;
}
.hero::after {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  opacity: 0.4;
}
```

### 2. The Card Grid of Sameness
**What AI does:** Three identical cards in a row, each with an icon, a heading, and a description. Equal spacing. Equal sizing. `border-radius: 12px`. `box-shadow: 0 4px 6px rgba(0,0,0,0.1)`.

**What a designer does:**
- Vary the visual treatment across cards (different sizes, one card highlighted)
- Use numbered lists instead of icon + text cards
- Let one card break the grid (span two columns, or offset vertically)
- Skip the shadow -- use a border, background color change, or nothing
- Give each card a unique accent color (see Magic Spoon pattern)

```css
/* Asymmetric grid instead of uniform */
.features {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: var(--space-m);
}
.feature:nth-child(1) { grid-column: 1 / 8; }
.feature:nth-child(2) { grid-column: 8 / 13; }
.feature:nth-child(3) { grid-column: 1 / 5; }
.feature:nth-child(4) { grid-column: 5 / 13; }
```

### 3. The Hero With Centered Everything
**What AI does:** Centered headline, centered subtext, centered button. Perfectly symmetrical. Perfectly boring.

**What a designer does:**
- Left-aligned hero text with a visual element on the right
- Oversized type that fills the viewport width
- Text overlapping an image
- Asymmetric composition with the CTA in an unexpected position
- A video or animation as the hero instead of text

```css
/* Left-aligned hero with dramatic type */
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: var(--space-2xl);
}
.hero h1 {
  font-size: clamp(3rem, 10vw, 8rem);
  line-height: 0.95;
  letter-spacing: -0.03em;
  max-width: 12ch; /* Force line breaks for visual rhythm */
}
```

### 4. The Predictable Color Palette
**What AI does:** Blue primary, gray secondary, white background. Or: dark mode with purple accents. Every. Single. Time.

**What a designer does:**
- Derive color from the CONTENT, not from a template
- A hot sauce brand gets reds and oranges
- A wellness brand gets earth tones and sage greens
- A tech startup might get monochrome + one electric accent
- A children's brand gets high saturation and varied hues

### 5. The Hover Effect That Does Nothing
**What AI does:** `opacity: 0.8` on hover. Or `transform: scale(1.02)`. Minimal, safe, meaningless.

**What a designer does:**
- Text slides up to reveal alternate content
- Background color inverts (dark becomes light)
- An underline wipes in from one direction
- The entire card tilts in 3D based on cursor position
- An image behind the text zooms slightly while text stays fixed

### 6. The Font Stack Nobody Chose
**What AI does:** `font-family: 'Inter', system-ui, sans-serif` and calls it a day.

**What a designer does:**
- Picks a typeface that expresses the brand's personality
- Considers: Do we want warmth (humanist sans)? Authority (serif)? Energy (geometric display)? Craft (handwritten accent)?
- Uses at most 2 font families, but uses the WEIGHT RANGE within those families aggressively
- Makes the type system the primary visual design element

### 7. The Spacing Monotony
**What AI does:** `p-4` or `p-6` on everything. `gap-4` everywhere. All sections have the same padding.

**What a designer does:**
- Varies section padding dramatically (one section has `8rem` padding, the next has `2rem`)
- Uses asymmetric padding (more on top than bottom, or more on one side)
- Creates visual rhythm through spacing variation
- Generous white space on hero sections, tighter spacing in content-dense sections

### 8. The Button That Matches Every Other AI Button
**What AI does:** `bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg`

**What a designer does:**
- **Outlined button** with fill on hover
- **Text-only button** with animated underline
- **Full-width block button** for high-commitment CTAs
- **Pill-shaped button** (`border-radius: 999px`) for playful brands
- **Button with icon that animates** on hover (arrow slides right)
- **No visible button** -- the entire section/card is the click target

```css
/* The arrow-slide button */
.btn-arrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  text-decoration: none;
  font-weight: 600;
}
.btn-arrow .arrow {
  transition: transform 0.3s var(--ease-out);
}
.btn-arrow:hover .arrow {
  transform: translateX(4px);
}
```

### 9. The Footer Nobody Designed
**What AI does:** Dark gray box, four columns of links, social icons, copyright. Identical to every other site.

**What a designer does:**
- The footer is a design opportunity, not a dumping ground
- Large, bold CTA in the footer ("Ready to start?")
- The footer uses a different background that creates a visual "destination"
- Interesting typography for the company name or tagline
- The footer can be minimal (just a line of text) if the brand is minimal

### 10. The Dark Mode Toggle With No Design Thought
**What AI does:** Swaps white to `#1a1a2e` and calls it dark mode. Colors look washed out. Text contrast is broken.

**What a designer does:**
- Dark mode is a separate design, not an automated inversion
- Colors are re-selected for dark backgrounds (lighter accents, warmer grays)
- Shadows are replaced with glows or borders (shadows don't work on dark)
- Image brightness may need adjustment (`filter: brightness(0.9)`)
- Elevation in dark mode uses lighter surfaces, not shadows

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0d0d0d;
    --color-surface: #1a1a1a;
    --color-text: #e5e3dc;
    --color-border: rgba(255, 255, 255, 0.08);
    /* Shadows become glows or disappear */
    --shadow-card: 0 0 0 1px rgba(255, 255, 255, 0.06);
    /* Accent may need to brighten */
    --color-accent: #ff4d58;
  }
}
```

## The Litmus Test

Before shipping any design, ask:

1. **Could someone guess this was AI-generated?** If yes, find the generic parts and redesign them.
2. **Does it have a signature?** One memorable visual element that makes it distinctive.
3. **Does it have rhythm?** Visual variety between sections, not monotonous repetition.
4. **Does the typography do work?** Or is it just "text in a box"?
5. **Is there tension?** Large vs. small, dark vs. light, dense vs. spacious, serif vs. sans.
6. **Would YOU screenshot this?** If not, push harder.

## The Creative Injection Process

When you catch yourself defaulting to the AI look, use this process:

1. **Stop.** Recognize the pattern you're falling into.
2. **Reference.** Think about which of the award-winning sites handled this element well.
3. **Contrast.** What is the OPPOSITE of what you were about to do? Try that.
4. **Commit.** Pick the bolder option. Default to brave, not safe.

The goal is not to be different for its own sake. The goal is to be INTENTIONAL. Every design choice should be a choice, not a default.
