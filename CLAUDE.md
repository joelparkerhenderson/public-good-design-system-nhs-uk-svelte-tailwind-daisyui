# CLAUDE.md

Project context for Claude Code AI assistant.

## Project Overview

Public Good Design System: a Svelte component library inspired by the NHS UK Design System, styled with Tailwind CSS v4 and DaisyUI v5. The project provides 36 accessible UI components for public good web applications.

## Tech Stack

- **Svelte 5** with runes (`$props()`, `$state()`, `$derived()`, `$bindable()`)
- **SvelteKit 2** with `adapter-auto`, `vitePreprocess`
- **TypeScript 5** with strict mode, bundler module resolution
- **Tailwind CSS v4** configured via CSS (`@import 'tailwindcss'`), not `tailwind.config.js`
- **DaisyUI v5** loaded via `@plugin "daisyui"` in `src/app.css`
- **PostCSS** with `@tailwindcss/postcss` (handles vendor prefixing, no autoprefixer needed)
- **Vite** for dev server and production builds

## Key Architecture Decisions

### Tailwind v4 CSS-based Configuration

All Tailwind and DaisyUI configuration lives in `src/app.css` using CSS directives:
- `@import 'tailwindcss'` for the framework
- `@plugin "daisyui"` to load DaisyUI
- `@plugin "daisyui/theme" { ... }` for the custom "public-good" theme
- No `tailwind.config.js` file (v3 pattern, removed)

### Svelte 5 Patterns

Components use Svelte 5 runes exclusively:
- `$props()` for component props with TypeScript interfaces
- `$state()` for reactive local state
- `$derived(expression)` for computed values (NOT `$derived(() => expr)` which creates a function)
- `$derived((() => { ... })())` IIFE pattern for complex multi-statement derived values
- `$bindable()` for two-way bindable props
- `{@render children()}` for slot content (not `<slot />`)
- `{#snippet name()}` for reusable template fragments
- `onclick`/`onchange`/`oninput` (not `on:click`/`on:change`/`on:input`)

### Component Props Pattern

Every component follows this structure:
```svelte
<script lang="ts">
  import type { SomeProps } from '$lib/types.js';
  interface Props extends SomeProps {}
  let { prop1, prop2, classes = '', attributes = {}, children, ...restProps }: Props = $props();
</script>
```

### Dynamic Heading Levels

Components that support configurable heading levels (h1-h6) use:
```svelte
const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);
<svelte:element this={HeadingTag}>...</svelte:element>
```

### CSS Classes

Components use a combination of:
- `public-good-*` prefixed classes for component-specific selectors
- DaisyUI component classes (`btn`, `card`, `alert`, `badge`, `input`, etc.)
- Tailwind utility classes for layout and spacing

## File Structure

```
src/
  app.css                         # Tailwind + DaisyUI + theme config
  app.html                        # HTML template
  lib/
    index.ts                      # Re-exports components and types
    types.ts                      # All TypeScript interfaces (~550 lines)
    components/
      index.ts                    # Barrel exports for all 36 components
      [component-name]/
        ComponentName.svelte      # Component implementation
  routes/
    +layout.svelte                # Root layout (imports app.css)
    +page.svelte                  # Home page
    components/+page.svelte       # Component showcase/demo page
```

## Commands

```bash
npm run dev          # Start dev server (port 5173)
npm run build        # Production build
npm run preview      # Preview production build
npm run check        # svelte-check + TypeScript validation
```

## Important Notes

- **No test files exist yet** - no Vitest, Playwright, or other test infrastructure
- **No i18n** - single language (English)
- **No Storybook** - component demos are in `routes/components/+page.svelte`
- All component type interfaces are centralized in `src/lib/types.ts`
- The `BaseComponentProps` interface provides `classes`, `attributes`, and `children` to all components
- DaisyUI theme uses oklch color format for perceptual uniformity
- `@tailwindcss/forms` and `@tailwindcss/typography` are NOT used (DaisyUI provides form and typography styling)
- The build target is `adapter-auto` which detects the deployment platform

## Common Pitfalls

1. **$derived(() => expr)** creates a getter function, NOT a direct value. Use `$derived(expr)` for simple expressions or `$derived((() => { ... })())` for complex logic.
2. **Tailwind v4** does not use `tailwind.config.js`. All config is CSS-based in `src/app.css`.
3. **DaisyUI v5** themes use oklch colors and are configured via `@plugin "daisyui/theme"` in CSS.
4. **Svelte 5** uses `onclick` not `on:click`, `{@render children()}` not `<slot />`.
5. **Do not add redundant ARIA roles** to semantic HTML elements (e.g., `role="navigation"` on `<nav>`).
6. **Avoid `Math.random()` for IDs** in components - causes SSR hydration mismatches.
