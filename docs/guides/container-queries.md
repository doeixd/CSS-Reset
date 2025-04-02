# Container Queries Guide

This guide explains how our CSS framework implements container queries for component-level responsive design, a powerful feature that enables truly reusable and context-aware layouts.

## Core Concepts

Container queries allow you to apply styles based on the size of a containing element rather than the viewport size. This creates a more modular approach to responsive design where components can adapt to their container regardless of where they're placed in the UI.

Our framework leverages container queries throughout its layout system to create:

1. **Self-Contained Components**: Components that adapt to their container size
2. **Context-Aware Layouts**: Layouts that respond to their available space
3. **Reusable Patterns**: Patterns that work in any context, regardless of viewport size
4. **Compositional Design**: The ability to compose complex layouts from adaptable parts

## Container Query Implementation

### Container Types

The framework defines containers using the `container-type` and `container-name` properties:

```css
.l-container {
  container-type: var(--l-container-type, inline-size);
  container-name: var(--l-container-name, layout);
}

.l-grid {
  display: grid;
  container-type: inline-size;
  container-name: layout-grid;
  /* Other grid properties */
}
```

We use different container types depending on the layout needs:
- `inline-size`: Responds to changes in the container's width (most common)
- `size`: Responds to changes in both width and height
- `normal`: A standard container but doesn't establish a query container

### Container Names

Container names help target specific containers in complex nested layouts:

```css
.l-sidebar {
  container-type: inline-size;
  container-name: layout-sidebar;
  /* Other sidebar properties */
}

@container layout-sidebar (min-width: 45em) {
  /* Styles that apply when the sidebar container is at least 45em wide */
}
```

### Container Query Breakpoints

The framework provides standardized container query breakpoints:

```css
:root {
  /* Container Query Breakpoints */
  --cq-bp-xs: 20em;  /* 320px */
  --cq-bp-sm: 30em;  /* 480px */
  --cq-bp-md: 45em;  /* 720px */
  --cq-bp-lg: 60em;  /* 960px */
  --cq-bp-xl: 75em;  /* 1200px */
}

@container layout-grid (min-width: var(--cq-bp-sm)) {
  /* Styles that apply at the small breakpoint */
}

@container layout-grid (min-width: var(--cq-bp-md)) {
  /* Styles that apply at the medium breakpoint */
}
```

## Layout Components with Container Queries

### Grid Layout

The grid layout uses container queries to adjust its columns:

```css
.l-grid {
  display: grid;
  gap: var(--l-grid-gap, var(--space-md));
  grid-template-columns: repeat(auto-fit, minmax(min(100%, var(--l-grid-min-item-size, 15rem)), 1fr));
  container-type: inline-size;
  container-name: layout-grid;
}

@container layout-grid (min-width: var(--cq-bp-md)) {
  .l-grid {
    gap: var(--l-grid-gap-md, var(--space-lg));
  }
}

@container layout-grid (min-width: var(--cq-bp-lg)) {
  .l-grid {
    gap: var(--l-grid-gap-lg, var(--space-xl));
  }
}
```

### Split Layout

The split layout adapts from a stacked to a side-by-side layout:

```css
.l-split {
  display: grid;
  grid-template-columns: 1fr; /* Default to single column */
  gap: var(--l-split-gap, var(--space-lg));
  container-type: inline-size;
  container-name: layout-split;
}

@container layout-split (min-width: var(--l-split-breakpoint, var(--cq-bp-sm))) {
  .l-split {
    grid-template-columns: var(--l-split-fraction, 1fr) 1fr; /* Two columns at breakpoint */
  }
}
```

### Row Layout

The row layout switches between column and row orientations:

```css
.l-row {
  display: flex;
  flex-wrap: var(--l-row-wrap, wrap);
  gap: var(--l-row-gap, var(--space-md));
  container-type: inline-size;
  container-name: layout-row;
  flex-direction: column; /* Default to stacked */
  align-items: var(--l-row-align-stacked, stretch);
}

@container layout-row (min-width: var(--l-row-stack-breakpoint, var(--cq-bp-xs))) {
  .l-row:not(.l-row--force-stack) {
    flex-direction: var(--l-row-direction, row);
    align-items: var(--l-row-align, center);
    justify-content: var(--l-row-justify, flex-start);
  }
}
```

### Sidebar Layout

The sidebar layout adapts its structure based on container width:

```css
.l-sidebar {
  display: grid;
  gap: var(--l-sidebar-gap, var(--space-lg));
  container-type: inline-size;
  container-name: layout-sidebar;
  grid-template-areas: "content" "sidebar"; /* Default stacked layout */
}

.l-sidebar > *:not(.l-sidebar__aside) {
  grid-area: content;
  min-width: 0;
}

.l-sidebar > .l-sidebar__aside {
  grid-area: sidebar;
  min-width: 0;
  width: 100%;
}

@container layout-sidebar (min-width: var(--l-sidebar-breakpoint, var(--cq-bp-md))) {
  .l-sidebar {
    grid-template-columns: var(--l-sidebar-width, minmax(15rem, 25%)) 1fr;
    grid-template-areas: "sidebar content";
  }
  
  .l-sidebar > .l-sidebar__aside {
    width: auto;
  }
  
  .l-sidebar--right {
    grid-template-columns: 1fr var(--l-sidebar-width, minmax(15rem, 25%));
    grid-template-areas: "content sidebar";
  }
}
```

## Using Container Queries

### Basic Usage

To use container queries in your layouts:

1. Define a container with `container-type` and `container-name`:

```html
<div class="l-container">
  <!-- Container content -->
</div>
```

2. Apply container queries in your CSS:

```css
@container layout (min-width: 30em) {
  /* Styles that apply when the container is at least 30em wide */
}
```

### Nested Containers

Containers can be nested for more complex responsive layouts:

```html
<div class="l-container" style="--l-container-name: outer;">
  <div class="l-grid">
    <div class="card">Grid Item 1</div>
    <div class="card">Grid Item 2</div>
  </div>
</div>
```

```css
@container outer (min-width: 60em) {
  .l-grid {
    --l-grid-min-item-size: 20rem;
  }
}

@container layout-grid (min-width: 30em) {
  .card {
    padding: var(--space-lg);
  }
}
```

### Customizing Container Query Breakpoints

You can customize container query breakpoints for specific components:

```html
<div class="l-sidebar" style="--l-sidebar-breakpoint: 50em;">
  <!-- Sidebar that switches layout at 50em instead of the default breakpoint -->
</div>
```

### Progressive Enhancement

For browsers that don't support container queries, the framework provides fallbacks:

1. Default styles that work without container queries
2. Optional non-container-query classes

```html
<!-- Will use container queries if supported -->
<div class="l-row">
  <!-- Content -->
</div>

<!-- Will always use row layout regardless of container support -->
<div class="l-row l-row--no-stack">
  <!-- Content -->
</div>
```

```css
.l-row {
  display: flex;
  flex-direction: column; /* Default for all browsers */
}

@container layout-row (min-width: var(--cq-bp-xs)) {
  .l-row:not(.l-row--force-stack) {
    flex-direction: row; /* Container query enhancement */
  }
}

/* Fallback for browsers without container query support */
.l-row--no-stack {
  flex-direction: row;
}
```

## Creating Container Query Components

### Simple Component Example

Here's how to create a card component that adapts to its container:

```css
.responsive-card {
  container-type: inline-size;
  container-name: card;
  display: flex;
  flex-direction: column;
  padding: var(--space-md);
  border-radius: var(--radius-md);
  background-color: var(--surface-default);
}

.responsive-card__media {
  margin-bottom: var(--space-md);
}

.responsive-card__content {
  flex-grow: 1;
}

@container card (min-width: 24em) {
  .responsive-card {
    flex-direction: row;
    align-items: flex-start;
  }
  
  .responsive-card__media {
    margin-bottom: 0;
    margin-right: var(--space-md);
    width: 40%;
  }
  
  .responsive-card__content {
    width: 60%;
  }
}
```

### Complex Component Example

Here's a more complex product listing component:

```css
.product-listing {
  container-type: inline-size;
  container-name: product;
  display: grid;
  gap: var(--space-md);
  grid-template-areas:
    "image"
    "title"
    "price"
    "description"
    "actions";
}

.product-listing__image { grid-area: image; }
.product-listing__title { grid-area: title; }
.product-listing__price { grid-area: price; }
.product-listing__description { grid-area: description; }
.product-listing__actions { grid-area: actions; }

@container product (min-width: 30em) {
  .product-listing {
    grid-template-columns: 1fr 2fr;
    grid-template-areas:
      "image title"
      "image price"
      "image description"
      "image actions";
  }
}

@container product (min-width: 45em) {
  .product-listing {
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-areas:
      "image title title"
      "image price description"
      "image actions actions";
  }
}
```

## Advanced Techniques

### Container Query Units

Container query units allow you to size elements relative to their container:

```css
.responsive-font {
  /* Font size is 5% of the container width */
  font-size: 5cqi;
}

.responsive-padding {
  /* Padding is 3% of the container width */
  padding: 3cqi;
}
```

Available units:
- `cqw`: 1% of a query container's width
- `cqh`: 1% of a query container's height
- `cqi`: 1% of a query container's inline size
- `cqb`: 1% of a query container's block size
- `cqmin`: The smaller value of `cqi` or `cqb`
- `cqmax`: The larger value of `cqi` or `cqb`

### Style Queries (Future)

While not yet widely supported, style queries will allow querying the style of the container:

```css
@container style(--theme: dark) {
  /* Styles for elements within containers with --theme: dark */
}
```

### Container Query Combinators

Combine container queries for more complex conditions:

```css
@container layout (min-width: 30em) and (max-width: 60em) {
  /* Styles for medium-sized containers */
}

@container layout (min-width: 60em) or (min-height: 40em) {
  /* Styles for wide or tall containers */
}
```

## Best Practices

1. **Start mobile-first**: Define base styles for small containers, then enhance for larger ones
2. **Use standardized breakpoints**: Stick to the defined breakpoints for consistency
3. **Name containers meaningfully**: Use descriptive container names for clarity
4. **Don't over-nest**: Too many nested container queries can be hard to manage
5. **Provide fallbacks**: Ensure layouts work reasonably well even without container query support
6. **Document container behaviors**: Make it clear how components respond to container sizes
7. **Consider both width and height**: Some components may need to respond to container height
8. **Test thoroughly**: Check behavior in a variety of container sizes and contexts
9. **Use container query units sparingly**: They're powerful but can lead to unexpected results
10. **Combine with media queries when appropriate**: Some designs need both approaches

## Browser Support

Container queries are supported in:
- Chrome 105+
- Firefox 110+
- Safari 16+
- Edge 105+

For browsers without support:
- Define sensible defaults
- Consider using feature detection
- Provide fallback classes if needed

```javascript
// Feature detection for container queries
if ('container' in document.documentElement.style || 
    'containerType' in document.documentElement.style) {
  // Container queries are supported
  document.documentElement.classList.add('cq-supported');
} else {
  // Container queries are not supported
  document.documentElement.classList.add('cq-not-supported');
}
```

## Resources

- [MDN Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries)
- [CSS Working Group: Container Queries Spec](https://drafts.csswg.org/css-contain-3/)
- [Una Kravets: Container Queries for Designers](https://una.im/cqfill/)
- [Ahmad Shadeed: Container Queries in Practice](https://ishadeed.com/article/container-queries-practical-guide/)
- [Every Layout: Layout Primitives](https://every-layout.dev/)