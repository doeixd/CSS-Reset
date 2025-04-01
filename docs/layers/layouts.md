# Layouts Layer

The Layouts layer provides reusable layout patterns and structural components that help organize content on the page. These layout components use container queries for component-level responsive design, making them truly reusable regardless of their context.

## Core Concept

Layout components focus on the arrangement and positioning of elements rather than their visual appearance. They provide the structural foundation upon which you can build more complex interfaces.

The Layouts layer has the highest specificity in the cascade, allowing layout components to override other styles when necessary:

```css
@layer reset, tokens, engine, theme, palette, defaults, components, utilities, layouts;
```

Unlike traditional layout systems that rely on viewport-based media queries, our layout components use container queries to adapt based on their own size rather than the size of the viewport. This makes them more flexible and reusable.

## Key Features

### Container Query Support

All layout components use container queries to adapt their layout based on their container size:

```css
.l-container {
  container-type: var(--l-container-type, inline-size);
  container-name: var(--l-container-name, layout);
}

.l-grid {
  display: grid;
  gap: var(--l-grid-gap, var(--space-md));
  grid-template-columns: repeat(auto-fit, minmax(min(100%, var(--l-grid-min-item-size, 15rem)), 1fr));
  container-type: inline-size;
  container-name: layout-grid;
}

@container layout-grid (min-width: var(--cq-bp-sm, 30em)) {
  /* Layout changes at container width of 30em */
}

@container layout-grid (min-width: var(--cq-bp-md, 45em)) {
  /* Layout changes at container width of 45em */
}
```

### Customization via CSS Variables

Layout components are highly customizable through CSS variables:

```css
.l-grid {
  --l-grid-gap: var(--space-lg); /* Override default gap */
  --l-grid-min-item-size: 20rem; /* Override default minimum item size */
}

.l-split {
  --l-split-fraction: 2fr; /* Change the split ratio */
  --l-split-gap: var(--space-xl); /* Override default gap */
  --l-split-breakpoint: var(--cq-bp-md); /* Custom breakpoint */
}
```

### Progressive Enhancement

Layouts are designed with progressive enhancement in mind, working with and without container query support:

```css
.l-row {
  display: flex;
  flex-wrap: var(--l-row-wrap, wrap);
  gap: var(--l-row-gap, var(--space-md));
  container-type: inline-size;
  container-name: layout-row;
  flex-direction: column; /* Default stacked layout */
  align-items: var(--l-row-align-stacked, stretch);
}

/* With container queries */
@container layout-row (min-width: var(--l-row-stack-breakpoint, var(--cq-bp-xs, 20em))) {
  .l-row:not(.l-row--force-stack) {
    flex-direction: var(--l-row-direction, row);
    align-items: var(--l-row-align, center);
    justify-content: var(--l-row-justify, flex-start);
  }
}

/* Without container queries - can use a forced class */
.l-row--no-stack {
  flex-direction: var(--l-row-direction, row);
  align-items: var(--l-row-align, center);
  justify-content: var(--l-row-justify, flex-start);
}
```

## Layout Components

### Grid Layout

A responsive grid layout that automatically adjusts columns based on container width:

```css
.l-grid {
  display: grid;
  gap: var(--l-grid-gap, var(--space-md));
  grid-template-columns: repeat(auto-fit, minmax(min(100%, var(--l-grid-min-item-size, 15rem)), 1fr));
  container-type: inline-size;
  container-name: layout-grid;
}

.l-grid > * {
  min-width: 0; /* Prevent grid items from overflowing */
}
```

Usage:

```html
<div class="l-grid">
  <div class="card">Grid Item 1</div>
  <div class="card">Grid Item 2</div>
  <div class="card">Grid Item 3</div>
  <div class="card">Grid Item 4</div>
</div>
```

Customization:

```html
<div class="l-grid" style="--l-grid-min-item-size: 20rem; --l-grid-gap: var(--space-lg);">
  <!-- Grid items -->
</div>
```

### Two-Column Layout

A simple two-column layout that stacks on smaller containers:

```css
.l-two-col {
  display: grid;
  gap: var(--l-two-col-gap, var(--space-lg));
  container-type: inline-size;
  container-name: layout-two-col;
  grid-template-columns: 1fr; /* Default to single column */
}

.l-two-col > * {
  min-width: 0;
}

@container layout-two-col (min-width: var(--l-two-col-breakpoint, var(--cq-bp-sm, 30em))) {
  .l-two-col {
    grid-template-columns: repeat(2, 1fr); /* Two equal columns at breakpoint */
  }
}
```

### Split Layout

A two-column layout with customizable proportions:

```css
.l-split {
  display: grid;
  grid-template-columns: 1fr; /* Default to single column */
  gap: var(--l-split-gap, var(--space-lg));
  container-type: inline-size;
  container-name: layout-split;
}

.l-split > * {
  min-width: 0;
}

@container layout-split (min-width: var(--l-split-breakpoint, var(--cq-bp-sm, 30em))) {
  .l-split {
    grid-template-columns: var(--l-split-fraction, 1fr) 1fr; /* Customizable split ratio */
  }
}

.l-split--no-stack {
  grid-template-columns: var(--l-split-fraction, 1fr) 1fr; /* Always use columns */
}
```

Usage:

```html
<div class="l-split" style="--l-split-fraction: 2fr;">
  <div class="bg-surface-subtle p-md">Wider column (2fr)</div>
  <div class="bg-surface-subtle p-md">Narrower column (1fr)</div>
</div>
```

### Row Layout

A flexible row layout that stacks on smaller containers:

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

.l-row > * {
  min-width: 0;
}

@container layout-row (min-width: var(--l-row-stack-breakpoint, var(--cq-bp-xs, 20em))) {
  .l-row:not(.l-row--force-stack) {
    flex-direction: var(--l-row-direction, row);
    align-items: var(--l-row-align, center);
    justify-content: var(--l-row-justify, flex-start);
  }
}

.l-row--no-stack {
  flex-direction: var(--l-row-direction, row);
  align-items: var(--l-row-align, center);
  justify-content: var(--l-row-justify, flex-start);
}
```

Usage:

```html
<div class="l-row" style="--l-row-justify: space-between;">
  <div>Start content</div>
  <div>Middle content</div>
  <div>End content</div>
</div>
```

### Stack Layout

A vertical stack with consistent spacing:

```css
.l-stack {
  display: flex;
  flex-direction: column;
  justify-content: var(--l-stack-justify, flex-start);
  align-items: var(--l-stack-align, stretch);
  gap: var(--l-stack-gap, var(--space-md));
}
```

Usage:

```html
<div class="l-stack" style="--l-stack-gap: var(--space-lg);">
  <h2>Heading</h2>
  <p>Paragraph text</p>
  <button class="button">Action</button>
</div>
```

### Cluster Layout

A flexible layout for grouping related elements:

```css
.l-cluster {
  display: flex;
  flex-wrap: wrap;
  gap: var(--l-cluster-gap, var(--space-sm));
  justify-content: var(--l-cluster-justify, flex-start);
  align-items: var(--l-cluster-align, center);
}
```

Usage:

```html
<div class="l-cluster">
  <span class="badge">Tag 1</span>
  <span class="badge">Tag 2</span>
  <span class="badge">Long Tag 3</span>
  <span class="badge">Tag 4</span>
</div>
```

### Reel Layout

A horizontally scrolling container:

```css
.l-reel {
  display: flex;
  gap: var(--l-reel-gap, var(--space-md));
  overflow-x: auto;
  overflow-y: hidden;
  scrollbar-width: thin;
  scrollbar-color: var(--scrollbar-thumb-color) var(--scrollbar-track-color);
  -webkit-overflow-scrolling: touch;
}

.l-reel--no-scrollbar {
  scrollbar-width: none;
}

.l-reel--no-scrollbar::-webkit-scrollbar {
  display: none;
}

.l-reel > * {
  flex-shrink: 0;
}

.l-reel > img {
  height: 100%;
  max-height: var(--l-reel-item-max-height, 100%);
  width: auto;
  flex-basis: auto;
}
```

Usage:

```html
<div class="l-reel">
  <div class="card" style="width: 300px;">Card 1</div>
  <div class="card" style="width: 300px;">Card 2</div>
  <div class="card" style="width: 300px;">Card 3</div>
  <div class="card" style="width: 300px;">Card 4</div>
</div>
```

### Switcher Layout

A layout that switches between row and column based on container width:

```css
.l-switcher {
  display: flex;
  flex-wrap: wrap;
  gap: var(--l-switcher-gap, var(--space-sm));
}

.l-switcher > * {
  flex-grow: 1;
  flex-basis: calc((var(--l-switcher-threshold, 20rem) - 100%) * 999);
}
```

Usage:

```html
<div class="l-switcher" style="--l-switcher-threshold: 25rem;">
  <div class="card">Section 1</div>
  <div class="card">Section 2</div>
</div>
```

### Spread Layout

A layout for distributing items evenly:

```css
.l-spread {
  display: flex;
  flex-direction: var(--l-spread-direction, row);
  justify-content: space-between;
  align-items: var(--l-spread-align, center);
  gap: var(--l-spread-gap, var(--space-md));
}
```

Usage:

```html
<div class="l-spread">
  <div>Left content</div>
  <div>Right content</div>
</div>
```

## Wrapper Components

### Padding Wrapper

Adds consistent padding to an element:

```css
.l-pad {
  padding: var(--l-pad-padding, var(--space-md));
  padding-inline: var(--l-pad-padding-x, var(--l-pad-padding, var(--space-md)));
  padding-block: var(--l-pad-padding-y, var(--l-pad-padding, var(--space-md)));
}
```

Usage:

```html
<div class="l-pad" style="--l-pad-padding-x: var(--space-lg); --l-pad-padding-y: var(--space-md);">
  Content with custom padding
</div>
```

### Center Content

Centers content horizontally with a maximum width:

```css
.l-center-content {
  box-sizing: content-box;
  margin-inline: auto;
  max-width: var(--l-center-content-max-width, var(--width-container-max, 60ch));
  padding-inline: var(--l-center-content-gutter, 0);
  text-align: var(--l-center-content-text-align, initial);
}
```

Usage:

```html
<div class="l-center-content" style="--l-center-content-max-width: 80ch; --l-center-content-gutter: var(--space-md);">
  <p>Centered content with a maximum width and gutters.</p>
</div>
```

### Cover Layout

Creates a full-height layout with centered content:

```css
.l-cover {
  display: grid;
  place-content: var(--l-cover-place-content, center);
  place-items: var(--l-cover-place-items, center);
  padding: var(--l-cover-padding, var(--space-lg));
  min-height: var(--l-cover-min-height, 50vh);
  overflow: hidden;
  text-align: var(--l-cover-text-align, center);
}
```

Usage:

```html
<div class="l-cover" style="--l-cover-min-height: 100vh;">
  <div class="l-stack">
    <h1>Centered Cover Layout</h1>
    <p>This content is centered vertically and horizontally.</p>
    <button class="button button-filled-accent">Action</button>
  </div>
</div>
```

### Frame Layout

Creates a responsive container for media with a fixed aspect ratio:

```css
.l-frame {
  position: relative;
  overflow: hidden;
  aspect-ratio: var(--l-frame-ratio, 16 / 9);
}

.l-frame > :first-child {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: var(--l-frame-object-fit, cover);
  object-position: var(--l-frame-object-position, center);
}
```

Usage:

```html
<div class="l-frame" style="--l-frame-ratio: 1 / 1;">
  <img src="image.jpg" alt="Square framed image">
</div>
```

### Center Layout

Centers content horizontally, vertically, or both:

```css
.l-center {
  display: flex;
  justify-content: var(--l-center-justify, center);
  align-items: var(--l-center-align, center);
  min-height: var(--l-center-min-height, auto);
  padding: var(--l-center-padding, 0);
}

.l-center--h {
  align-items: initial;
}

.l-center--v {
  justify-content: initial;
}
```

Usage:

```html
<div class="l-center" style="min-height: 200px;">
  <div>Centered content</div>
</div>
```

## Complex Layout Patterns

### Sidebar Layout

A sidebar layout with customizable width and position:

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

@container layout-sidebar (min-width: var(--l-sidebar-breakpoint, var(--cq-bp-md, 45em))) {
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

Usage:

```html
<div class="l-sidebar">
  <main>
    <h1>Main Content</h1>
    <p>This is the main content area.</p>
  </main>
  <aside class="l-sidebar__aside">
    <nav>
      <h2>Navigation</h2>
      <ul>
        <li><a href="#">Link 1</a></li>
        <li><a href="#">Link 2</a></li>
        <li><a href="#">Link 3</a></li>
      </ul>
    </nav>
  </aside>
</div>
```

### Standard Page Layout

A common layout with header, main content, and footer:

```css
.l-standard-page {
  display: grid;
  grid-template-rows: auto 1fr auto;
  min-height: var(--l-standard-page-min-height, 100vh);
  gap: var(--l-standard-page-gap, 0);
}

.l-standard-page > * {
  min-width: 0;
}

.l-standard-page__header {
  grid-row: 1;
}

.l-standard-page__main {
  grid-row: 2;
}

.l-standard-page__footer {
  grid-row: 3;
}
```

Usage:

```html
<div class="l-standard-page">
  <header class="l-standard-page__header">
    <nav>Header content</nav>
  </header>
  <main class="l-standard-page__main">
    <div class="l-center-content l-pad">
      <h1>Main Content</h1>
      <p>This is the main content area.</p>
    </div>
  </main>
  <footer class="l-standard-page__footer">
    <div class="l-center-content l-pad">
      Footer content
    </div>
  </footer>
</div>
```

### Media Layout

A layout for image and text combinations:

```css
.l-media {
  display: flex;
  align-items: var(--l-media-align, flex-start);
  gap: var(--l-media-gap, var(--space-md));
}

.l-media > :first-child {
  flex-shrink: 0;
}

.l-media > :last-child {
  flex-grow: 1;
  min-width: 0;
}

.l-media--reverse {
  flex-direction: row-reverse;
}
```

Usage:

```html
<div class="l-media">
  <img src="avatar.jpg" alt="User avatar" width="64" height="64">
  <div>
    <h3>John Doe</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </div>
</div>
```

### Tabs Layout

A flexible tabs layout:

```css
.l-tabs {
  display: flex;
  flex-direction: column;
  gap: var(--l-tabs-gap, var(--space-md));
}

.l-tabs__list {
  flex-shrink: 0;
}

.l-tabs__panel {
  flex-grow: 1;
  min-height: 0;
}

.l-tabs--bottom {
  flex-direction: column-reverse;
}

.l-tabs--left {
  flex-direction: row;
}

.l-tabs--right {
  flex-direction: row-reverse;
}

.l-tabs--left > .l-tabs__panel,
.l-tabs--right > .l-tabs__panel {
  min-width: 0;
}

.l-tabs--left > .l-tabs__list,
.l-tabs--right > .l-tabs__list {
  width: var(--l-tabs-side-width, max-content);
  flex-shrink: 0;
}
```

Usage:

```html
<div class="l-tabs">
  <div class="l-tabs__list">
    <button class="button" aria-selected="true">Tab 1</button>
    <button class="button">Tab 2</button>
    <button class="button">Tab 3</button>
  </div>
  <div class="l-tabs__panel">
    Tab 1 content
  </div>
</div>
```

## Using the Layouts Layer

### Basic Usage

Layout components are used by applying their CSS classes:

```html
<!-- Basic grid layout -->
<div class="l-grid">
  <div class="card">Grid Item 1</div>
  <div class="card">Grid Item 2</div>
  <div class="card">Grid Item 3</div>
</div>

<!-- Stack layout for vertical content -->
<div class="l-stack gap-lg">
  <h2>Stack Layout</h2>
  <p>Content stacked vertically with consistent spacing.</p>
  <button class="button">Action</button>
</div>
```

### Customizing Layouts

Layouts can be customized using CSS variables:

```html
<!-- Customized grid layout -->
<div class="l-grid" style="--l-grid-min-item-size: 20rem; --l-grid-gap: var(--space-lg);">
  <div class="card">Grid Item 1</div>
  <div class="card">Grid Item 2</div>
  <div class="card">Grid Item 3</div>
</div>

<!-- Customized split layout -->
<div class="l-split" style="--l-split-fraction: 2fr; --l-split-gap: var(--space-xl);">
  <div class="bg-surface-subtle p-md">Wider column (2fr)</div>
  <div class="bg-surface-subtle p-md">Narrower column (1fr)</div>
</div>
```

### Combining with Components and Utilities

Layouts work well with components and utility classes:

```html
<div class="l-standard-page">
  <header class="l-standard-page__header bg-surface-default shadow-sm">
    <div class="l-center-content l-pad">
      <div class="l-spread">
        <h1 class="text-xl font-bold">Site Title</h1>
        <nav class="l-row gap-sm">
          <a href="#" class="text-link">Home</a>
          <a href="#" class="text-link">About</a>
          <a href="#" class="text-link">Contact</a>
        </nav>
      </div>
    </div>
  </header>
  
  <main class="l-standard-page__main bg-base">
    <div class="l-center-content l-pad">
      <div class="l-stack gap-xl">
        <section>
          <h2 class="text-2xl font-bold mb-md">Featured Content</h2>
          <div class="l-grid">
            <div class="card">
              <div class="card__body">
                <h3>Card 1</h3>
                <p>Card content here.</p>
              </div>
            </div>
            <div class="card">
              <div class="card__body">
                <h3>Card 2</h3>
                <p>Card content here.</p>
              </div>
            </div>
            <div class="card">
              <div class="card__body">
                <h3>Card 3</h3>
                <p>Card content here.</p>
              </div>
            </div>
          </div>
        </section>
        
        <section>
          <h2 class="text-2xl font-bold mb-md">Sidebar Example</h2>
          <div class="l-sidebar">
            <div class="bg-surface-default p-lg rounded-md">
              <h3>Main Content</h3>
              <p>This is the main content area.</p>
            </div>
            <aside class="l-sidebar__aside bg-surface-subtle p-md rounded-md">
              <h3>Sidebar</h3>
              <p>This is the sidebar content.</p>
            </aside>
          </div>
        </section>
      </div>
    </div>
  </main>
  
  <footer class="l-standard-page__footer bg-surface-default border-t border-outline-subtle">
    <div class="l-center-content l-pad">
      <div class="l-spread">
        <p class="text-subtle">© 2023 Company Name</p>
        <div class="l-cluster">
          <a href="#" class="text-link">Terms</a>
          <a href="#" class="text-link">Privacy</a>
          <a href="#" class="text-link">Contact</a>
        </div>
      </div>
    </div>
  </footer>
</div>
```

## Extending the Layouts Layer

### Creating New Layout Components

To create a new layout component:

```css
@layer layouts {
  /* Creating a new "card grid" layout component */
  .l-card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(min(100%, var(--l-card-grid-min-size, 18rem)), 1fr));
    gap: var(--l-card-grid-gap, var(--space-lg));
    container-type: inline-size;
    container-name: layout-card-grid;
  }
  
  .l-card-grid > * {
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  
  .l-card-grid-item__media {
    aspect-ratio: var(--l-card-grid-media-ratio, 16 / 9);
    overflow: hidden;
  }
  
  .l-card-grid-item__media img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .l-card-grid-item__content {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  
  .l-card-grid-item__footer {
    margin-top: auto;
  }
}
```

### Extending Existing Layout Components

To extend an existing layout component:

```css
@layer layouts {
  /* Adding a variant to the sidebar layout */
  .l-sidebar--sticky-aside {
    height: 100%;
  }
  
  .l-sidebar--sticky-aside > .l-sidebar__aside {
    position: sticky;
    top: var(--l-sidebar-sticky-top, 1rem);
    max-height: var(--l-sidebar-sticky-max-height, calc(100vh - 2rem));
    overflow-y: auto;
  }
  
  /* Adding a new variant to the standard page layout */
  .l-standard-page--fixed-header .l-standard-page__header {
    position: sticky;
    top: 0;
    z-index: var(--z-index-20);
  }
}
```

## Best Practices

1. **Separation of Concerns**: Keep layout separate from visual styling
2. **Container Queries**: Use container queries for true component responsiveness
3. **Progressive Enhancement**: Provide fallbacks for browsers without container query support
4. **Customization**: Use CSS variables for customization rather than adding variants
5. **Semantics**: Use semantic HTML within your layout components
6. **Accessibility**: Ensure layouts maintain good accessibility
7. **Performance**: Keep layouts simple and avoid unnecessary nesting

### Guidelines for Using Layouts

1. **Choose the Right Layout**: Select the layout that best matches your content structure
2. **Combine Layouts**: Nest layouts to create complex structures
3. **Mind the Content**: Ensure content flows well within the chosen layout
4. **Responsive Considerations**: Test layouts at various container sizes
5. **Customize with Variables**: Use CSS variables to adapt layouts to specific needs

## Complete Reference

The Layouts layer includes these layout components:

### Grid Layouts
- `.l-grid`: Responsive auto-fit grid layout
- `.l-two-col`: Simple two-column layout
- `.l-split`: Two-column layout with customizable proportions

### Flexbox Layouts
- `.l-row`: Horizontal row that stacks at small sizes
- `.l-stack`: Vertical stack with consistent spacing
- `.l-cluster`: Flexible layout for grouped elements
- `.l-reel`: Horizontally scrolling container
- `.l-switcher`: Layout that switches between row and column
- `.l-spread`: Layout for distributing items evenly

### Wrapper Components
- `.l-pad`: Consistent padding wrapper
- `.l-center-content`: Centers content with max-width
- `.l-cover`: Full-height centered layout
- `.l-frame`: Fixed aspect ratio container
- `.l-center`: Centering layout (horizontal, vertical, or both)

### Complex Layouts
- `.l-sidebar`: Sidebar layout with customizable position
- `.l-standard-page`: Header, main, footer page structure
- `.l-media`: Image and text layout
- `.l-tabs`: Flexible tabs layout