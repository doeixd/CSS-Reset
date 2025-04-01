# Dark Mode Guide

This guide explains how our CSS framework implements dark mode and how to work with it effectively in your projects.

## Core Concepts

Our framework includes built-in dark mode support using:

1. **CSS Variables**: Theme colors are defined as variables that change in dark mode
2. **Media Queries**: Automatic detection of user preference via `prefers-color-scheme`
3. **Class Toggle**: Manual control through `.dark` and `.light` classes
4. **Color Space**: OKLCH color space for perceptually uniform color transformations

## Automatic Dark Mode

The framework automatically detects the user's preferred color scheme:

```css
@media (prefers-color-scheme: dark) {
  :root:not(.light) {
    /* Dark mode color variables */
    --base: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
    --bedrock: oklch(var(--scale-l-11) var(--scale-c-2) var(--gray-h));
    --surface-muted: oklch(var(--scale-l-11) var(--scale-c-1) var(--gray-h));
    --surface-subtle: oklch(var(--scale-l-10) var(--scale-c-1) var(--gray-h));
    --surface-default: oklch(var(--scale-l-9) var(--scale-c-2) var(--gray-h));
    --surface-overt: oklch(var(--scale-l-8) var(--scale-c-2) var(--gray-h));
    
    /* Dark mode text colors */
    --text-muted: oklch(var(--scale-l-5) var(--scale-c-1) var(--gray-h));
    --text-subtle: oklch(var(--scale-l-4) var(--scale-c-2) var(--gray-h));
    --text-default: oklch(var(--scale-l-2) var(--scale-c-2) var(--gray-h));
    --text-overt: oklch(var(--scale-l-0) var(--scale-c-1) var(--gray-h));
    
    /* Dark mode outline colors */
    --outline-muted: oklch(var(--scale-l-8) var(--scale-c-1) var(--gray-h));
    --outline-subtle: oklch(var(--scale-l-7) var(--scale-c-2) var(--gray-h));
    --outline-default: oklch(var(--scale-l-6) var(--scale-c-2) var(--gray-h));
    --outline-overt: oklch(var(--scale-l-5) var(--scale-c-3) var(--gray-h));
    
    /* Dark mode shadow color */
    --shadow-color-base: 220 30% 80%;
    
    /* Other dark mode adaptations... */
  }
}
```

The `:not(.light)` selector ensures that dark mode is only applied when the user hasn't explicitly chosen light mode.

## Manual Dark Mode Control

You can manually control dark mode using CSS classes:

```html
<!-- Force dark mode regardless of system preference -->
<div class="dark">
  This content will always use dark mode
</div>

<!-- Force light mode regardless of system preference -->
<div class="light">
  This content will always use light mode
</div>
```

These classes can be applied to any element, including the `<html>` or `<body>` tag to control the entire page:

```html
<html class="dark">
  <!-- Entire page in dark mode -->
</html>
```

## Dark Mode Implementation Details

### Color Inversion Philosophy

Our dark mode doesn't simply invert colors or swap fixed values. Instead, it:

1. Inverts the lightness scale (light colors become dark, dark colors become light)
2. Slightly reduces chroma (color intensity) for better visual comfort
3. Maintains the same hues for color harmony and consistency

### Shadow Adjustments

Shadows work differently in dark mode:

```css
/* Light mode shadow base */
--shadow-color-base: 220 10% 10%;

/* Dark mode shadow base */
--shadow-color-base: 220 30% 80%;
```

In dark mode:
- Shadow colors are lighter rather than darker
- Opacity is adjusted for better visibility
- Spread and blur may be increased slightly

### Focus State Adaptation

Focus states are adapted for better visibility in dark mode:

```css
/* Dark mode focus adjustments */
--focus-ring-color: oklch(var(--scale-l-3) var(--scale-c-8) var(--primary-h));
--focus-ring-offset: 3px;
```

## Working with Dark Mode

### Testing Dark Mode

To effectively test dark mode:

1. **Browser Tools**: Use browser developer tools to toggle dark mode
   - Chrome: DevTools > Rendering > Emulate CSS prefers-color-scheme: dark
   - Firefox: DevTools > 3-dot menu > Settings > Enable dark mode

2. **Manual Toggle**: Add a theme toggle to your application
   ```html
   <button onclick="document.documentElement.classList.toggle('dark')">
     Toggle Dark Mode
   </button>
   ```

3. **System Preference**: Change your operating system's theme setting

### Creating Dark Mode Compatible Components

When building custom components:

1. **Use semantic variables** instead of hard-coded colors
   ```css
   /* Good */
   .custom-component {
     background-color: var(--surface-default);
     color: var(--text-default);
   }
   
   /* Avoid */
   .custom-component {
     background-color: white;
     color: black;
   }
   ```

2. **Adjust shadows appropriately**
   ```css
   .custom-card {
     box-shadow: var(--shadow-md);
     /* Shadow automatically adapts to dark mode */
   }
   ```

3. **Consider contrast for all states**
   ```css
   .custom-button:hover {
     background-color: var(--highlight-bg-subtle);
     /* Uses a variable that adjusts properly in dark mode */
   }
   ```

### Dark Mode Specific Overrides

For cases where you need dark-mode-specific styles:

```css
/* Component with dark mode override */
.special-component {
  background-image: url('light-image.jpg');
}

@media (prefers-color-scheme: dark) {
  :root:not(.light) .special-component {
    background-image: url('dark-image.jpg');
  }
}

/* Or with class-based approach */
.dark .special-component {
  background-image: url('dark-image.jpg');
}
```

### Images and Media in Dark Mode

For images and media that need to adapt to dark mode:

1. **Use SVG with currentColor**
   ```html
   <svg fill="currentColor">
     <!-- SVG will inherit text color which adapts to dark mode -->
   </svg>
   ```

2. **Use the `<picture>` element with `prefers-color-scheme`**
   ```html
   <picture>
     <source srcset="dark-image.jpg" media="(prefers-color-scheme: dark)">
     <img src="light-image.jpg" alt="Description">
   </picture>
   ```

3. **Apply filters to invert images**
   ```css
   @media (prefers-color-scheme: dark) {
     .invertible-image {
       filter: invert(1) hue-rotate(180deg);
     }
   }
   ```

## Implementing a Theme Toggle

### Basic Toggle Implementation

Here's a simple JavaScript implementation for a theme toggle:

```javascript
// Theme toggle function
function toggleTheme() {
  // Check if user has a preference stored
  const currentTheme = localStorage.getItem('theme');
  
  if (currentTheme === 'dark') {
    document.documentElement.classList.remove('dark');
    document.documentElement.classList.add('light');
    localStorage.setItem('theme', 'light');
  } else {
    document.documentElement.classList.remove('light');
    document.documentElement.classList.add('dark');
    localStorage.setItem('theme', 'dark');
  }
}

// Initialize theme on page load
function initTheme() {
  // Check if user has a preference stored
  const storedTheme = localStorage.getItem('theme');
  
  if (storedTheme === 'dark') {
    document.documentElement.classList.add('dark');
  } else if (storedTheme === 'light') {
    document.documentElement.classList.add('light');
  } else {
    // If no preference stored, check system preference
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      document.documentElement.classList.add('dark');
    }
  }
}

// Initialize on page load
document.addEventListener('DOMContentLoaded', initTheme);

// Listen for system preference changes
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
  if (!localStorage.getItem('theme')) {
    if (e.matches) {
      document.documentElement.classList.add('dark');
      document.documentElement.classList.remove('light');
    } else {
      document.documentElement.classList.add('light');
      document.documentElement.classList.remove('dark');
    }
  }
});
```

### Toggle Button HTML

```html
<button class="theme-toggle" onclick="toggleTheme()" aria-label="Toggle dark mode">
  <span class="theme-toggle__icon theme-toggle__icon--light">☀️</span>
  <span class="theme-toggle__icon theme-toggle__icon--dark">🌙</span>
</button>
```

### Toggle Button CSS

```css
.theme-toggle {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: var(--radius-full);
  color: var(--text-default);
}

.theme-toggle:hover {
  background-color: var(--surface-subtle);
}

.theme-toggle__icon--dark {
  display: none;
}

.theme-toggle__icon--light {
  display: inline;
}

.dark .theme-toggle__icon--dark {
  display: inline;
}

.dark .theme-toggle__icon--light {
  display: none;
}
```

## Advanced Dark Mode Topics

### Color Theory in Dark Mode

When designing for dark mode, consider these principles:

1. **Reduce saturation**: Colors appear more vibrant on dark backgrounds, so reduce saturation
2. **Increase contrast carefully**: Too much contrast can cause eye strain
3. **Avoid pure black**: Use dark grays instead of pure black for better readability
4. **Reduce blue light**: Consider slightly warming dark backgrounds

Our framework handles these automatically through the OKLCH color adjustments.

### Handling User Preferences and Defaults

When implementing dark mode, consider these scenarios:

1. **System preference**: Respect the user's system preference initially
2. **User override**: Allow users to override the system preference
3. **Per-page preference**: Consider whether theme should be remembered globally or per page
4. **Time-based switching**: Consider automatically switching based on time of day

### Transition Effects

To create a smooth transition between light and dark modes:

```css
:root {
  --base: oklch(var(--scale-l-0) var(--scale-c-1) var(--gray-h));
  /* Other light mode variables... */
  
  transition: color 0.3s ease, background-color 0.3s ease, border-color 0.3s ease, outline-color 0.3s ease;
}

@media (prefers-color-scheme: dark) {
  :root:not(.light) {
    --base: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
    /* Other dark mode variables... */
  }
}

/* Or for class-based approach */
.dark {
  --base: oklch(var(--scale-l-12) var(--scale-c-1) var(--gray-h));
  /* Other dark mode variables... */
}

/* Disable transitions for users who prefer reduced motion */
@media (prefers-reduced-motion: reduce) {
  :root {
    transition: none;
  }
}
```

## Performance and Optimization

### Reducing Flash of Incorrect Theme

To prevent a flash of incorrect theme (FOIT), you can use:

1. **Early theme detection**:
   ```html
   <script>
     // Inline script in the <head> to set theme before page renders
     const theme = localStorage.getItem('theme') || 
                  (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
     document.documentElement.classList.add(theme);
   </script>
   ```

2. **CSS-only approach** (no stored preference):
   ```html
   <style>
     @media (prefers-color-scheme: dark) {
       :root:not(.light) {
         /* Critical dark mode variables */
         --base: #121212;
         --text-default: #e0e0e0;
       }
     }
   </style>
   ```

### Minimize Repaints

Dark mode can cause performance issues if not implemented carefully:

1. **Only transition necessary properties**:
   ```css
   /* Better performance */
   :root {
     transition: color 0.3s ease, background-color 0.3s ease;
   }
   
   /* Avoid */
   :root {
     transition: all 0.3s ease;
   }
   ```

2. **Use hardware-accelerated properties**:
   ```css
   /* Use transform and opacity for transitions where possible */
   .card {
     transition: transform 0.3s ease, opacity 0.3s ease;
   }
   ```

## Best Practices

1. **Use semantic color variables** rather than direct color values
2. **Test both modes thoroughly** for contrast and readability
3. **Respect user preferences** by checking `prefers-color-scheme`
4. **Allow manual override** through a theme toggle
5. **Ensure smooth transitions** between modes when switching
6. **Consider accessibility** in both light and dark modes
7. **Test with actual users** to ensure your dark mode is comfortable
8. **Provide context-appropriate imagery** for each mode
9. **Use CSS custom properties** for dynamic theme switching
10. **Keep color systems consistent** between modes