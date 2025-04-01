# Accessibility Guide

This guide explains the accessibility features of our CSS framework and provides best practices for creating accessible interfaces.

## Core Accessibility Features

### Enhanced Focus States

Our framework includes comprehensive focus state handling:

```css
/* Global focus style for keyboard navigation */
:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

/* Custom focus styles for specific elements */
a:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
  text-decoration: none;
}

.button:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}
```

Key aspects:
- Uses `:focus-visible` to apply focus rings only for keyboard navigation
- Customizable focus ring properties (width, style, color, offset)
- Consistent focus indicators across all interactive elements

### High Contrast Mode Support

The framework automatically adapts to users with high contrast preferences:

```css
@media (prefers-contrast: more) {
  :root {
    /* Increase contrast for text */
    --text-default: oklch(calc(var(--scale-l-12) * var(--contrast-multiplier)) var(--scale-c-2) var(--gray-h));
    --text-muted: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-3) var(--gray-h));
    
    /* Strengthen border contrast */
    --outline-default: oklch(calc(var(--scale-l-8) * var(--contrast-multiplier)) var(--scale-c-4) var(--gray-h));
    
    /* Make focus indicators more visible */
    --focus-ring-width: 3px;
    --focus-ring-style: dashed;
    --focus-ring-color: var(--outline-focus);
  }
}
```

Additional high contrast features:
- Increased color contrast for all text and UI elements
- More prominent borders for better visual separation
- Enhanced focus indicators with thicker outlines

### Auto-Contrast Text

Our Engine layer includes automatic contrast calculation for text:

```css
--auto-contrast-text: oklch(
  from var(--bg, var(--base))
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
);
```

This ensures:
- Text always has sufficient contrast against its background
- Adapts automatically to theme changes and color variants
- Reduces chroma (color intensity) for improved readability

### Screen Reader Utilities

The framework includes utilities for screen reader accessibility:

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}

.not-sr-only {
  position: static;
  width: auto;
  height: auto;
  padding: 0;
  margin: 0;
  overflow: visible;
  clip: auto;
  white-space: normal;
}
```

These utilities allow:
- Adding content visible only to screen readers
- Implementing the "visually hidden" pattern properly

### Reduced Motion Support

The framework respects user motion preferences:

```css
@media (prefers-reduced-motion: reduce) {
  :root {
    --animation-duration-fast: 0.01ms;
    --animation-duration-normal: 0.01ms;
    --animation-duration-slow: 0.01ms;
  }
}
```

This ensures:
- Animations and transitions are minimized for users who prefer reduced motion
- Core functionality remains intact without distracting movements

## Accessibility Best Practices

### Text and Typography

1. **Use relative units**
   - Our framework uses `rem` units for font sizes
   - This ensures text scales with user preferences

   ```css
   .text-base { font-size: var(--font-size-base); /* 1rem */ }
   ```

2. **Maintain sufficient line height**
   - Line heights are set to improve readability
   - Minimum recommended line height of 1.5 for body text

   ```css
   body {
     line-height: var(--line-height-normal); /* 1.5 */
   }
   ```

3. **Ensure adequate text spacing**
   - Letter spacing is appropriate for different text sizes
   - Word spacing allows for clear distinction between words

   ```css
   .tracking-wide { letter-spacing: var(--letter-spacing-wide); }
   ```

### Color and Contrast

1. **Meet minimum contrast requirements**
   - Text meets WCAG 2.1 AA requirements (4.5:1 for normal text, 3:1 for large text)
   - Our auto-contrast system helps maintain these ratios

2. **Don't rely on color alone**
   - Always use additional indicators (icons, text, patterns)
   - For example, error states use both color and icons

   ```html
   <div class="alert alert--error">
     <div class="alert__icon">⚠️</div>
     <div class="alert__content">Error message</div>
   </div>
   ```

3. **Test in different color modes**
   - Check interfaces in light mode, dark mode, and high contrast mode
   - Ensure all states are properly visible in each mode

### Interactive Elements

1. **Use semantic HTML**
   - Prefer native elements (`<button>`, `<a>`, etc.) when possible
   - Add appropriate ARIA attributes when extending functionality

   ```html
   <!-- Correct -->
   <button class="button">Click me</button>
   
   <!-- Avoid -->
   <div class="button" onclick="...">Click me</div>
   ```

2. **Ensure proper focus management**
   - All interactive elements must be keyboard accessible
   - Focus order should follow a logical sequence
   - Use `tabindex="0"` only when absolutely necessary

3. **Provide adequate target sizes**
   - Interactive elements have sufficient padding
   - Minimum touch target size of 44×44px for touch interfaces

   ```css
   .button {
     padding: var(--space-button-y, 0.7em) var(--space-button-x, 1.3em);
     /* Ensures adequate touch target */
   }
   ```

### Forms and Inputs

1. **Use explicit labels**
   - Every form control should have an associated label
   - Labels should be properly connected via the `for` attribute

   ```html
   <div class="form-group">
     <label for="name" class="form-label">Name</label>
     <input id="name" class="form-input" type="text">
   </div>
   ```

2. **Provide clear feedback**
   - Error states are visually distinct and described
   - Success states confirm actions were completed

   ```html
   <div class="form-group">
     <label for="email" class="form-label">Email</label>
     <input id="email" class="form-input form-input--invalid" type="email">
     <span class="form-error">Please enter a valid email address</span>
   </div>
   ```

3. **Group related controls**
   - Use fieldsets and legends for related inputs
   - Organize forms in a logical structure

   ```html
   <fieldset>
     <legend>Contact Information</legend>
     <!-- Form controls here -->
   </fieldset>
   ```

### Images and Media

1. **Always use alt text**
   - Provide descriptive alt text for images
   - Use empty alt (`alt=""`) for decorative images

   ```html
   <img src="chart.png" alt="Sales chart showing 20% growth in Q2">
   ```

2. **Consider color blindness**
   - Don't rely solely on color for data visualization
   - Use patterns, shapes, and labels in addition to color

3. **Ensure media controls are accessible**
   - Audio and video players should have keyboard-accessible controls
   - Provide captions and transcripts when applicable

## Testing for Accessibility

### Automated Testing

1. **Use accessibility linters**
   - Integrate tools like axe, WAVE, or Lighthouse
   - Make accessibility testing part of your CI/CD pipeline

2. **Test with browser extensions**
   - Chrome/Edge: Lighthouse, axe DevTools
   - Firefox: WAVE Evaluation Tool

### Manual Testing

1. **Keyboard navigation testing**
   - Navigate your interface using only the keyboard
   - Ensure focus states are clearly visible
   - Check for logical tab order

2. **Screen reader testing**
   - Test with popular screen readers:
     - NVDA or JAWS (Windows)
     - VoiceOver (macOS)
     - TalkBack (Android)
   - Verify that all content is properly announced

3. **Zoom and magnification**
   - Test at 200% zoom
   - Ensure content remains usable and doesn't overlap

4. **User preference testing**
   - Test with different user preferences:
     - Dark mode
     - High contrast mode
     - Reduced motion
     - Increased font size

## ARIA and Semantic HTML

### Using ARIA Appropriately

1. **Use native elements first**
   - Choose semantic HTML elements when possible
   - Only use ARIA when native semantics are insufficient

2. **Common ARIA patterns**
   - Landmarks: `role="navigation"`, `role="main"`, etc.
   - Live regions: `aria-live="polite"`, `aria-live="assertive"`
   - State indicators: `aria-expanded`, `aria-selected`, etc.

   ```html
   <div role="alert" aria-live="assertive" class="alert alert--error">
     An error occurred during form submission
   </div>
   ```

### Semantic Structure

1. **Use proper headings**
   - Maintain a logical heading hierarchy (h1-h6)
   - Don't skip heading levels

   ```html
   <h1>Page Title</h1>
   <section>
     <h2>Section Title</h2>
     <h3>Subsection Title</h3>
   </section>
   ```

2. **Use landmarks appropriately**
   - `<header>`, `<main>`, `<footer>`, `<nav>`, `<aside>`
   - These help screen reader users navigate your page

   ```html
   <header>
     <nav>
       <!-- Navigation items -->
     </nav>
   </header>
   <main>
     <!-- Main content -->
   </main>
   <footer>
     <!-- Footer content -->
   </footer>
   ```

## Implementing Accessible Components

### Modal Dialogs

```html
<div class="modal" role="dialog" aria-labelledby="modal-title" aria-modal="true">
  <div class="modal__dialog">
    <div class="modal__header">
      <h2 id="modal-title" class="modal__title">Modal Title</h2>
      <button class="modal__close" aria-label="Close">×</button>
    </div>
    <div class="modal__body">
      Modal content
    </div>
    <div class="modal__footer">
      <button class="button">Cancel</button>
      <button class="button button--filled-accent">Confirm</button>
    </div>
  </div>
</div>
```

Key accessibility features:
- `role="dialog"` identifies the component as a dialog
- `aria-labelledby` associates the title with the dialog
- `aria-modal="true"` indicates it's a modal dialog
- Focus management (not shown in CSS) should trap focus inside the modal when open

### Tabs

```html
<div class="l-tabs" role="tablist">
  <div class="l-tabs__list">
    <button id="tab1" class="button" role="tab" aria-selected="true" aria-controls="panel1">Tab 1</button>
    <button id="tab2" class="button" role="tab" aria-selected="false" aria-controls="panel2">Tab 2</button>
    <button id="tab3" class="button" role="tab" aria-selected="false" aria-controls="panel3">Tab 3</button>
  </div>
  <div id="panel1" class="l-tabs__panel" role="tabpanel" aria-labelledby="tab1">
    Tab 1 content
  </div>
  <div id="panel2" class="l-tabs__panel" role="tabpanel" aria-labelledby="tab2" hidden>
    Tab 2 content
  </div>
  <div id="panel3" class="l-tabs__panel" role="tabpanel" aria-labelledby="tab3" hidden>
    Tab 3 content
  </div>
</div>
```

Key accessibility features:
- `role="tablist"`, `role="tab"`, and `role="tabpanel"` establish the tabbed interface
- `aria-selected` indicates the currently selected tab
- `aria-controls` associates tabs with their panels
- `aria-labelledby` associates panels with their tabs
- JavaScript (not shown) should handle keyboard navigation between tabs

### Dropdown Menus

```html
<div class="dropdown">
  <button class="button dropdown__trigger" aria-haspopup="true" aria-expanded="false" id="dropdown-menu">
    Menu
  </button>
  <ul class="dropdown__menu" role="menu" aria-labelledby="dropdown-menu">
    <li role="none">
      <a href="#" role="menuitem">Option 1</a>
    </li>
    <li role="none">
      <a href="#" role="menuitem">Option 2</a>
    </li>
    <li role="none">
      <a href="#" role="menuitem">Option 3</a>
    </li>
  </ul>
</div>
```

Key accessibility features:
- `aria-haspopup="true"` indicates the button controls a popup
- `aria-expanded` reflects the open/closed state
- `role="menu"` and `role="menuitem"` establish the menu structure
- `aria-labelledby` associates the menu with its trigger button
- JavaScript (not shown) should handle keyboard navigation within the menu

## Resources

### WCAG Guidelines
- [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
- [WCAG Quick Reference](https://www.w3.org/WAI/WCAG21/quickref/)

### Testing Tools
- [axe DevTools](https://www.deque.com/axe/)
- [WAVE Evaluation Tool](https://wave.webaim.org/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)

### Screen Readers
- [NVDA](https://www.nvaccess.org/) (Windows, free)
- [JAWS](https://www.freedomscientific.com/products/software/jaws/) (Windows, commercial)
- [VoiceOver](https://www.apple.com/accessibility/mac/vision/) (macOS, built-in)
- [TalkBack](https://support.google.com/accessibility/android/answer/6283677) (Android, built-in)

### Additional Resources
- [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [A11y Project Patterns](https://www.a11yproject.com/patterns/)
- [Inclusive Components](https://inclusive-components.design/)