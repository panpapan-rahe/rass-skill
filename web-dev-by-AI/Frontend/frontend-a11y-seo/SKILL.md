---
name: frontend-a11y-seo
description: Accessibility and SEO for frontend work: semantic HTML, ARIA, keyboard UX, metadata, and structured data.
category: web-development
platforms: [linux, macos, windows]
---

# Frontend Accessibility & SEO

Accessibility and SEO practices for frontend systems that are usable, discoverable, and resilient.

## Core Topics

### Semantic HTML
- Use native landmarks: `header`, `nav`, `main`, `article`, `section`, `aside`, `footer`
- Prefer semantic elements before adding ARIA

### ARIA Discipline
- Use ARIA only when semantic HTML is insufficient
- Avoid incorrect or redundant roles
- Native first, ARIA last

### Keyboard UX
- Logical tab order
- Visible focus states
- Skip links for fast navigation
- Ensure interactive elements are reachable by keyboard

### WCAG Framing
- Use WCAG as the evaluation baseline
- Think about contrast, focus, labels, motion, and operability

### SEO Basics
- Correct heading hierarchy
- Meta description
- Canonical URL
- Open Graph tags
- Structured data JSON-LD when relevant

## Best Practices
- Build accessible UI from the start
- Test with keyboard only
- Maintain meaningful text alternatives for images
- Ensure forms have proper labels and errors

## Triggers
- "accessibility", "a11y", "seo", "semantic html", "aria", "wcag", "keyboard ux"