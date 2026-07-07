# Frontend Skills

Frontend web development skills covering modern CSS, frameworks, accessibility, components, and UI experiments.

## Skills

| Skill | Description |
|-------|-------------|
| `modern-css` | Container queries, :has(), cascade layers, subgrid, fluid typography |
| `nextjs-app-router` | Next.js App Router, Server Components, Server Actions, metadata, revalidation |
| `frontend-a11y-seo` | Semantic HTML, ARIA, keyboard UX, WCAG, SEO, metadata |
| `web-components` | Custom Elements, Shadow DOM, slots, form-associated components |
| `frontend-experiments` | Skeleton loading, micro-interactions, animations, dark mode, View Transitions |

## Quick Reference

### Container Query
```css
.card-wrapper { container-type: inline-size; }
@container (min-width: 400px) { .card { ... } }
```

### :has() Selector
```css
.card:has(.badge) { border-color: blue; }
form:has(input:invalid) { border-color: red; }
```

### Cascade Layers
```css
@layer reset, base, components, utilities;
```

### Next.js Server Component
```jsx
// default is server component
export default function Page() {
  const data = await fetchData();
  return <div>{data.title}</div>;
}
```

### Next.js Client Component
```jsx
'use client';
import { useState } from 'react';
export function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(c => c+1)}>{count}</button>;
}
```

### Dark Mode CSS
```css
:root { --bg: #fff; --text: #000; }
:root.dark { --bg: #1a1a1a; --text: #fff; }
body { background: var(--bg); color: var(--text); }
```

## Folder Structure

```
Frontend/
├── modern-css/
├── nextjs-app-router/
├── frontend-a11y-seo/
├── web-components/
├── frontend-experiments/
└── README.md
```

## Triggers

Use these skills when:
- Working with modern CSS features
- Building Next.js applications
- Improving accessibility or SEO
- Creating reusable components
- Adding micro-interactions or animations