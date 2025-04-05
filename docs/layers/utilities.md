# Utilities Layer

The Utilities layer provides single-purpose utility classes for quickly applying specific styles directly in your HTML. These utility classes form a powerful system for rapid development, fine-tuning designs, and creating consistent interfaces without writing custom CSS.

## Core Concept

Utility classes follow a functional CSS approach, where each class does one thing and does it well. This creates a highly composable system where complex designs can be built by combining multiple small, focused classes.

Unlike the Components layer (which provides pre-designed patterns), the Utilities layer provides atomic building blocks that can be combined in countless ways to implement custom designs without writing new CSS.

## Key Features

### Design Token Mapping

Utility classes directly map to the design tokens defined in the Tokens layer, ensuring consistency with the design system:

```css
/* Spacing utility classes map to spacing tokens */
.m-0 { margin: var(--space-0); }
.m-xs { margin: var(--space-xs); }
.m-sm { margin: var(--space-sm); }
.m-md { margin: var(--space-md); }
/* ... */

/* Typography utility classes map to typography tokens */
.text-xs { font-size: var(--font-size-xs); }
.text-sm { font-size: var(--font-size-sm); }
.text-base { font-size: var(--font-size-base); }
.text-lg { font-size: var(--font-size-lg); }
/* ... */
```

### High Specificity

The Utilities layer has the highest specificity in the cascade (except for Layouts), allowing utility classes to override styles from the Components and Defaults layers:

```css
@layer reset, tokens, engine, theme, palette, defaults, components, utilities, layouts;
```

This means you can easily adjust component styles without having to write additional CSS.

### Consistent Naming Convention

Utility classes follow a consistent naming convention:

- `property-value` format (e.g., `text-lg`, `m-md`)
- Abbreviated property names for common properties (e.g., `bg` for background-color)
- Full property names for less common properties (e.g., `opacity`)
- Direction modifiers for spacing and positioning (e.g., `mt` for margin-top)

## Utility Categories

### Color Utilities

#### Background Colors

Theme role background colors:

```css
.bg-base { background-color: var(--base); }
.bg-bedrock { background-color: var(--bedrock); }
.bg-surface-muted { background-color: var(--surface-muted); }
.bg-surface-subtle { background-color: var(--surface-subtle); }
.bg-surface-default { background-color: var(--surface-default); }
.bg-surface-overt { background-color: var(--surface-overt); }
.bg-accent { background-color: var(--accent); }
.bg-secondary { background-color: var(--secondary); }
.bg-tertiary { background-color: var(--tertiary); }
.bg-success { background-color: var(--success); }
.bg-warning { background-color: var(--warning); }
.bg-error { background-color: var(--error); }
.bg-info { background-color: var(--info); }
.bg-transparent { background-color: transparent; }
```

Palette scale background colors:

```css
.bg-gray-0 { background-color: var(--gray-0); }
.bg-gray-1 { background-color: var(--gray-1); }
/* ... through .bg-gray-12 */

.bg-blue-0 { background-color: var(--blue-0); }
/* ... */
.bg-blue-12 { background-color: var(--blue-12); }

/* ... similar classes for all color scales */
```

#### Text Colors

Theme role text colors:

```css
.text-muted { color: var(--text-muted); }
.text-subtle { color: var(--text-subtle); }
.text-default { color: var(--text-default); }
.text-overt { color: var(--text-overt); }
.text-link { color: var(--text-link); }
.text-success { color: var(--text-success); }
.text-warning { color: var(--text-warning); }
.text-error { color: var(--text-error); }
.text-info { color: var(--text-info); }
.text-inherit { color: inherit; }
```

Contrast text colors:

```css
.text-contrast-on-base { --bg: var(--base); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); }
.text-contrast-on-accent { --bg: var(--accent); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); }
/* ... similar classes for other backgrounds */
```

Palette scale text colors:

```css
.text-gray-0 { color: var(--gray-0); }
.text-gray-1 { color: var(--gray-1); }
/* ... through .text-gray-12 */

/* ... similar classes for all color scales */
```

#### Border Colors

Theme role border colors:

```css
.border-outline-muted { border-color: var(--outline-muted); }
.border-outline-subtle { border-color: var(--outline-subtle); }
.border-outline-default { border-color: var(--outline-default); }
.border-outline-overt { border-color: var(--outline-overt); }
.border-accent { border-color: var(--accent); }
.border-success { border-color: var(--outline-success); }
.border-warning { border-color: var(--outline-warning); }
.border-error { border-color: var(--outline-error); }
.border-info { border-color: var(--outline-info); }
.border-transparent { border-color: transparent; }
```

### Spacing Utilities

#### Margin

```css
/* All sides */
.m-0 { margin: var(--space-0); }
.m-px { margin: var(--space-px); }
.m-xs { margin: var(--space-xs); }
.m-sm { margin: var(--space-sm); }
.m-md { margin: var(--space-md); }
.m-lg { margin: var(--space-lg); }
.m-xl { margin: var(--space-xl); }
.m-2xl { margin: var(--space-2xl); }
.m-3xl { margin: var(--space-3xl); }
.m-auto { margin: auto; }

/* Horizontal (x-axis) */
.mx-0 { margin-left: var(--space-0); margin-right: var(--space-0); }
.mx-px { margin-left: var(--space-px); margin-right: var(--space-px); }
/* ... through .mx-3xl */
.mx-auto { margin-left: auto; margin-right: auto; }

/* Vertical (y-axis) */
.my-0 { margin-top: var(--space-0); margin-bottom: var(--space-0); }
.my-px { margin-top: var(--space-px); margin-bottom: var(--space-px); }
/* ... through .my-3xl */
.my-auto { margin-top: auto; margin-bottom: auto; }

/* Individual sides (top, right, bottom, left) also available */
```

#### Padding

```css
/* All sides */
.p-0 { padding: var(--space-0); }
.p-px { padding: var(--space-px); }
.p-xs { padding: var(--space-xs); }
.p-sm { padding: var(--space-sm); }
.p-md { padding: var(--space-md); }
.p-lg { padding: var(--space-lg); }
.p-xl { padding: var(--space-xl); }
.p-2xl { padding: var(--space-2xl); }
.p-3xl { padding: var(--space-3xl); }

/* Horizontal (x-axis) */
.px-0 { padding-left: var(--space-0); padding-right: var(--space-0); }
.px-px { padding-left: var(--space-px); padding-right: var(--space-px); }
/* ... through .px-3xl */

/* Vertical (y-axis) */
.py-0 { padding-top: var(--space-0); padding-bottom: var(--space-0); }
.py-px { padding-top: var(--space-px); padding-bottom: var(--space-px); }
/* ... through .py-3xl */

/* Individual sides (top, right, bottom, left) also available */
```

#### Gap

```css
.gap-0 { gap: var(--space-0); }
.gap-px { gap: var(--space-px); }
.gap-xs { gap: var(--space-xs); }
.gap-sm { gap: var(--space-sm); }
.gap-md { gap: var(--space-md); }
.gap-lg { gap: var(--space-lg); }
.gap-xl { gap: var(--space-xl); }
.gap-2xl { gap: var(--space-2xl); }
.gap-3xl { gap: var(--space-3xl); }
```

### Typography Utilities

#### Font Family

```css
.font-sans { font-family: var(--font-family-sans); }
.font-serif { font-family: var(--font-family-serif); }
.font-mono { font-family: var(--font-family-mono); }
```

#### Font Size

```css
.text-xs { font-size: var(--font-size-xs); }
.text-sm { font-size: var(--font-size-sm); }
.text-base { font-size: var(--font-size-base); }
.text-md { font-size: var(--font-size-md); }
.text-lg { font-size: var(--font-size-lg); }
.text-xl { font-size: var(--font-size-xl); }
.text-2xl { font-size: var(--font-size-2xl); }
.text-3xl { font-size: var(--font-size-3xl); }
.text-4xl { font-size: var(--font-size-4xl); }
```

#### Font Weight

```css
.font-thin { font-weight: var(--font-weight-thin); }
.font-extra-light { font-weight: var(--font-weight-extra-light); }
.font-light { font-weight: var(--font-weight-light); }
.font-normal { font-weight: var(--font-weight-normal); }
.font-medium { font-weight: var(--font-weight-medium); }
.font-semibold { font-weight: var(--font-weight-semibold); }
.font-bold { font-weight: var(--font-weight-bold); }
.font-extra-bold { font-weight: var(--font-weight-extra-bold); }
.font-black { font-weight: var(--font-weight-black); }
```

#### Line Height

```css
.leading-none { line-height: var(--line-height-none); }
.leading-tight { line-height: var(--line-height-tight); }
.leading-snug { line-height: var(--line-height-snug); }
.leading-normal { line-height: var(--line-height-normal); }
.leading-relaxed { line-height: var(--line-height-relaxed); }
.leading-loose { line-height: var(--line-height-loose); }
```

#### Letter Spacing

```css
.tracking-tighter { letter-spacing: var(--letter-spacing-tighter); }
.tracking-tight { letter-spacing: var(--letter-spacing-tight); }
.tracking-normal { letter-spacing: var(--letter-spacing-normal); }
.tracking-wide { letter-spacing: var(--letter-spacing-wide); }
.tracking-wider { letter-spacing: var(--letter-spacing-wider); }
.tracking-widest { letter-spacing: var(--letter-spacing-widest); }
```

#### Text Alignment

```css
.text-left { text-align: left; }
.text-center { text-align: center; }
.text-right { text-align: right; }
.text-justify { text-align: justify; }
```

### Border Utilities

#### Border Width

```css
.border { border-width: var(--border-width); }
.border-thin { border-width: var(--border-width-thin); }
.border-thick { border-width: var(--border-width-thick); }
.border-none { border-width: 0; }
```

#### Border Radius

```css
.rounded-none { border-radius: 0; }
.rounded-sm { border-radius: var(--radius-sm); }
.rounded-md { border-radius: var(--radius-md); }
.rounded-lg { border-radius: var(--radius-lg); }
.rounded-xl { border-radius: var(--radius-xl); }
.rounded-full { border-radius: var(--radius-full); }
```

### Shadow Utilities

```css
.shadow-none { box-shadow: none; }
.shadow-sm { box-shadow: var(--shadow-sm); }
.shadow-md { box-shadow: var(--shadow-md); }
.shadow-lg { box-shadow: var(--shadow-lg); }
.shadow-xl { box-shadow: var(--shadow-xl); }
.shadow-inner { box-shadow: var(--shadow-inner); }
```

### Position Utilities

```css
.static { position: static; }
.fixed { position: fixed; }
.absolute { position: absolute; }
.relative { position: relative; }
.sticky { position: sticky; }
```

### Z-Index Utilities

```css
.z-0 { z-index: var(--z-index-0); }
.z-10 { z-index: var(--z-index-10); }
.z-20 { z-index: var(--z-index-20); }
.z-30 { z-index: var(--z-index-30); }
.z-40 { z-index: var(--z-index-40); }
.z-50 { z-index: var(--z-index-50); }
.z-auto { z-index: var(--z-index-auto); }
```

### Display Utilities

```css
.block { display: block; }
.inline-block { display: inline-block; }
.inline { display: inline; }
.flex { display: flex; }
.inline-flex { display: inline-flex; }
.grid { display: grid; }
.inline-grid { display: inline-grid; }
.hidden { display: none; }
```

### Flex Utilities

```css
.flex-row { flex-direction: row; }
.flex-row-reverse { flex-direction: row-reverse; }
.flex-col { flex-direction: column; }
.flex-col-reverse { flex-direction: column-reverse; }
.flex-wrap { flex-wrap: wrap; }
.flex-nowrap { flex-wrap: nowrap; }
.flex-wrap-reverse { flex-wrap: wrap-reverse; }
.flex-1 { flex: var(--flex-1); }
.flex-auto { flex: var(--flex-auto); }
.flex-initial { flex: var(--flex-initial); }
.flex-none { flex: var(--flex-none); }
```

### Grid Utilities

```css
.grid-cols-1 { grid-template-columns: repeat(1, minmax(0, 1fr)); }
.grid-cols-2 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
.grid-cols-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
.grid-cols-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }
.grid-cols-6 { grid-template-columns: repeat(6, minmax(0, 1fr)); }
.grid-cols-12 { grid-template-columns: repeat(12, minmax(0, 1fr)); }
```

### Width and Height Utilities

```css
.w-auto { width: auto; }
.w-full { width: 100%; }
.w-screen { width: 100vw; }
.w-min { width: min-content; }
.w-max { width: max-content; }
.w-fit { width: fit-content; }
.w-1\/2 { width: 50%; }
.w-1\/3 { width: 33.333333%; }
.w-2\/3 { width: 66.666667%; }
.w-1\/4 { width: 25%; }
.w-3\/4 { width: 75%; }

.h-auto { height: auto; }
.h-full { height: 100%; }
.h-screen { height: 100vh; }
.h-min { height: min-content; }
.h-max { height: max-content; }
.h-fit { height: fit-content; }
.h-1\/2 { height: 50%; }
.h-1\/3 { height: 33.333333%; }
.h-2\/3 { height: 66.666667%; }
```

### Opacity Utilities

```css
.opacity-0 { opacity: var(--alpha-0); }
.opacity-5 { opacity: var(--alpha-1); }
.opacity-10 { opacity: var(--alpha-2); }
.opacity-20 { opacity: var(--alpha-3); }
.opacity-40 { opacity: var(--alpha-4); }
.opacity-60 { opacity: var(--alpha-5); }
.opacity-75 { opacity: var(--alpha-6); }
.opacity-80 { opacity: var(--alpha-7); }
.opacity-90 { opacity: var(--alpha-8); }
.opacity-95 { opacity: var(--alpha-9); }
.opacity-100 { opacity: var(--alpha-10); }
```

### Overflow Utilities

```css
.overflow-auto { overflow: auto; }
.overflow-hidden { overflow: hidden; }
.overflow-visible { overflow: visible; }
.overflow-scroll { overflow: scroll; }
.overflow-x-auto { overflow-x: auto; }
.overflow-y-auto { overflow-y: auto; }
.overflow-x-hidden { overflow-x: hidden; }
.overflow-y-hidden { overflow-y: hidden; }
```

### Interactivity Utilities

```css
.cursor-auto { cursor: auto; }
.cursor-default { cursor: default; }
.cursor-pointer { cursor: pointer; }
.cursor-wait { cursor: wait; }
.cursor-text { cursor: text; }
.cursor-move { cursor: move; }
.cursor-not-allowed { cursor: not-allowed; }

.pointer-events-none { pointer-events: none; }
.pointer-events-auto { pointer-events: auto; }

.select-none { user-select: none; }
.select-text { user-select: text; }
.select-all { user-select: all; }
.select-auto { user-select: auto; }
```

### Accessibility Utilities

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

.focus-visible-outline:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}
```

### Button Style Utilities

For use with the button component:

```css
/* Filled Buttons */
.button-filled-accent { background-color: var(--accent); --bg: var(--accent); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-secondary { background-color: var(--secondary); --bg: var(--secondary); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-tertiary { background-color: var(--tertiary); --bg: var(--tertiary); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-success { background-color: var(--success); --bg: var(--success); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-warning { background-color: var(--warning); --bg: var(--warning); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-error { background-color: var(--error); --bg: var(--error); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-info { background-color: var(--info); --bg: var(--info); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }
.button-filled-gray { background-color: var(--surface-overt); --bg: var(--surface-overt); color:     var(--auto-contrast-text, oklch(
  from var(--bg, currentColor)
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
)); border-color: transparent; }

/* Outline Buttons */
.button-outline-accent { color: var(--accent); border-color: var(--accent-subtle); background-color: transparent; }
.button-outline-secondary { color: var(--secondary); border-color: var(--secondary-subtle); background-color: transparent; }
.button-outline-tertiary { color: var(--tertiary); border-color: var(--tertiary-subtle); background-color: transparent; }
.button-outline-success { color: var(--success); border-color: var(--outline-success); background-color: transparent; }
.button-outline-warning { color: var(--warning); border-color: var(--outline-warning); background-color: transparent; }
.button-outline-error { color: var(--error); border-color: var(--outline-error); background-color: transparent; }
.button-outline-info { color: var(--info); border-color: var(--outline-info); background-color: transparent; }
.button-outline-gray { color: var(--text-subtle); border-color: var(--outline-default); background-color: transparent; }

/* Text Buttons */
.button-text-accent { color: var(--accent); background-color: transparent; border-color: transparent;}
.button-text-secondary { color: var(--secondary); background-color: transparent; border-color: transparent;}
.button-text-tertiary { color: var(--tertiary); background-color: transparent; border-color: transparent;}
.button-text-success { color: var(--success); background-color: transparent; border-color: transparent;}
.button-text-warning { color: var(--warning); background-color: transparent; border-color: transparent;}
.button-text-error { color: var(--error); background-color: transparent; border-color: transparent;}
.button-text-info { color: var(--info); background-color: transparent; border-color: transparent;}
.button-text-gray { color: var(--text-subtle); background-color: transparent; border-color: transparent;}
```

## Using the Utilities Layer

### Basic Usage

Utility classes are applied directly in your HTML:

```html
<div class="bg-surface-default p-md rounded-md shadow-md">
  <h2 class="text-xl font-bold text-default mb-sm">Card Title</h2>
  <p class="text-subtle mb-md">Card description goes here.</p>
  <button class="button button-filled-accent">Action</button>
</div>
```

### Combining Utilities

The power of utilities comes from combining them:

```html
<!-- A responsive card with hover effect -->
<div class="bg-surface-default p-sm p-md rounded-md shadow-sm hover:shadow-lg transition">
  <div class="flex items-center gap-sm mb-md">
    <div class="rounded-full bg-accent w-12 h-12 flex items-center justify-center text-white font-bold">A</div>
    <div>
      <h3 class="text-lg font-semibold text-default">Card Title</h3>
      <p class="text-sm text-subtle">Subtitle or metadata</p>
    </div>
  </div>
  <p class="text-default mb-md">This is the card content with a <a href="#" class="text-link">link</a>.</p>
  <div class="flex justify-end gap-sm">
    <button class="button button-text-subtle">Cancel</button>
    <button class="button button-filled-accent">Action</button>
  </div>
</div>
```

### With Components

Utility classes work well with components to customize them for specific contexts:

```html
<div class="card mb-lg shadow-lg">
  <div class="card__header bg-accent-subtle">
    <h2 class="card__title text-accent">Custom Header</h2>
  </div>
  <div class="card__body p-lg">
    <p class="text-default mb-md">Card content with custom padding.</p>
    <div class="flex flex-col gap-md">
      <input type="text" class="form-input border-accent-subtle" placeholder="Enter value">
      <textarea class="form-input h-24" placeholder="Additional details"></textarea>
    </div>
  </div>
  <div class="card__footer flex justify-between">
    <button class="button button-text-subtle">Cancel</button>
    <button class="button button-filled-accent">Submit</button>
  </div>
</div>
```

## Extending the Utilities Layer

### Adding New Utilities

To add new utility classes, extend the Utilities layer:

```css
@layer utilities {
  /* Adding new utilities */
  .rotate-45 { transform: rotate(45deg); }
  .rotate-90 { transform: rotate(90deg); }
  .rotate-180 { transform: rotate(180deg); }
  
  .scale-75 { transform: scale(0.75); }
  .scale-90 { transform: scale(0.9); }
  .scale-110 { transform: scale(1.1); }
  .scale-125 { transform: scale(1.25); }
  
  .transition-transform { transition-property: transform; }
  .transition-colors { transition-property: color, background-color, border-color; }
  .transition-opacity { transition-property: opacity; }
  .transition-all { transition-property: all; }
  
  .duration-100 { transition-duration: 100ms; }
  .duration-200 { transition-duration: 200ms; }
  .duration-300 { transition-duration: 300ms; }
  .duration-500 { transition-duration: 500ms; }
}
```

### Creating Utility Variants

For more complex scenarios, create utility variants:

```css
@layer utilities {
  /* Hover variants */
  .hover\:bg-accent:hover { background-color: var(--accent); }
  .hover\:text-accent:hover { color: var(--accent); }
  .hover\:scale-105:hover { transform: scale(1.05); }
  
  /* Focus variants */
  .focus\:border-accent:focus { border-color: var(--accent); }
  .focus\:outline-none:focus { outline: none; }
  
  /* Active variants */
  .active\:bg-accent-overt:active { background-color: var(--accent-overt); }
  .active\:scale-95:active { transform: scale(0.95); }
}
```

## Best Practices

### When to Use Utilities

Use utility classes when:

1. **Building one-off UI elements** that don't warrant a dedicated component
2. **Prototyping designs** quickly without writing new CSS
3. **Adjusting components** for specific contexts
4. **Creating spacing and layout** throughout your application
5. **Fine-tuning designs** without adding custom CSS

### When to Use Components Instead

Use components instead of utilities when:

1. **The same pattern repeats** throughout your application
2. **The element has complex behavior** beyond simple styling
3. **The styling is too complex** to express cleanly with utilities
4. **You need to ensure consistency** across multiple instances
5. **The pattern includes accessibility logic** like keyboard handling

### Utility-First Approach

1. **Start with utilities**: Begin building with utility classes
2. **Extract components**: When patterns repeat, extract them into components
3. **Customize with utilities**: Use utilities to adapt components to specific contexts

### Naming and Organization

1. **Follow consistent naming**: Use the established naming pattern
2. **Group related utilities**: Keep related utilities together in your code
3. **Document utility purpose**: Add comments to explain complex utilities
4. **Consider responsive variants**: Create responsive variants for key utilities

### Performance Considerations

1. **Selective inclusion**: Consider only including the utilities you use
2. **Compression**: Use gzip/brotli compression to minimize transfer size
3. **Cache effectively**: Leverage browser caching for utility CSS
4. **Consider CSS-in-JS**: For dynamic utilities, consider CSS-in-JS approaches

## Complete Reference

The Utilities layer includes the following categories:

1. **Colors**
   - Background colors
   - Text colors
   - Border colors
   
2. **Typography**
   - Font family
   - Font size
   - Font weight
   - Line height
   - Letter spacing
   - Text alignment
   
3. **Spacing**
   - Margin
   - Padding
   - Gap
   
4. **Borders**
   - Border width
   - Border style
   - Border radius
   
5. **Effects**
   - Shadows
   - Opacity
   
6. **Layout**
   - Display
   - Position
   - Z-index
   - Width and height
   - Overflow
   
7. **Flexbox**
   - Flex direction
   - Flex wrapping
   - Flex grow/shrink
   - Alignment
   
8. **Grid**
   - Grid columns
   - Grid rows
   - Grid placement
   
9. **Interactivity**
   - Cursor
   - Pointer events
   - User select
   
10. **Accessibility**
    - Screen reader utilities
    - Focus management

For a comprehensive list of all available utility classes, refer to the utilities.css file.