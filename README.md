# Public Good Design System &rarr; NHS UK &rarr; Svelte + Tailwind + DaisyUI

A modern, accessible Svelte component library inspired by the NHS UK Design System, built with Svelte 5, TypeScript, Tailwind CSS v4, and DaisyUI v5.

One of three variations:

- [NHS UK &rarr; HTML CSS Javascript](https://github.com/joelparkerhenderson/public-good-design-system-nhs-uk-html-css-typescript)
- [NHS UK &rarr; Next.js Tailwind DaisyUI](https://github.com/joelparkerhenderson/public-good-design-system-nhs-uk-next-tailwind-daisyui)
- [NHS UK &rarr; Svelte Tailwind DaisyUI](https://github.com/joelparkerhenderson/public-good-design-system-nhs-uk-svelte-tailwind-daisyui) (This one)

## Overview

This project converts NHS UK Design System components into reusable Svelte 5 components styled with Tailwind CSS utility classes and DaisyUI component classes. It is intended to serve as a foundation for public good web applications that need accessible, well-structured UI components.

## Tech Stack

- **Svelte 5** with runes (`$props`, `$state`, `$derived`, `$bindable`)
- **SvelteKit 2** for routing, SSR, and static generation
- **TypeScript 5** with strict mode
- **Tailwind CSS v4** with CSS-based configuration
- **DaisyUI v5** component classes and theming
- **Vite 6** for development and bundling

## Getting Started

### Prerequisites

- Node.js 20.9.0 or 22.11.0+
- npm

### Installation

```bash
git clone <repository-url>
cd public-good-design-system-nhs-uk-svelte-tailwind-daisyui
npm install
```

### Development

```bash
npm run dev       # Start development server
npm run build     # Build for production
npm run preview   # Preview production build locally
npm run check     # Run TypeScript and Svelte checks
```

## Components (36)

All components are available as Svelte 5 components with TypeScript props interfaces.

### Form Elements

| Component      | Description                                               |
| -------------- | --------------------------------------------------------- |
| Button         | Primary, secondary, and warning button variants           |
| CharacterCount | Textarea with character/word count and threshold warnings |
| Checkboxes     | Checkbox group with conditional reveal support            |
| DateInput      | Day/month/year date input fields                          |
| ErrorMessage   | Inline error message for form fields                      |
| ErrorSummary   | Summary of form errors with anchor links                  |
| Fieldset       | Groups related form fields with legend                    |
| Hint           | Help text for form fields                                 |
| Input          | Text input with prefix/suffix and width support           |
| Label          | Accessible form label with page heading option            |
| Radios         | Radio group with conditional reveal and dividers          |
| Select         | Dropdown select with option groups                        |
| Textarea       | Multi-line text input with rows/cols support              |

### Navigation

| Component    | Description                                     |
| ------------ | ----------------------------------------------- |
| ActionLink   | Call-to-action link with arrow icon             |
| BackLink     | "Go back" navigation link                       |
| Breadcrumb   | Breadcrumb trail navigation                     |
| ContentsList | Table of contents with anchor links             |
| Footer       | Page footer with navigation links and copyright |
| Header       | Site header with logo, navigation, and search   |
| Pagination   | Previous/next page navigation                   |
| SkipLink     | Accessibility skip-to-content link              |

### Content Display

| Component          | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| Card               | Content card with heading, description, image, and clickable variants |
| Details            | Expandable disclosure widget                                          |
| DoDontList         | Side-by-side do/don't guidance lists                                  |
| Hero               | Full-width hero banner with actions and background image              |
| Images             | Responsive image with caption                                         |
| InsetText          | Visually indented block of text                                       |
| NotificationBanner | Alert banner for success, info, or warning messages                   |
| Panel              | Confirmation or highlight panel                                       |
| SummaryList        | Key-value summary with optional actions                               |
| Tables             | Data table with responsive header and caption                         |
| Tabs               | Tabbed content with keyboard navigation                               |
| Tag                | Status badge/tag with colour variants                                 |
| TaskList           | Task list with status indicators                                      |
| WarningCallout     | Warning callout box with heading                                      |

## Project Structure

```
src/
  app.css                    # Tailwind + DaisyUI theme configuration
  app.html                   # HTML shell
  lib/
    index.ts                 # Library entry point (re-exports)
    types.ts                 # TypeScript interfaces for all components
    components/
      index.ts               # Component barrel exports
      action-link/           # Each component in its own directory
      back-link/
      breadcrumb/
      button/
      ...
  routes/
    +layout.svelte           # Root layout
    +page.svelte             # Home page
    components/+page.svelte  # Component showcase/demo page
```

## Component Usage

```svelte
<script>
  import { Button, Card, Header } from '$lib/components';
</script>

<Header
  logoText="My Service"
  showNavigation={true}
  navigationItems={[
    { text: 'Home', href: '/' },
    { text: 'About', href: '/about' }
  ]}
/>

<Card
  heading="Welcome"
  description="This is a card component."
  href="/details"
/>

<Button variant="primary">Save and continue</Button>
```

## Theming

The design system uses a custom DaisyUI theme named "public-good" defined in `src/app.css`. Theme colours are configured using oklch colour space for perceptual uniformity:

- **Primary**: Sky blue (`oklch(68.47% 0.1479 237.32)`)
- **Secondary**: Slate grey
- **Accent**: Amber
- **Info/Success/Warning/Error**: Semantic colours

To customise the theme, edit the `@plugin "daisyui/theme"` block in `src/app.css`.

## Accessibility

Components follow WCAG AA guidelines:

- Semantic HTML elements with proper ARIA attributes
- Keyboard navigation support (arrow keys, tab, enter, escape)
- Screen reader compatible labels and descriptions
- Focus management and visible focus indicators
- `aria-describedby` linking for hints and error messages

## Configuration Files

| File                | Purpose                                   |
| ------------------- | ----------------------------------------- |
| `package.json`      | Dependencies and scripts                  |
| `svelte.config.js`  | SvelteKit configuration with adapter-auto |
| `vite.config.ts`    | Vite build configuration                  |
| `postcss.config.js` | PostCSS with `@tailwindcss/postcss`       |
| `tsconfig.json`     | TypeScript strict configuration           |
| `src/app.css`       | Tailwind CSS + DaisyUI theme              |

## Acknowledgments

- [NHS UK Design System](https://service-manual.nhs.uk/design-system) for the original component designs and accessibility patterns
- [GOV.UK Design System](https://design-system.service.gov.uk/) for design system principles
- [Svelte](https://svelte.dev/), [Tailwind CSS](https://tailwindcss.com/), and [DaisyUI](https://daisyui.com/) communities

## License

MIT License
