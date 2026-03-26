# Web Designer Plugin

**Stop generating generic AI frontends. Start designing award-winning websites.**

This plugin transforms Claude from a code generator into a world-class web designer. It injects real design thinking -- typography systems, color theory, animation vocabulary, layout patterns, and 3D techniques -- extracted from 38 of the best-designed websites of 2025-2026.

> "Would this get featured on Awwwards?" -- The standard this plugin holds you to.

## See It In Action

### FUEGO -- Bold E-commerce

![FUEGO Hot Sauce - Bold E-commerce Demo](gifs/concept-2-bold-ecommerce.gif)

Triple-stacked giant typography, torn paper SVG dividers, 3D physical buttons, spinning starburst, dual marquee tickers.

### PL-5000 -- Retro Device Portfolio

![PL-5000 Retro Device Portfolio Demo](gifs/concept-4-retro-device.gif)

CRT screen grain, physical 3D buttons that depress, rotating knob, blinking LEDs, screen content swap with glitch transition.

### WRECK -- Brutalist Agency

![WRECK Brutalist Agency Demo](gifs/concept-11-brutalist-agency.gif)

Cursor trail with mix-blend-mode inversion, text scramble cipher effect, horizontal drag scroll, live clock, acid green hover states.

### Retro Terminal -- KATREDUX

![Retro Terminal Demo](gifs/concept-retro-terminal.gif)

CRT phosphor glow, scanline overlay, terminal typing animation, ASCII art, green-on-black hacker aesthetic.

### Paper Collage -- Jules Atelier

![Paper Collage Demo](gifs/concept-paper-collage.gif)

Hand-crafted paper texture, sticky notes, polaroid photos, torn edges, tape strips, organic handmade aesthetic.

## The Problem

AI-generated frontends all look the same: blue-purple gradients, uniform card grids, `border-radius: 12px` on everything, Inter font, centered layouts, generic shadows. This is the **"AI Look"** and users can spot it instantly.

## The Solution

48 battle-tested design patterns extracted from real award-winning sites, organized into a skill that activates on demand and guides Claude to produce distinctive, creative, production-quality frontend code.

## What's Inside

| File | Content |
|---|---|
| `SKILL.md` | Core design philosophy, decision framework, anti-pattern checklist |
| `design-patterns.md` | 48 patterns -- layout, cards, navigation, text effects, 3D, advanced techniques |
| `color-and-typography.md` | 5 palette archetypes, 5 font pairing formulas, fluid type system |
| `animation-playbook.md` | Motion design vocabulary -- entrances, hovers, scroll-linked, transitions |
| `anti-patterns.md` | 10 "AI Look" traps identified and how to break each one |

### Design Patterns Include

- 3D card tilt following cursor (SVZ Design)
- Outlined/stroked typography (VOUS Church, Chiara Luzzana)
- Clip-path image reveals (SVZ Design)
- Physical 3D buttons with depth (Pierre-Louis Labonne)
- Two-tone split headings (Superlist)
- Torn paper dividers (De La Calle)
- Giant compressed hero text (DONUTS)
- Frosted glass navigation (Michael Kors, Ready.so)
- Sticky-scroll cinematic scenes (The Goonies)
- Staggered menu cascades (207ouest)
- Infinite logo tickers with fade masks (Superlist)
- Wide-gamut P3 accent colors (Superlist)
- Perspective app screenshots (Daylight Computer)
- Ambient radial glow effects (Superlist)
- And 34 more...

### Palette Archetypes

1. **Monochrome + Single Accent** -- SVZ, April Ford, Chiara Luzzana
2. **Warm Neutrals** -- VOUS Church, Hardgraft, Everlane
3. **Bold Brand** -- De La Calle, Magic Spoon, Couplet Coffee
4. **Dark Luxury** -- SVZ, Chiara Luzzana, The Goonies
5. **Sophisticated Minimal** -- Ready.so, Slite, Calm

## Installation

### Claude Code

```bash
# Add the marketplace
/plugin marketplace add MickeyAlton33/web-designer-plugin

# Install the plugin
/plugin install web-designer
```

Or install directly:

```bash
/install-plugin https://github.com/MickeyAlton33/web-designer-plugin
```

### Cursor

The plugin is automatically detected via `.cursor-plugin/plugin.json`. Clone or add as a submodule in your project.

### GitHub Copilot

Detected via `.github/plugin/plugin.json`.

### Verify Installation

After installing, you should see `web-designer` in your available skills:

```
/skills
```

## Usage

This plugin activates **on demand** -- it does not auto-trigger on every frontend task. Invoke it when you want designer-quality output:

```
Use the web-designer skill to build a landing page for a meditation app
```

```
/web-designer -- Create a portfolio site for a photographer
```

```
Use web-designer to redesign this component with award-winning quality
```

### The Decision Framework

When activated, the skill guides Claude through:

1. **MOOD** -- What emotional register? (calm/energetic/luxurious/playful/authoritative)
2. **PALETTE** -- Derived from mood, committed to constraint
3. **TYPE** -- Font strategy that carries the mood
4. **LAYOUT** -- Rhythm that serves the content
5. **MOTION** -- What needs to move and why
6. **SIGNATURE** -- The ONE thing that makes this design memorable

### Anti-Pattern Checklist

Before finalizing, the skill verifies the output doesn't fall into these traps:

- No blue-purple gradient backgrounds
- No uniform card grids with identical spacing
- No centered-everything heroes
- No `font-family: Inter` on everything
- No generic `opacity: 0.8` hover effects
- No `box-shadow: 0 4px 6px` on every card
- No identical section treatments throughout
- And 3 more...

## Examples

The `examples/` directory contains 10 concept sites spanning diverse design archetypes. Download any HTML file and open it in a browser -- they're fully self-contained.

| Preview | Concept | Signature Features |
|---|---|---|
| ![](examples/screenshots/concept-1-gravity-playground.png) | **Gravity Playground "Nova Chen"** | Outlined display text, dark immersive hero, scroll-driven reveals, motion-first portfolio |
| ![](examples/screenshots/concept-2-retro-terminal.png) | **Retro Terminal "KATREDUX"** | CRT phosphor glow, scanlines, terminal typing, ASCII art, green-on-black hacker aesthetic |
| ![](examples/screenshots/concept-2-bold-ecommerce.png) | **Bold E-commerce "FUEGO"** | Giant stacked typography, torn paper dividers, 3D buttons, spinning starburst, marquee tickers |
| ![](examples/screenshots/concept-4-paper-collage.png) | **Paper Collage "Jules Atelier"** | Hand-crafted paper texture, sticky notes, polaroids, torn edges, tape strips, organic aesthetic |
| ![](examples/screenshots/concept-4-retro-device.png) | **Retro Device "PL-5000"** | CRT grain, physical buttons, crank knob, LED indicators, screen swap with glitch, easter egg |
| ![](examples/screenshots/concept-5-fashion-editorial.png) | **Fashion Editorial "MAISON NOIR"** | Museum-frame gallery, 750ms luxury transitions, lookbook masonry grid, credits ticker |
| ![](examples/screenshots/concept-6-candy-app.png) | **Candy App "gloopy"** | Confetti on click, scratch-to-reveal, wiggle hover, bouncy easing, star badges, wavy footer |
| ![](examples/screenshots/concept-7-immersive-scroll.png) | **Immersive Scroll "Lost Observatory"** | Sticky-scroll scenes, radar pulses, typewriter effect, music player, parallax depth |
| ![](examples/screenshots/concept-10-conference.png) | **Tech Conference "GLITCH CONF"** | CSS confetti rain, SVG distortion hover, magnetic buttons, 3D rotating cube, typing effect |
| ![](examples/screenshots/concept-11-brutalist-agency.png) | **Brutalist Agency "WRECK"** | Cursor trail, text scramble cipher, mix-blend-mode, drag scroll, live clock, acid green hover |

## Research Sources

This plugin's patterns were extracted from deep analysis of these award-winning websites:

**Webflow Blog "Best Websites":** SVZ Design, Wayside Studio, VOUS Church, Ready.so, April Ford, Chiara Luzzana, Pierre-Louis Labonne, Superlist, Michael Kors Collection, Slite, The Goonies, DONUTS

**Shopify Blog "Beautiful E-commerce":** De La Calle, Magic Spoon, Couplet Coffee, Hardgraft, Haus, Koffiracha, 207ouest, Daylight Computer, Collider, and more

Each site was analyzed for: color palette, typography approach, layout/grid system, animation patterns, visual hierarchy techniques, and specific replicable CSS techniques.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The best contributions are patterns extracted from real award-winning websites with production-ready code.

## License

[MIT](LICENSE)
