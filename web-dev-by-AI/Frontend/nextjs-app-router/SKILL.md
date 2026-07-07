---
name: nextjs-app-router
description: Next.js App Router architecture, Server Components, Server Actions, metadata, middleware, and revalidation patterns.
category: web-development
platforms: [linux, macos, windows]
---

# Next.js App Router

Patterns and practices for building modern Next.js applications with the App Router.

## Core Topics

### App Router Structure
- `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`
- Nested layouts by route segment
- Route groups for organization

### Server Components
- Default in App Router
- Good for data fetching and initial render
- Avoid sending unnecessary logic to browser

### Client Components
- Use `'use client'` only when needed
- Required for state, hooks, and browser events

### Server Actions
- Direct form/action mutations
- Useful for create/update/delete flows without extra API routes

### Revalidation
- `revalidatePath()` for route refresh after mutation
- `revalidateTag()` for tag-based caching strategies

### Metadata & SEO
- Use `metadata` export for page/head data
- Keep layout metadata consistent and centralized

### Middleware
- Auth gate, redirects, rewrites, request control
- Useful before route resolution

## Best Practices
- Prefer Server Components until interactivity is required
- Keep route structure simple and intentional
- Avoid unnecessary client-side bundles
- Use clear boundaries between server and client logic

## Triggers
- "nextjs", "app router", "server components", "server actions", "middleware", "revalidation"