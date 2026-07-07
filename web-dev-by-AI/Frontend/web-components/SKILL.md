---
name: web-components
description: Web Components fundamentals and advanced patterns: Custom Elements, Shadow DOM, slots, events, and form-associated components.
category: web-development
platforms: [linux, macos, windows]
---

# Web Components

Build reusable framework-agnostic UI components with native browser primitives.

## Core Topics

### Custom Elements
- Define reusable HTML elements
- Lifecycle: constructor → connectedCallback → disconnectedCallback → attributeChangedCallback

### Shadow DOM
- Encapsulation for markup and styles
- Use `:host`, `::part()`, and CSS custom properties for theming API

### Slots
- Named slots and default slot
- `::slotted()` for projected content
- `slotchange` event for updates

### Form-Associated Elements
- `attachInternals()`
- `setFormValue()`
- Validity and FormData integration

### Events
- Use `CustomEvent` with `bubbles` + `composed` for cross-boundary communication

### Declarative Shadow DOM
- Useful for SSR without extra client JS in some setups

## Best Practices
- Keep component API small and explicit
- Expose styling hooks carefully
- Preserve accessibility in shadow trees
- Test keyboard and focus behavior inside components

## Triggers
- "web components", "custom elements", "shadow dom", "slots", "form-associated", "declarative shadow dom"