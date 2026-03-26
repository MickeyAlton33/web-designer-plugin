# Contributing to Web Designer Plugin

Thanks for wanting to make AI-generated design better for everyone.

## Adding New Patterns

The best contributions are **patterns extracted from real award-winning websites**, not theoretical CSS techniques. Each pattern should:

1. **Come from a real site** -- link it in your PR
2. **Include production-ready code** -- CSS that works, not pseudocode
3. **Respect accessibility** -- `prefers-reduced-motion`, contrast ratios, keyboard navigation
4. **Include a "when to use" context** -- not every pattern fits every project

## Where to Add Things

- **Layout/card/nav/text patterns** --> `skills/web-designer/design-patterns.md`
- **Color palettes or font pairings** --> `skills/web-designer/color-and-typography.md`
- **Animation techniques** --> `skills/web-designer/animation-playbook.md`
- **AI aesthetic traps to avoid** --> `skills/web-designer/anti-patterns.md`
- **Concept site demos** --> `examples/`

## Style Guide

- Keep code examples self-contained (no external dependencies)
- Use CSS custom properties for colors and spacing
- Use `clamp()` for fluid sizing, never fixed `px` for typography
- Include both CSS and JS where animation requires it
- Number patterns sequentially within their section

## Testing

Build a concept site that uses your new pattern. Add it to `examples/` if it demonstrates something the existing concepts don't cover.
