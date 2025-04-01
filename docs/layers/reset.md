# Reset Layer

The Reset layer forms the foundation of our CSS framework, ensuring consistent rendering across browsers by neutralizing default browser styles.

## Core Concept

Unlike traditional CSS resets or normalizers, our Reset layer uses the `:where()` pseudo-class to apply styles with zero specificity. This innovative approach ensures that reset styles won't interfere with your custom styles, avoiding the specificity issues common in other CSS resets.

## Features

### Zero-Specificity Reset

All selectors are wrapped in `:where()` to ensure they have no specificity weight:

```css
:where(*, *::before, *::after) {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

This means any style you define elsewhere will automatically override the reset styles without needing specificity hacks.

### Box Model Normalization

The Reset layer standardizes the box model using `box-sizing: border-box` for all elements, making layout calculations more intuitive and predictable.

### Typography Reset

Base typography is normalized to create a consistent foundation:

- Font sizes are set to use relative units
- Line heights are standardized
- Font families are inherited properly

### Form Element Normalization

Form elements are notoriously inconsistent across browsers:

- Input styles are normalized (borders, padding, etc.)
- Buttons are reset to have consistent behavior
- Select elements and other form controls are standardized

### List Reset

Lists (ul, ol) have their default styling removed:

- No default padding or margin
- No default list-style
- Consistent spacing behavior

### Table Reset

Tables are normalized for more predictable behavior:

- Border-collapse set to a consistent value
- Cell spacing and padding normalized
- Table layout optimized for common use cases

### Media Elements

Image, video, and other media elements are set to behave more predictably:

- `max-width: 100%` for responsive behavior by default
- Appropriate display properties
- Eliminated default margins and alignment issues

### Accessibility Considerations

The Reset layer is careful not to remove styles that aid accessibility:

- Focus states are preserved (not removed)
- Screen reader-only content handling is included
- Default interactive behaviors are maintained

## Using the Reset Layer

The Reset layer is meant to be used as-is without modification in most cases. It's the foundation that other layers build upon.

### When to Customize

You should rarely need to modify the Reset layer, but there are cases where you might:

- If you're supporting legacy browsers with specific normalization needs
- If you're working in a highly specialized domain with unique default style requirements
- If you have specific accessibility requirements that need foundational changes

### How to Extend

If you need to extend the Reset layer, make sure to:

1. Maintain the zero-specificity approach using `:where()`
2. Focus only on normalizing browser defaults, not adding new styles
3. Document your changes thoroughly, especially browser-specific fixes

```css
@layer reset {
  :where(your-new-selector) {
    /* Your reset properties */
  }
}
```

## Complete Reference

Here's what the Reset layer addresses:

### Box Model

- `box-sizing: border-box` for all elements
- Margin and padding reset to zero
- Border-width normalized

### Typography

- Font inheritance setup
- Line-height normalization
- Font-size baseline
- Text-decoration handling
- Vertical alignment fixes

### Lists

- List-style removal
- List spacing normalization
- Nested list behavior

### Tables

- Border-collapse setting
- Table layout properties
- Cell spacing and borders

### Forms

- Button appearance normalization
- Input styling consistency
- Form element inheritance properties
- Legend and fieldset fixes

### Media

- Image, video responsive defaults
- SVG normalization
- Media element alignment
- Max-width behavior

### Miscellaneous

- Hidden element handling
- Horizontal rule normalization
- Quote styling
- Code and pre element fixes

## Browser Support

The Reset layer is designed to work in all modern browsers, with careful consideration for:

- Chrome, Firefox, Safari, Edge (latest versions)
- Mobile browsers
- IE11 (with some polyfills)

For older browsers, additional normalization may be required through polyfills or supplementary CSS.