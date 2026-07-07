---
name: modern-css
description: Modern CSS techniques including container queries, :has(), cascade layers, subgrid, nesting, and fluid typography.
category: web-development
platforms: [linux, macos, windows]
---

# Modern CSS

Modern CSS patterns for building reusable, responsive, and maintainable UI systems.

## Core Topics

### Container Queries
- Use `container-type: inline-size` on the correct wrapper
- Build responsiveness around component size, not viewport size
- Great for reusable card/layout components

### `:has()` Selector
- Style parent based on child state/content
- Useful for forms, toggles, cards, and conditional UI
- Watch selector specificity inside `:has()`

### Cascade Layers
- Use `@layer` to control CSS order explicitly
- Suggested order: `reset`, `base`, `components`, `utilities`
- Reduces specificity wars

### Subgrid
- Align nested layouts to parent grid tracks
- Very useful for cards, forms, and content tables

### CSS Nesting
- Improves readability for component styles
- Keep nesting shallow to avoid overly complex selectors

### Fluid Typography
- Use `clamp()` for scalable type
- Avoid too many breakpoint-specific font sizes

## Best Practices
- Prefer semantic class naming
- Keep component styles local and predictable
- Use CSS variables for theme tokens
- Prefer modern CSS before adding JavaScript behavior

## Triggers
- "css", "container queries", ":has()", "@layer", "subgrid", "nesting", "fluid typography"