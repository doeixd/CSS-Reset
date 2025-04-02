# High Contrast Mode Guide

This guide explains how our CSS framework supports high contrast mode, an important accessibility feature that helps users with low vision or visual impairments.

## Core Concepts

High contrast mode is designed to improve readability by:

1. **Increasing color contrast** between foreground and background elements
2. **Simplifying color palettes** to reduce visual complexity
3. **Emphasizing borders and outlines** to better delineate UI elements
4. **Removing subtle visual effects** that may reduce visibility

Our framework supports high contrast mode through:
- Media query detection via `prefers-contrast`
- Increased contrast token adjustments
- Enhanced focus states and borders
- Removed or simplified background patterns and gradients

## Automatic High Contrast Detection

The framework automatically detects when a user prefers high contrast:

```css
@media (prefers-contrast: more) {
  :root {
    /* High contrast mode variables */
    --contrast-multiplier: 1.2;
    
    /* Increase text contrast */
    --text-default: oklch(calc(var(--scale-l-12) * var(--contrast-multiplier)) var(--scale-c-2) var(--gray-h));
    --text-muted: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-3) var(--gray-h));
    
    /* Increase border contrast */
    --outline-default: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-4) var(--gray-h));
    --outline-subtle: oklch(calc(var(--scale-l-7) * var(--contrast-multiplier)) var(--scale-c-3) var(--gray-h));
    
    /* Strengthen focus indicators */
    --focus-ring-width: 3px;
    --focus-ring-style: dashed;
    --focus-ring-color: var(--outline-focus);
    
    /* Increase shadow contrast */
    --shadow-color-base: 220 35% 10%;
    
    /* Other high contrast adaptations... */
  }
}
```

## High Contrast Implementation Details

### Color Contrast Enhancement

In high contrast mode, we make several key adjustments to colors:

1. **Increased lightness differential** between text and backgrounds
2. **Slightly increased chroma** (color intensity) for better differentiation
3. **Simplified color palettes** to focus on core visual distinctions
4. **Bolder borders** around interactive elements

### Focus State Enhancement

Focus states are significantly enhanced in high contrast mode:

```css
@media (prefers-contrast: more) {
  :root {
    /* Enhanced focus states */
    --focus-ring-width: 3px;
    --focus-ring-style: dashed;
    --focus-ring-offset: 3px;
  }
  
  /* Add outlines to additional elements */
  button:focus-visible, 
  a:focus-visible, 
  input:focus-visible, 
  select:focus-visible, 
  textarea:focus-visible {
    outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
    outline-offset: var(--focus-ring-offset);
  }
}
```

### Border and Outline Enhancements

In high contrast mode, borders and outlines are enhanced:

```css
@media (prefers-contrast: more) {
  /* Add borders to elements that might not have them normally */
  .card, .alert, .badge {
    border: 2px solid var(--outline-default);
  }
  
  /* Ensure all inputs have visible borders */
  input, select, textarea {
    border-width: 2px;
  }
  
  /* Add borders to interactive elements */
  button, .button, a.nav__link, summary {
    outline: 1px solid currentColor;
    outline-offset: -1px;
  }
}
```

### Pattern and Background Simplification

In high contrast mode, we simplify backgrounds and patterns:

```css
@media (prefers-contrast: more) {
  /* Remove subtle background patterns */
  .pattern-bg {
    background-image: none;
  }
  
  /* Increase contrast of alternating rows */
  tr:nth-child(even) {
    background-color: var(--surface-overt);
  }
  
  /* Simplify gradient backgrounds */
  .gradient-bg {
    background-image: none;
    background-color: var(--surface-default);
  }
}
```

## Working with High Contrast Mode

### Testing High Contrast Mode

To effectively test high contrast mode:

1. **Browser Support**: 
   - Currently, the `prefers-contrast` media feature is supported in Firefox and Safari
   - For browsers without support, simulate it by adding a `.high-contrast` class

2. **System Settings**:
   - Windows: Settings > Ease of Access > High Contrast
   - macOS: System Preferences > Accessibility > Display > Increase Contrast

3. **Manual Testing**:
   - Add a class to force high contrast mode regardless of system preference
   ```html
   <div class="high-contrast">
     <!-- Content with forced high contrast mode -->
   </div>
   ```

### Design Considerations for High Contrast

When designing with high contrast in mind:

1. **Avoid relying solely on color** to convey information
2. **Use strong borders** around interactive elements
3. **Ensure sufficient spacing** between elements
4. **Test text on various backgrounds** to ensure readability
5. **Consider text size and font weight** for improved readability

### High Contrast Compatible Components

When building custom components:

1. **Use semantic variables** that will adapt to high contrast mode
   ```css
   /* Good */
   .custom-component {
     border-color: var(--outline-default);
   }
   
   /* Avoid */
   .custom-component {
     border-color: rgba(0, 0, 0, 0.1);
   }
   ```

2. **Consider interaction states**
   ```css
   .custom-button:hover {
     background-color: var(--highlight-bg-subtle);
     /* Uses a variable that adjusts properly in high contrast mode */
   }
   ```

3. **Don't rely on subtle differences**
   ```css
   /* Better for high contrast mode */
   .status-indicator {
     color: var(--text-default);
     border: 2px solid currentColor;
   }
   
   /* Instead of */
   .status-indicator {
     color: var(--text-subtle);
     background-color: var(--surface-subtle);
   }
   ```

### High Contrast Specific Overrides

For cases where you need high-contrast-specific styles:

```css
/* Component with high contrast override */
.subtle-card {
  box-shadow: var(--shadow-sm);
  border: 1px solid transparent;
}

@media (prefers-contrast: more) {
  .subtle-card {
    box-shadow: none;
    border: 2px solid var(--outline-default);
  }
}
```

## Implementing a High Contrast Toggle

While high contrast mode should primarily respect system settings, you can offer a manual toggle for testing or user preference:

```javascript
// High contrast toggle function
function toggleHighContrast() {
  document.documentElement.classList.toggle('high-contrast');
  localStorage.setItem('highContrast', document.documentElement.classList.contains('high-contrast'));
}

// Initialize high contrast setting on page load
function initHighContrast() {
  const storedPreference = localStorage.getItem('highContrast');
  
  if (storedPreference === 'true') {
    document.documentElement.classList.add('high-contrast');
  }
}

// Initialize on page load
document.addEventListener('DOMContentLoaded', initHighContrast);
```

```css
/* CSS for high contrast class */
.high-contrast {
  --contrast-multiplier: 1.2;
  --text-default: oklch(calc(var(--scale-l-12) * var(--contrast-multiplier)) var(--scale-c-2) var(--gray-h));
  --text-muted: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-3) var(--gray-h));
  /* Other high contrast variable overrides */
}
```

### Toggle Button HTML

```html
<button class="contrast-toggle" onclick="toggleHighContrast()" aria-label="Toggle high contrast mode">
  <span class="contrast-toggle__icon">🔍</span>
  <span class="contrast-toggle__text">High Contrast</span>
</button>
```

## Integration with Other Accessibility Features

### High Contrast with Dark Mode

Consider the interaction between high contrast mode and dark mode:

```css
/* High contrast mode in light theme */
@media (prefers-contrast: more) {
  :root:not(.dark) {
    /* Light theme high contrast variables */
  }
}

/* High contrast mode in dark theme */
@media (prefers-contrast: more) {
  .dark, :root.dark {
    /* Dark theme high contrast variables */
  }
}

/* Force high contrast in light theme */
.high-contrast:not(.dark) {
  /* Light theme high contrast variables */
}

/* Force high contrast in dark theme */
.dark.high-contrast {
  /* Dark theme high contrast variables */
}
```

### High Contrast with Reduced Motion

Users who prefer high contrast may also prefer reduced motion:

```css
@media (prefers-contrast: more) and (prefers-reduced-motion: reduce) {
  :root {
    /* Combined high contrast and reduced motion variables */
    --transition-duration-standard: 0.01ms;
    --focus-ring-style: solid;
  }
}
```

## Best Practices

1. **Test with actual users** who rely on high contrast mode
2. **Use the right semantic HTML elements** to ensure proper behavior
3. **Don't disable high contrast mode** unless absolutely necessary
4. **Maintain color meaning** even in monochrome high contrast
5. **Provide sufficient information** beyond just color differences
6. **Test keyboard navigation** in high contrast mode
7. **Check color contrast ratios** to ensure WCAG compliance (minimum 4.5:1 for normal text)
8. **Consider printability** of high contrast styles
9. **Add borders to adjacent elements** of the same color
10. **Use patterns along with colors** for data visualization

## Additional Resources

- [WCAG Contrast Guidelines](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [Microsoft High Contrast Documentation](https://docs.microsoft.com/en-us/windows/apps/design/accessibility/high-contrast-mode)
- [MDN prefers-contrast Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-contrast)