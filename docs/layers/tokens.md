# Tokens Layer

The Tokens layer defines the fundamental design values of the system as CSS custom properties (variables). These tokens serve as the building blocks for the entire framework, creating a single source of truth for design values.

## Core Concept

Design tokens are named entities that store visual design attributes. They help create and maintain a scalable and consistent visual system for UI development. In our framework, tokens are implemented as CSS custom properties without any semantic meaning - they are raw values that get assigned semantic meaning in the Theme layer.

## Token Categories

### Color Tokens

Color tokens define the base colors used throughout the system:

```css
/* Base Color Hues */
--primary-h: 220;    /* Primary color hue (blue) */
--success-h: 160;    /* Success color hue (green) */
--warning-h: 35;     /* Warning color hue (amber) */
--error-h: 355;      /* Error color hue (red) */
--info-h: 200;       /* Info color hue (cyan) */
--gray-h: 220;       /* Gray color hue (cool gray) */
--neutral-h: 0;      /* Neutral gray hue (true gray) */

/* Base Lightness Scale */
--scale-l-0: 0.98;   /* Lightest value */
--scale-l-1: 0.95;
--scale-l-2: 0.90;
--scale-l-3: 0.85;
--scale-l-4: 0.78;
--scale-l-5: 0.70;
--scale-l-6: 0.60;
--scale-l-7: 0.50;
--scale-l-8: 0.40;
--scale-l-9: 0.32;
--scale-l-10: 0.25;
--scale-l-11: 0.18;
--scale-l-12: 0.10;  /* Darkest value */

/* Base Chroma Scale */
--scale-c-1: 0.02;
--scale-c-2: 0.04;
--scale-c-3: 0.06;
--scale-c-4: 0.08;
--scale-c-5: 0.10;
--scale-c-6: 0.12;
--scale-c-7: 0.14;
--scale-c-8: 0.16;
--scale-c-9: 0.18;
```

### Typography Tokens

Typography tokens define text styles and properties:

```css
/* Font Families */
--font-family-sans: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
--font-family-serif: ui-serif, Georgia, Cambria, 'Times New Roman', Times, serif;
--font-family-mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace;

/* Font Sizes */
--font-size-xs: 0.75rem;
--font-size-sm: 0.875rem;
--font-size-base: 1rem;
--font-size-md: 1.125rem;
--font-size-lg: 1.25rem;
--font-size-xl: 1.5rem;
--font-size-2xl: 1.75rem;
--font-size-3xl: 2rem;
--font-size-4xl: 2.5rem;

/* Font Weights */
--font-weight-thin: 100;
--font-weight-extra-light: 200;
--font-weight-light: 300;
--font-weight-normal: 400;
--font-weight-medium: 500;
--font-weight-semibold: 600;
--font-weight-bold: 700;
--font-weight-extra-bold: 800;
--font-weight-black: 900;

/* Line Heights */
--line-height-none: 1;
--line-height-tight: 1.25;
--line-height-snug: 1.375;
--line-height-normal: 1.5;
--line-height-relaxed: 1.625;
--line-height-loose: 2;

/* Letter Spacing */
--letter-spacing-tighter: -0.05em;
--letter-spacing-tight: -0.025em;
--letter-spacing-normal: 0em;
--letter-spacing-wide: 0.025em;
--letter-spacing-wider: 0.05em;
--letter-spacing-widest: 0.1em;
```

### Spacing Tokens

Spacing tokens define the whitespace system:

```css
/* Spacing Scale */
--space-0: 0;
--space-px: 1px;
--space-xs: 0.25rem;  /* 4px */
--space-sm: 0.5rem;   /* 8px */
--space-md: 1rem;     /* 16px */
--space-lg: 1.5rem;   /* 24px */
--space-xl: 2rem;     /* 32px */
--space-2xl: 3rem;    /* 48px */
--space-3xl: 4rem;    /* 64px */
```

### Border Tokens

Border tokens define border styles, widths, and radii:

```css
/* Border Widths */
--border-width-none: 0;
--border-width-thin: 1px;
--border-width: 2px;
--border-width-thick: 3px;

/* Border Radii */
--radius-none: 0;
--radius-sm: 0.125rem;  /* 2px */
--radius-md: 0.25rem;   /* 4px */
--radius-lg: 0.5rem;    /* 8px */
--radius-xl: 1rem;      /* 16px */
--radius-full: 9999px;
```

### Shadow Tokens

Shadow tokens define the elevation system:

```css
/* Shadow Color Base using HSL format for easier adjustments */
--shadow-color-base: 220 10% 10%;
--shadow-color-dark: 220 20% 90%;

/* Light Mode Shadows */
--shadow-sm: 0 1px 2px oklch(from hsl(var(--shadow-color-base)) l c h / 7%),
             0 1px 1px oklch(from hsl(var(--shadow-color-base)) l c h / 4%);

--shadow-md: 0 4px 6px oklch(from hsl(var(--shadow-color-base)) l c h / 7%),
             0 2px 4px oklch(from hsl(var(--shadow-color-base)) l c h / 4%);

--shadow-lg: 0 10px 15px oklch(from hsl(var(--shadow-color-base)) l c h / 8%),
             0 4px 6px oklch(from hsl(var(--shadow-color-base)) l c h / 5%);

--shadow-xl: 0 20px 25px oklch(from hsl(var(--shadow-color-base)) l c h / 10%),
             0 8px 10px oklch(from hsl(var(--shadow-color-base)) l c h / 6%);

--shadow-inner: inset 0 2px 4px oklch(from hsl(var(--shadow-color-base)) l c h / 6%);
```

### Z-Index Tokens

Z-index tokens define the stacking order:

```css
--z-index-0: 0;
--z-index-10: 10;
--z-index-20: 20;
--z-index-30: 30;
--z-index-40: 40;
--z-index-50: 50;
--z-index-auto: auto;
```

### Animation Tokens

Animation tokens define timing and easing:

```css
/* Animation Timing */
--animation-duration-fast: 150ms;
--animation-duration-normal: 300ms;
--animation-duration-slow: 500ms;

/* Easing Functions */
--ease-linear: linear;
--ease-in: cubic-bezier(0.4, 0, 1, 1);
--ease-out: cubic-bezier(0, 0, 0.2, 1);
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
```

### Opacity Tokens

Opacity tokens define transparency levels:

```css
--alpha-0: 0;
--alpha-1: 0.05;
--alpha-2: 0.1;
--alpha-3: 0.2;
--alpha-4: 0.4;
--alpha-5: 0.6;
--alpha-6: 0.75;
--alpha-7: 0.8;
--alpha-8: 0.9;
--alpha-9: 0.95;
--alpha-10: 1;
```

### Container Query Breakpoints

Tokens for container query breakpoints:

```css
--cq-bp-xs: 20em;  /* 320px */
--cq-bp-sm: 30em;  /* 480px */
--cq-bp-md: 45em;  /* 720px */
--cq-bp-lg: 60em;  /* 960px */
--cq-bp-xl: 75em;  /* 1200px */
```

## Advanced Token Features

### Token Registration with @property

Some tokens use the `@property` CSS at-rule to define proper inheritance and interpolation behavior:

```css
@property --accent-h {
  syntax: "<number>";
  initial-value: 220;
  inherits: true;
}
```

This ensures that tokens are interpolated correctly during animations and transitions, particularly important for color tokens.

### Color Palette Calculations

The Tokens layer includes base calculations for systematic color palette generation:

```css
/* Delta Values for systematic modifications */
--l-delta-1-up: 0.05;
--l-delta-2-up: 0.10;
--l-delta-3-up: 0.15;
--l-delta-1-down: -0.05;
--l-delta-2-down: -0.10;
--l-delta-3-down: -0.15;

/* Chroma Constraints */
--clamp-max-c-0: 0.03;  /* Max chroma for near-whites */
--clamp-max-c-12: 0.04; /* Max chroma for near-blacks */
```

## Using Tokens

Tokens should never be used directly in your HTML. Instead:

1. Use them to build semantic variables in the Theme layer
2. Use them in custom component definitions
3. Reference them in utility classes

For example, instead of:

```html
<!-- DON'T do this -->
<div style="padding: var(--space-md); color: oklch(var(--scale-l-12) var(--scale-c-9) var(--primary-h));">
  Content
</div>
```

Do this:

```html
<!-- DO this instead -->
<div class="p-md text-default bg-surface-subtle">
  Content
</div>
```

## Extending Tokens

To add new tokens to the system:

1. Add them to the Tokens layer
2. Follow the existing naming conventions
3. Create corresponding semantic variables in the Theme layer

Example:

```css
@layer tokens {
  :root {
    /* Custom icon size tokens */
    --icon-size-sm: 1rem;
    --icon-size-md: 1.5rem;
    --icon-size-lg: 2rem;
  }
}

@layer theme {
  :root {
    /* Semantic usage of the tokens */
    --icon-navigation: var(--icon-size-md);
    --icon-button: var(--icon-size-sm);
    --icon-hero: var(--icon-size-lg);
  }
}
```

## Design Token Philosophy

Our tokens follow these principles:

1. **Abstraction**: Tokens are abstracted from their application
2. **Consistency**: Tokens provide a consistent system of values
3. **Scalability**: Tokens can be extended without breaking existing patterns
4. **Clarity**: Token names clearly communicate their purpose and value
5. **Composability**: Tokens can be combined to create more complex values

By adhering to these principles, the token system enables a consistent, maintainable, and scalable design language.