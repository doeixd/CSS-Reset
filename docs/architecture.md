# CSS Framework Architecture

This document explains the architectural approach of our CSS framework, which leverages CSS cascade layers for a more predictable and maintainable styling system.

## Cascade Layers Overview

Our CSS framework is organized into distinct layers using the `@layer` directive. This creates an explicit cascade order that prevents specificity conflicts and provides a clear mental model for how styles are applied.

Layers are defined in order of increasing specificity:

```css
@layer reset, tokens, engine, theme, palette, defaults, components, utilities, layouts;
```

## Layer Responsibilities

Each layer has a distinct responsibility and role in the cascade:

### 1. Reset Layer
- **Purpose**: Normalize browser defaults with zero specificity
- **Content**: Browser reset styles using `:where()` selectors
- **Specificity**: Zero, allowing easy overrides

### 2. Tokens Layer
- **Purpose**: Define design tokens as CSS variables
- **Content**: Colors, typography, spacing, borders, shadows, etc.
- **Structure**: Raw values without semantic meaning

### 3. Engine Layer
- **Purpose**: Provide color and contrast calculations
- **Content**: Mathematical color transformations and auto-contrast logic
- **Usage**: Powers theme adaptability and accessibility features

### 4. Theme Layer
- **Purpose**: Define semantic color roles and theme variables
- **Content**: Mapping tokens to semantic design roles
- **Features**: Dark mode, high contrast mode, focus states

### 5. Palette Layer
- **Purpose**: Define the complete color palette scales
- **Content**: Color scales for UI elements and data visualization
- **Structure**: Systematic color scales with stepped lightness values

### 6. Defaults Layer
- **Purpose**: Apply default styling to HTML elements
- **Content**: Base typography, form elements, tables, etc.
- **Approach**: Minimal styling with semantic theme variables

### 7. Components Layer
- **Purpose**: Define reusable UI components
- **Content**: Buttons, cards, alerts, navigation, etc.
- **Design**: Self-contained, themable, accessible

### 8. Utilities Layer
- **Purpose**: Provide single-purpose utility classes
- **Content**: Colors, spacing, typography, layout helpers
- **Pattern**: Small, composable classes for rapid development

### 9. Layouts Layer
- **Purpose**: Define layout patterns and structural components
- **Content**: Grid systems, flex layouts, container components
- **Feature**: Container query-based responsive behavior

## File Structure

Each layer is defined in its own file for easier maintenance:

```
src/
├── index.css       # Main entry point defining layers and imports
├── reset.css       # Browser reset styles
├── tokens.css      # Design token definitions
├── engine.css      # Color calculations and functions
├── theme.css       # Semantic color roles and themes
├── palette.css     # Color palette definitions
├── defaults.css    # Default element styling
├── components.css  # Common UI components
├── utilities.css   # Utility classes
└── layouts.css     # Layout patterns and primitives
```

The `index.css` file defines the layer order and imports all other files:

```css
@layer reset, tokens, engine, theme, palette, defaults, components, utilities, layouts;

@import url("reset.css");
@import url("tokens.css");
@import url("engine.css");
@import url("theme.css");
@import url("palette.css");
@import url("defaults.css");
@import url("components.css");
@import url("utilities.css");
@import url("layouts.css");
```

## Cascade Flow

The cascade layers create a deliberate flow of increasing specificity:

1. **Foundation Layers** (reset, tokens, engine)
   - Establish the baseline and design system primitives
   - No visible styles, just the building blocks

2. **System Layers** (theme, palette)
   - Define the visual language and color system
   - Connect tokens to semantic roles

3. **Application Layers** (defaults, components)
   - Apply the visual language to HTML elements and patterns
   - Establish the core look and feel

4. **Override Layers** (utilities, layouts)
   - Provide tools for customization and specific layouts
   - Have the highest specificity for easy application

## Benefits of This Architecture

### 1. Predictable Specificity

- Layer order defeats cascade conflicts, not specificity hacks
- No need for `!important` or complex selectors
- Utilities naturally override components, which override defaults

### 2. Modular Organization

- Each layer has a clear purpose and boundary
- Files can be modified, removed, or replaced independently
- Easier onboarding for new developers

### 3. Performance Optimization

- Individual layers can be loaded or deferred as needed
- Critical CSS can be extracted from foundation layers
- Utilities can be tree-shaken based on usage

### 4. Theming Capability

- Clear separation between tokens and their application
- Themes can be swapped by changing the theme layer
- Design tokens create a single source of truth

## Using This Architecture

### Extending with Custom Styles

When adding custom styles to a project using this framework, you should:

1. Decide which layer is appropriate for your styles
2. Place them in the corresponding layer for proper cascade behavior
3. Use the existing token system and semantic variables

Example:

```css
/* For a custom component */
@layer components {
  .my-custom-component {
    background-color: var(--surface-default);
    color: var(--text-default);
    padding: var(--space-md);
    border-radius: var(--radius-md);
  }
}

/* For a utility class */
@layer utilities {
  .my-custom-utility {
    isolation: isolate;
  }
}
```

### When to Use Each Layer

- **Reset Layer**: Only for global normalization, rarely extended
- **Tokens Layer**: Add new design tokens or variables
- **Engine Layer**: Add new color math or calculated variables
- **Theme Layer**: Add new semantic roles or modes
- **Palette Layer**: Add new color scales or palette extensions
- **Defaults Layer**: Modify default styling of HTML elements
- **Components Layer**: Add new UI components or patterns
- **Utilities Layer**: Add new single-purpose helper classes
- **Layouts Layer**: Add new layout patterns or structures

## Resources

For more information on CSS Cascade Layers:

- [MDN Web Docs: Cascade Layers](https://developer.mozilla.org/en-US/docs/Web/CSS/@layer)
- [CSS Working Group: Cascade Layers Spec](https://www.w3.org/TR/css-cascade-5/#layering)
- [CSS Tricks: A Complete Guide to CSS Cascade Layers](https://css-tricks.com/css-cascade-layers/)