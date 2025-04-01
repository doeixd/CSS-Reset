# Introduction

## Philosophy & Core Principles

Our CSS framework is built on a set of fundamental principles designed to provide a robust foundation for modern web development:

### 1. Progressive Enhancement

The framework embraces progressive enhancement, starting with a solid baseline experience that works for all users, then enhancing it for those with more capable browsers. This ensures that your content remains accessible regardless of the user's device or browser capabilities.

### 2. Cascade Layering

We leverage the CSS `@layer` directive to establish a clear and predictable order of specificity. This prevents specificity conflicts and creates a clear mental model of how styles are applied. Each layer has a distinct responsibility, making the codebase easier to maintain and extend.

### 3. Design Token System

At the core of our framework is a comprehensive design token system implemented with CSS custom properties. This creates a single source of truth for design values, enabling consistent interfaces and simplifying theme customization.

### 4. Modern Color Science

Instead of traditional RGB or HSL, we use the OKLCH color space for its perceptual uniformity and improved color manipulation. This enables more predictable color transformations, better contrast ratios, and more accessible interfaces.

### 5. Accessibility First

Accessibility is not an afterthought but a foundational principle. The framework includes enhanced focus states, high contrast mode support, and automatic contrast calculations to ensure your interfaces are usable by everyone.

### 6. Utility-First Approach

While providing sensible defaults and components, the framework embraces a utility-first methodology for rapid development and consistent design implementation. Utility classes are generated from the design token system, ensuring coherence.

### 7. Component Autonomy

Layout components are designed to be self-contained using container queries rather than viewport-based media queries. This enables truly reusable components that adapt to their container rather than the viewport.

## Key Features

### Zero-Specificity Reset

Our reset layer uses the `:where()` pseudo-class to apply browser normalization with zero specificity, preventing specificity issues common in traditional CSS resets.

### Comprehensive Design Token System

The framework includes a complete design token system covering colors, typography, spacing, shadows, animations, and more, all implemented using CSS custom properties.

### Automatic Contrast Calculation

Text colors automatically adjust based on their background to ensure readability, leveraging OKLCH color math for precise contrast control.

### Enhanced High Contrast Mode

Beyond simply respecting `prefers-contrast`, the framework provides specific optimizations for high contrast scenarios, ensuring usability for users with visual impairments.

### Comprehensive Shadow System

A sophisticated shadow system that adapts to dark mode and high contrast preferences, with consistent naming and behavior.

### Enhanced Focus States

Focus states are designed to be clearly visible in all contexts, with support for focus-visible polyfilling and enhanced keyboard navigation.

### Container Query Support

Layout components use container queries for component-level responsive design, enabling truly reusable and context-aware layouts.

## Design Decisions

### Why CSS Layers?

CSS Cascade Layers (`@layer`) provide a way to organize CSS rules into layers with explicit precedence. This solves the traditional problem of CSS specificity conflicts and creates a more maintainable architecture.

### Why OKLCH Colors?

OKLCH (Oklab Lightness-Chroma-Hue) is a perceptually uniform color space that makes color manipulations more predictable. Unlike traditional RGB or HSL, changes in OKLCH values correspond more closely to how humans perceive color differences.

### Why a Utility-First Approach?

Utility classes offer several advantages:
- Direct mapping to design tokens for consistency
- Reduced need for custom CSS
- More predictable styling without side effects
- Improved performance by reducing style recalculations

### Why Container Queries?

Container queries enable responsive designs based on the size of a component's container rather than the viewport. This makes components more reusable and independent of their context.

## Browser Support

The framework is designed for modern browsers, leveraging features like:
- CSS Custom Properties (Variables)
- CSS Grid and Flexbox
- Container Queries
- OKLCH Color Space

For older browsers, we recommend using appropriate polyfills or fallbacks, though the core functionality will work in any browser that supports CSS custom properties.