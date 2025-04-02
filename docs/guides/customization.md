# Customization Guide

This guide explains how to customize and extend our CSS framework to meet your specific project needs while maintaining its architectural integrity.

## Core Customization Approaches

There are several ways to customize the framework:

1. **CSS Variables**: Override design tokens to change colors, spacing, typography, etc.
2. **Cascade Layers**: Extend existing layers or add new ones to the cascade
3. **Custom Components**: Create new components that follow the established patterns
4. **Utility Extensions**: Add new utility classes to complement the existing set
5. **Theme Variants**: Create alternative themes or modifications of the default theme

## Customizing with CSS Variables

### Overriding Design Tokens

The simplest way to customize the framework is by overriding CSS variables:

```css
:root {
  /* Override color hues */
  --primary-h: 250; /* Change primary/accent color to purple */
  --success-h: 150; /* Adjust success green */
  
  /* Override spacing scale */
  --space-md: 1.25rem; /* Default is 1rem */
  --space-lg: 2rem;    /* Default is 1.5rem */
  
  /* Override typography */
  --font-family-sans: 'Montserrat', sans-serif;
  --font-size-base: 1.125rem; /* Default is 1rem */
  
  /* Override border radius */
  --radius-md: 8px; /* Default is 6px */
}
```

Place these overrides in your own CSS file and load it after the framework.

### Creating Color Themes

You can create custom color themes:

```css
/* Blue Theme */
.theme-blue {
  --primary-h: 220; /* Blue */
  --secondary-h: 280; /* Purple */
  --tertiary-h: 160; /* Teal */
}

/* Green Theme */
.theme-green {
  --primary-h: 160; /* Green */
  --secondary-h: 220; /* Blue */
  --tertiary-h: 40; /* Gold */
}
```

Apply the theme class to your HTML:

```html
<body class="theme-blue">
  <!-- Blue theme applied -->
</body>
```

### Semantic Variable Overrides

You can customize semantic variables without changing the base tokens:

```css
:root {
  /* Use a different token for a semantic variable */
  --text-default: var(--gray-11); /* Instead of gray-10 */
  --surface-default: var(--gray-1); /* Instead of gray-3 */
  
  /* Create higher contrast between surfaces */
  --surface-subtle: var(--gray-3);
  --surface-muted: var(--gray-2);
}
```

This allows you to change the application of colors without modifying the underlying palette.

## Extending with Cascade Layers

### Adding to Existing Layers

You can extend existing layers with your own styles:

```css
@layer components {
  /* Add a new card variant */
  .card--featured {
    border-left: 4px solid var(--accent);
    background: linear-gradient(
      to right,
      var(--accent-subtle),
      var(--surface-default) 20%
    );
  }
  
  /* Add a new alert variant */
  .alert--feature {
    border-left-color: var(--tertiary);
    background-color: var(--tertiary-subtle);
  }
}

@layer utilities {
  /* Add new utility classes */
  .text-truncate {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  
  .aspect-video {
    aspect-ratio: 16 / 9;
  }
}
```

### Adding New Layers

You can add new layers to the cascade:

```css
/* Redefine the cascade order to include your custom layers */
@layer reset, tokens, engine, theme, palette, defaults, components, utilities, layouts, custom-components, overrides;

/* Add your custom layers */
@layer custom-components {
  /* Custom components specific to your project */
  .product-card {
    display: grid;
    grid-template-rows: auto 1fr auto;
    height: 100%;
    /* More styling... */
  }
}

@layer overrides {
  /* Highest specificity overrides for special cases */
  .legacy-component {
    /* Override styles for legacy components */
  }
}
```

## Creating Custom Components

### Component Structure

When creating custom components, follow the established pattern:

```css
@layer components {
  /* Base component */
  .feature-box {
    background-color: var(--surface-default);
    border-radius: var(--radius-lg);
    padding: var(--space-lg);
    box-shadow: var(--shadow-md);
  }
  
  /* Component parts */
  .feature-box__icon {
    color: var(--accent);
    font-size: var(--font-size-2xl);
    margin-bottom: var(--space-sm);
  }
  
  .feature-box__title {
    font-size: var(--font-size-xl);
    font-weight: var(--font-weight-bold);
    color: var(--text-overt);
    margin-bottom: var(--space-xs);
  }
  
  .feature-box__description {
    color: var(--text-default);
  }
  
  /* Component variants */
  .feature-box--compact {
    padding: var(--space-md);
  }
  
  .feature-box--accent {
    background-color: var(--accent-subtle);
    border-left: 4px solid var(--accent);
  }
}
```

### Responsive Components with Container Queries

Create responsive components using container queries:

```css
@layer components {
  .product-card {
    container-type: inline-size;
    container-name: product-card;
    display: grid;
    gap: var(--space-md);
    grid-template-areas:
      "image"
      "content"
      "actions";
  }
  
  .product-card__image {
    grid-area: image;
  }
  
  .product-card__content {
    grid-area: content;
  }
  
  .product-card__actions {
    grid-area: actions;
  }
  
  @container product-card (min-width: 30em) {
    .product-card {
      grid-template-columns: 2fr 3fr;
      grid-template-areas:
        "image content"
        "image actions";
    }
  }
}
```

## Adding Custom Utilities

### Creating Utility Classes

Add your own utility classes to complement the built-in ones:

```css
@layer utilities {
  /* Typography utilities */
  .text-balance { text-wrap: balance; }
  .line-clamp-1 { overflow: hidden; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 1; }
  .line-clamp-2 { overflow: hidden; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 2; }
  .line-clamp-3 { overflow: hidden; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 3; }
  
  /* Animation utilities */
  .animate-fade-in { animation: fade-in var(--animation-duration-normal) var(--ease-out); }
  .animate-slide-up { animation: slide-up var(--animation-duration-normal) var(--ease-out); }
  .animate-pulse { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
  
  /* Transform utilities */
  .scale-hover { transition: transform var(--animation-duration-fast) var(--ease-in-out); }
  .scale-hover:hover { transform: scale(1.05); }
  .rotate-45 { transform: rotate(45deg); }
  .rotate-90 { transform: rotate(90deg); }
  .rotate-180 { transform: rotate(180deg); }
}

@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slide-up {
  from { transform: translateY(1rem); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
```

### Responsive Utilities

Add responsive variants to your utilities:

```css
@layer utilities {
  /* Base utility */
  .hide { display: none; }
  
  /* Responsive variants */
  @media (min-width: 30em) {
    .sm\:hide { display: none; }
    .sm\:show { display: block; }
  }
  
  @media (min-width: 48em) {
    .md\:hide { display: none; }
    .md\:show { display: block; }
  }
  
  @media (min-width: 64em) {
    .lg\:hide { display: none; }
    .lg\:show { display: block; }
  }
}
```

## Creating Theme Variants

### Complete Theme System

You can create a comprehensive theme system:

```css
/* Define the theme variables in the theme layer */
@layer theme {
  /* Default (light) theme */
  :root {
    --base: oklch(var(--scale-l-0) var(--scale-c-1) var(--gray-h));
    --text-default: oklch(var(--scale-l-10) var(--scale-c-2) var(--gray-h));
    /* Other default theme variables */
  }
  
  /* Dark theme */
  .dark, :root.dark, @media (prefers-color-scheme: dark) {
    :root:not(.light) {
      --base: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
      --text-default: oklch(var(--scale-l-2) var(--scale-c-2) var(--gray-h));
      /* Other dark theme variables */
    }
  }
  
  /* High contrast theme */
  .high-contrast, @media (prefers-contrast: more) {
    --contrast-multiplier: 1.2;
    --text-default: oklch(calc(var(--scale-l-12) * var(--contrast-multiplier)) var(--scale-c-2) var(--gray-h));
    /* Other high contrast theme variables */
  }
  
  /* Specific branded themes */
  .theme-blue {
    --primary-h: 220;
    --accent: oklch(var(--scale-l-6) var(--scale-c-7) var(--primary-h));
    /* Other theme customizations */
  }
  
  .theme-green {
    --primary-h: 150;
    --accent: oklch(var(--scale-l-6) var(--scale-c-7) var(--primary-h));
    /* Other theme customizations */
  }
}
```

### Theme Switching

Implement theme switching with JavaScript:

```javascript
// Theme toggle function
function setTheme(themeName) {
  // Remove all theme classes
  document.documentElement.classList.remove(
    'light', 'dark', 'high-contrast', 'theme-blue', 'theme-green'
  );
  
  // Add the selected theme class
  if (themeName !== 'default') {
    document.documentElement.classList.add(themeName);
  }
  
  // Store the preference
  localStorage.setItem('theme', themeName);
}

// Initialize theme on page load
function initTheme() {
  const storedTheme = localStorage.getItem('theme');
  
  if (storedTheme) {
    setTheme(storedTheme);
  } else {
    // Detect system preferences
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      setTheme('dark');
    }
  }
}

// Listen for system preference changes
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
  if (!localStorage.getItem('theme')) {
    setTheme(e.matches ? 'dark' : 'default');
  }
});

// Initialize on page load
document.addEventListener('DOMContentLoaded', initTheme);
```

## Advanced Customization Techniques

### Custom Color System

To completely customize the color system:

```css
@layer tokens {
  :root {
    /* Define custom color hues */
    --brand-blue-h: 210;
    --brand-green-h: 160;
    --brand-purple-h: 270;
    
    /* Define custom lightness and chroma scales */
    --brand-l-scale-0: 0.97;
    --brand-l-scale-1: 0.92;
    /* ... other scale values */
    
    --brand-c-scale-0: 0.03;
    --brand-c-scale-1: 0.06;
    /* ... other scale values */
  }
}

@layer palette {
  :root {
    /* Create your custom color palette */
    --brand-blue-1: oklch(var(--brand-l-scale-0) var(--brand-c-scale-0) var(--brand-blue-h));
    --brand-blue-2: oklch(var(--brand-l-scale-1) var(--brand-c-scale-1) var(--brand-blue-h));
    /* ... other palette colors */
  }
}

@layer theme {
  :root {
    /* Map your custom colors to semantic roles */
    --brand-primary: var(--brand-blue-5);
    --brand-secondary: var(--brand-purple-5);
    --brand-accent: var(--brand-green-5);
    
    /* Override the framework's semantic colors with your brand colors */
    --accent: var(--brand-primary);
    --secondary: var(--brand-secondary);
    --tertiary: var(--brand-accent);
  }
}
```

### Custom Typography Scale

To implement a custom typography scale:

```css
@layer tokens {
  :root {
    /* Define a custom modular scale */
    --type-scale-ratio: 1.2; /* Minor third */
    --font-size-base: 1rem;
    --font-size-xs: calc(var(--font-size-base) / var(--type-scale-ratio) / var(--type-scale-ratio));
    --font-size-sm: calc(var(--font-size-base) / var(--type-scale-ratio));
    --font-size-md: calc(var(--font-size-base) * var(--type-scale-ratio));
    --font-size-lg: calc(var(--font-size-base) * var(--type-scale-ratio) * var(--type-scale-ratio));
    --font-size-xl: calc(var(--font-size-base) * var(--type-scale-ratio) * var(--type-scale-ratio) * var(--type-scale-ratio));
    --font-size-2xl: calc(var(--font-size-base) * var(--type-scale-ratio) * var(--type-scale-ratio) * var(--type-scale-ratio) * var(--type-scale-ratio));
    
    /* Custom font stacks */
    --font-family-sans: 'Roboto', -apple-system, BlinkMacSystemFont, sans-serif;
    --font-family-serif: 'Merriweather', Georgia, serif;
    --font-family-mono: 'Fira Code', monospace;
    
    /* Custom line heights */
    --line-height-tight: 1.2;
    --line-height-normal: 1.6;
    --line-height-relaxed: 1.8;
  }
}
```

### Custom Spacing Scale

To create a custom spacing scale:

```css
@layer tokens {
  :root {
    /* Define a custom spacing scale based on the golden ratio */
    --space-ratio: 1.618; /* Golden ratio */
    --space-base: 1rem;
    --space-3xs: calc(var(--space-base) / var(--space-ratio) / var(--space-ratio) / var(--space-ratio));
    --space-2xs: calc(var(--space-base) / var(--space-ratio) / var(--space-ratio));
    --space-xs: calc(var(--space-base) / var(--space-ratio));
    --space-sm: var(--space-base);
    --space-md: calc(var(--space-base) * var(--space-ratio));
    --space-lg: calc(var(--space-base) * var(--space-ratio) * var(--space-ratio));
    --space-xl: calc(var(--space-base) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio));
    --space-2xl: calc(var(--space-base) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio));
    --space-3xl: calc(var(--space-base) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio) * var(--space-ratio));
  }
}
```

## Best Practices

1. **Respect the Layer System**: Add your customizations to the appropriate cascade layer
2. **Use CSS Variables**: Modify design tokens rather than overriding component styles directly
3. **Follow Naming Conventions**: Maintain consistent naming patterns for your custom additions
4. **Document Your Customizations**: Keep track of your modifications for future reference
5. **Test Across Themes**: Ensure your customizations work in light mode, dark mode, and high contrast mode
6. **Avoid !important**: Let the cascade layers handle specificity instead
7. **Be Mindful of Performance**: Don't add unnecessary styles or complex selectors
8. **Maintain Accessibility**: Ensure your customizations meet accessibility standards
9. **Create Reusable Patterns**: Design custom components and utilities to be reusable
10. **Stay DRY**: Don't repeat styles that could be handled by existing utilities

## Handling Updates

When updating the framework, consider these approaches:

1. **Use Version Control**: Track your customizations separately from the framework
2. **Isolate Customizations**: Keep all your custom styles in separate files
3. **Document Dependencies**: Note which framework features your customizations depend on
4. **Test Thoroughly**: After updating, test your customizations to ensure they still work
5. **Use Feature Detection**: For browser features, use feature detection rather than hard-coding support

## Resources

- [MDN: Using CSS custom properties (variables)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN: Cascade layers (@layer)](https://developer.mozilla.org/en-US/docs/Web/CSS/@layer)
- [CSS Working Group: CSS Custom Properties](https://www.w3.org/TR/css-variables-1/)
- [CSS Working Group: CSS Cascade 5](https://www.w3.org/TR/css-cascade-5/)
- [CSS Tricks: A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)