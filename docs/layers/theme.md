# Theme Layer

The Theme layer assigns semantic meaning to the raw design tokens, creating a cohesive visual language for your application. It bridges the gap between abstract design tokens and their practical application in user interfaces.

## Core Concept

The Theme layer transforms abstract tokens into meaningful semantic variables that communicate their intended use. For example, instead of using a raw color token like `--scale-l-3` directly, you would use a semantic variable like `--text-default` that clearly communicates its purpose.

This layer is where theming capabilities come to life, enabling:
- Dark mode adaptation
- High contrast mode support
- Brand color customization
- Different visual themes

## Key Features

### Semantic Color System

The Theme layer defines semantic color roles that convey purpose rather than appearance:

```css
:root {
  /* Base Surface Colors */
  --base: oklch(var(--scale-l-0) var(--scale-c-1) var(--gray-h));
  --bedrock: oklch(var(--scale-l-1) var(--scale-c-2) var(--gray-h));
  
  /* Surface Colors - Progressive layers of UI */
  --surface-muted: oklch(var(--scale-l-1) var(--scale-c-1) var(--gray-h));
  --surface-subtle: oklch(var(--scale-l-2) var(--scale-c-1) var(--gray-h));
  --surface-default: oklch(var(--scale-l-3) var(--scale-c-2) var(--gray-h));
  --surface-overt: oklch(var(--scale-l-4) var(--scale-c-2) var(--gray-h));
  
  /* Text Colors - For content hierarchy */
  --text-muted: oklch(var(--scale-l-7) var(--scale-c-1) var(--gray-h));
  --text-subtle: oklch(var(--scale-l-8) var(--scale-c-2) var(--gray-h));
  --text-default: oklch(var(--scale-l-10) var(--scale-c-2) var(--gray-h));
  --text-overt: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
  
  /* Outline Colors - For borders and separators */
  --outline-muted: oklch(var(--scale-l-4) var(--scale-c-1) var(--gray-h));
  --outline-subtle: oklch(var(--scale-l-5) var(--scale-c-2) var(--gray-h));
  --outline-default: oklch(var(--scale-l-6) var(--scale-c-2) var(--gray-h));
  --outline-overt: oklch(var(--scale-l-7) var(--scale-c-3) var(--gray-h));
}
```

### Brand Colors

The Theme layer defines key brand colors and their variants:

```css
:root {
  /* Primary Brand Color (Accent) */
  --accent: oklch(var(--scale-l-6) var(--scale-c-7) var(--primary-h));
  --accent-muted: oklch(var(--scale-l-6) var(--scale-c-3) var(--primary-h));
  --accent-subtle: oklch(var(--scale-l-3) var(--scale-c-1) var(--primary-h));
  --accent-overt: oklch(var(--scale-l-5) var(--scale-c-8) var(--primary-h));
  
  /* Secondary Brand Color */
  --secondary: oklch(var(--scale-l-6) var(--scale-c-7) calc(var(--primary-h) + 60));
  --secondary-muted: oklch(var(--scale-l-6) var(--scale-c-3) calc(var(--primary-h) + 60));
  --secondary-subtle: oklch(var(--scale-l-3) var(--scale-c-1) calc(var(--primary-h) + 60));
  --secondary-overt: oklch(var(--scale-l-5) var(--scale-c-8) calc(var(--primary-h) + 60));
  
  /* Tertiary Brand Color */
  --tertiary: oklch(var(--scale-l-6) var(--scale-c-7) calc(var(--primary-h) + 120));
  --tertiary-muted: oklch(var(--scale-l-6) var(--scale-c-3) calc(var(--primary-h) + 120));
  --tertiary-subtle: oklch(var(--scale-l-3) var(--scale-c-1) calc(var(--primary-h) + 120));
  --tertiary-overt: oklch(var(--scale-l-5) var(--scale-c-8) calc(var(--primary-h) + 120));
}
```

### Status Colors

The Theme layer defines colors for different status states:

```css
:root {
  /* Success */
  --success: oklch(var(--scale-l-5) var(--scale-c-7) var(--success-h));
  --text-success: oklch(var(--scale-l-5) var(--scale-c-8) var(--success-h));
  --outline-success: oklch(var(--scale-l-6) var(--scale-c-7) var(--success-h));
  --surface-success: oklch(var(--scale-l-2) var(--scale-c-1) var(--success-h));
  
  /* Warning */
  --warning: oklch(var(--scale-l-5) var(--scale-c-7) var(--warning-h));
  --text-warning: oklch(var(--scale-l-5) var(--scale-c-8) var(--warning-h));
  --outline-warning: oklch(var(--scale-l-6) var(--scale-c-7) var(--warning-h));
  --surface-warning: oklch(var(--scale-l-2) var(--scale-c-1) var(--warning-h));
  
  /* Error */
  --error: oklch(var(--scale-l-5) var(--scale-c-7) var(--error-h));
  --text-error: oklch(var(--scale-l-5) var(--scale-c-8) var(--error-h));
  --outline-error: oklch(var(--scale-l-6) var(--scale-c-7) var(--error-h));
  --surface-error: oklch(var(--scale-l-2) var(--scale-c-1) var(--error-h));
  
  /* Info */
  --info: oklch(var(--scale-l-5) var(--scale-c-7) var(--info-h));
  --text-info: oklch(var(--scale-l-5) var(--scale-c-8) var(--info-h));
  --outline-info: oklch(var(--scale-l-6) var(--scale-c-7) var(--info-h));
  --surface-info: oklch(var(--scale-l-2) var(--scale-c-1) var(--info-h));
}
```

### Interactive States

The Theme layer defines colors for different interactive states:

```css
:root {
  /* Link Colors */
  --text-link: var(--accent);
  --text-link-visited: oklch(var(--scale-l-5) var(--scale-c-6) calc(var(--primary-h) + 30));
  --text-link-hover: var(--accent-overt);
  --text-link-active: oklch(var(--scale-l-4) var(--scale-c-8) var(--primary-h));
  
  /* Focus States */
  --outline-focus: oklch(var(--scale-l-5) var(--scale-c-8) var(--primary-h));
  --outline-active: oklch(var(--scale-l-6) var(--scale-c-9) var(--primary-h));
  
  /* Highlight Colors */
  --text-highlight-subtle: oklch(var(--scale-l-5) var(--scale-c-7) var(--primary-h));
  --text-highlight-overt: oklch(var(--scale-l-4) var(--scale-c-8) var(--primary-h));
  --text-highlight-bg: oklch(var(--scale-l-2) var(--scale-c-3) var(--primary-h));
  --highlight-bg-muted: oklch(var(--scale-l-1) var(--scale-c-1) var(--primary-h));
  --highlight-bg-subtle: oklch(var(--scale-l-2) var(--scale-c-2) var(--primary-h));
  --highlight-bg-overt: oklch(var(--scale-l-3) var(--scale-c-3) var(--primary-h));
}
```

### Enhanced Focus State

The Theme layer includes comprehensive focus state variables for better accessibility:

```css
:root {
  /* Focus Ring Properties */
  --focus-ring-width: 2px;
  --focus-ring-offset: 2px;
  --focus-ring-color: var(--outline-focus);
  --focus-ring-style: solid;
  
  /* Input Focus States */
  --input-focus-ring-width: var(--focus-ring-width);
  --input-focus-ring-offset: 0px;
  --input-focus-bg: oklch(var(--scale-l-1) var(--scale-c-1) var(--primary-h));
}
```

### Dark Mode Support

The Theme layer includes a comprehensive dark mode transformation:

```css
@media (prefers-color-scheme: dark) {
  :root:not(.light) {
    /* Base Surface Colors - Dark Mode */
    --base: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
    --bedrock: oklch(var(--scale-l-11) var(--scale-c-2) var(--gray-h));
    
    /* Surface Colors - Dark Mode */
    --surface-muted: oklch(var(--scale-l-11) var(--scale-c-1) var(--gray-h));
    --surface-subtle: oklch(var(--scale-l-10) var(--scale-c-1) var(--gray-h));
    --surface-default: oklch(var(--scale-l-9) var(--scale-c-2) var(--gray-h));
    --surface-overt: oklch(var(--scale-l-8) var(--scale-c-2) var(--gray-h));
    
    /* Text Colors - Dark Mode */
    --text-muted: oklch(var(--scale-l-5) var(--scale-c-1) var(--gray-h));
    --text-subtle: oklch(var(--scale-l-4) var(--scale-c-2) var(--gray-h));
    --text-default: oklch(var(--scale-l-2) var(--scale-c-2) var(--gray-h));
    --text-overt: oklch(var(--scale-l-0) var(--scale-c-1) var(--gray-h));
    
    /* Other dark mode adaptations... */
  }
}
```

### High Contrast Mode Support

The Theme layer includes adaptations for high contrast mode:

```css
@media (prefers-contrast: more) {
  :root {
    /* High contrast adaptations */
    --contrast-multiplier: 1.2;
    
    /* Increase contrast between elements */
    --text-default: oklch(calc(var(--scale-l-12) * var(--contrast-multiplier)) var(--scale-c-2) var(--gray-h));
    --text-muted: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-3) var(--gray-h));
    
    /* Increase border contrast */
    --outline-default: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-4) var(--gray-h));
    
    /* Strengthen focus indicators */
    --focus-ring-width: 3px;
    --focus-ring-style: dashed;
    
    /* Other high contrast adaptations... */
  }
}
```

## Using the Theme Layer

### In HTML/CSS

The Theme layer's semantic variables should be used throughout your application instead of raw tokens:

```css
.card {
  background-color: var(--surface-default);
  color: var(--text-default);
  border: 1px solid var(--outline-subtle);
  box-shadow: var(--shadow-sm);
}

.card__title {
  color: var(--text-overt);
  border-bottom: 1px solid var(--outline-muted);
}

.card__content {
  color: var(--text-default);
}

.card__action {
  color: var(--accent);
}
```

### Forcing Theme Modes

The Theme layer provides classes to force light or dark mode:

```html
<!-- Force light mode -->
<div class="light">
  This content will always use light mode styling
</div>

<!-- Force dark mode -->
<div class="dark">
  This content will always use dark mode styling
</div>
```

## Customizing the Theme

### Brand Color Customization

To customize brand colors, modify the hue variables:

```css
:root {
  --primary-h: 280; /* Purple accent */
  --secondary-h: 340; /* Complementary color automatically calculated */
}
```

### Creating a Custom Theme

To create a custom theme, extend the Theme layer:

```css
@layer theme {
  .theme-ocean {
    --primary-h: 200; /* Blue */
    --success-h: 170; /* Teal */
    --warning-h: 30; /* Orange */
    --error-h: 350; /* Red */
    --gray-h: 210; /* Cool gray */
    
    /* Customize surface colors for this theme */
    --surface-default: oklch(var(--scale-l-2) var(--scale-c-2) 220);
    
    /* Other theme customizations... */
  }
}
```

## Theme Layer Variables Reference

### Base Colors
- `--base`: The main background color of the application
- `--bedrock`: The base color for containers and sections

### Surface Colors
- `--surface-muted`: The most subtle surface color
- `--surface-subtle`: A slightly more prominent surface
- `--surface-default`: The standard surface color
- `--surface-overt`: The most prominent surface color

### Text Colors
- `--text-muted`: The least important text
- `--text-subtle`: Secondary text
- `--text-default`: Primary text color
- `--text-overt`: The most prominent text
- `--text-link`: For hyperlinks
- `--text-success`/`--text-warning`/`--text-error`/`--text-info`: Status text

### Outline Colors
- `--outline-muted`: The subtlest border
- `--outline-subtle`: Secondary borders
- `--outline-default`: Primary border color
- `--outline-overt`: The most prominent border
- `--outline-focus`: For focus states
- `--outline-success`/`--outline-warning`/`--outline-error`/`--outline-info`: Status borders

### Brand Colors
- `--accent`: Primary brand color
- `--accent-muted`/`--accent-subtle`/`--accent-overt`: Accent variants
- `--secondary`: Secondary brand color
- `--tertiary`: Tertiary brand color

### Status Colors
- `--success`: For success states
- `--warning`: For warning states
- `--error`: For error states
- `--info`: For informational states

### Highlight Colors
- `--highlight-bg-muted`/`--highlight-bg-subtle`/`--highlight-bg-overt`: Background highlights
- `--text-highlight-subtle`/`--text-highlight-overt`: Text highlights

### Focus States
- `--focus-ring-width`: Width of focus outlines
- `--focus-ring-offset`: Space between element and focus outline
- `--focus-ring-color`: Color of focus outlines
- `--focus-ring-style`: Style of focus outlines

## Best Practices

1. **Use Semantic Variables**: Always use semantic variables from the Theme layer rather than raw tokens
2. **Respect Dark Mode**: Test your application in both light and dark modes
3. **Consider Accessibility**: Ensure sufficient contrast in all states
4. **Create Theme Variations**: Use cascade layers to extend the theme for variations
5. **Document Custom Themes**: When creating custom themes, document the color palette and usage guidelines