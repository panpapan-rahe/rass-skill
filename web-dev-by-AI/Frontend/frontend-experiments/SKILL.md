---
name: frontend-experiments
description: Frontend UI experiments and micro-interactions: skeleton loading, animations, dark mode, scroll effects, and zero-dependency patterns.
category: web-development
platforms: [linux, macos, windows]
---

# Frontend Experiments

Frontend UI experiments and interactive patterns collected from learning sessions. Zero-framework, minimal-dependency approaches.

## Core Topics

### Skeleton Loading
- CSS-only with pulse animation
- Dismissal via `fonts.ready` + load event

### Micro-interactions
- Hover lift effects
- Button arrow transitions
- Nav underline animations
- Card border transitions

### Ripple Effect
- Material Design style ripple
- Pure JavaScript implementation
- Auto-cleanup via `animationend`

### Scroll Animations
- Intersection Observer for visibility
- Staggered animation delays
- Animate-once pattern

### Count-Up Animation
- `requestAnimationFrame` + ease-out cubic easing

### View Transitions API
- Page transitions with graceful degradation

### Dark Mode
- CSS custom properties + class toggle
- `localStorage` persistence
- System preference detection (`prefers-color-scheme`)

### Reduced Motion
- `prefers-reduced-motion` media query
- Accessibility for users sensitive to motion

### Zero-Framework Frontend
- When pure HTML/CSS/JS is better than React/Vue/Svelte
- Minimal bundle size approach

## Best Practices
- Start with CSS where possible
- Use `requestAnimationFrame` for animations
- Respect `prefers-reduced-motion`
- Keep interactions lightweight and performant

## Triggers
- "micro-interactions", "animation", "skeleton loading", "dark mode", "scroll animation", "view transitions"