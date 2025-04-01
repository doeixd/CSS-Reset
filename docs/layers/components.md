# Components Layer

The Components layer provides pre-styled, reusable UI components that build upon the Defaults layer to create more complex interface elements. These components encapsulate common UI patterns with built-in accessibility, responsiveness, and theming.

## Core Concept

Components are self-contained, reusable UI elements that implement common interface patterns. They provide more complex styling than the Defaults layer and serve as the building blocks for your application's interface.

Unlike the Defaults layer (which styles HTML elements directly), the Components layer uses class-based styling to create reusable patterns that can be applied consistently throughout your application.

## Key Components

### Button Component

The button component extends the default button styling with variants:

```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-button-y, 0.7em) var(--space-button-x, 1.3em);
  font-family: var(--font-family-sans);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-medium);
  line-height: 1;
  text-align: center;
  text-decoration: none;
  color: var(--text-default);
  background-color: var(--surface-default);
  border: 1px solid var(--outline-default);
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: color var(--animation-duration-fast) var(--ease-in-out),
              background-color var(--animation-duration-fast) var(--ease-in-out),
              border-color var(--animation-duration-fast) var(--ease-in-out),
              box-shadow var(--animation-duration-fast) var(--ease-in-out),
              opacity var(--animation-duration-fast) var(--ease-in-out);
  user-select: none;
}

.button:hover:not([disabled]) {
  background-color: var(--surface-subtle);
  color: var(--text-overt);
  border-color: var(--outline-overt);
}

.button:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

.button:active:not([disabled]) {
  transform: translateY(1px);
}

.button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.button--small {
  font-size: var(--font-size-sm);
  padding: 0.5em 1em;
}

.button--large {
  font-size: var(--font-size-lg);
  padding: 0.8em 1.5em;
}

.button--icon {
  padding: 0.7em;
  border-radius: var(--radius-full);
}

.button__icon {
  flex-shrink: 0;
  width: 1em;
  height: 1em;
}

.button__icon--left {
  margin-right: 0.5em;
}

.button__icon--right {
  margin-left: 0.5em;
}
```

### Card Component

The card component provides a container for content with various options:

```css
.card {
  background-color: var(--surface-default);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-sm);
  overflow: hidden;
  transition: box-shadow var(--animation-duration-normal) var(--ease-in-out),
              transform var(--animation-duration-normal) var(--ease-in-out);
}

.card--hover:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}

.card__header {
  padding: var(--space-md) var(--space-lg);
  border-bottom: 1px solid var(--outline-subtle);
}

.card__title {
  margin: 0;
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  color: var(--text-overt);
}

.card__subtitle {
  margin-top: var(--space-xs);
  color: var(--text-subtle);
  font-size: var(--font-size-sm);
}

.card__body {
  padding: var(--space-lg);
}

.card__footer {
  padding: var(--space-md) var(--space-lg);
  border-top: 1px solid var(--outline-subtle);
  background-color: var(--surface-subtle);
}

.card--borderless {
  border: none;
  box-shadow: none;
}

.card--flat {
  box-shadow: none;
  border: 1px solid var(--outline-subtle);
}
```

### Alert Component

The alert component provides status and notification styling:

```css
.alert {
  padding: var(--space-md) var(--space-lg);
  border-radius: var(--radius-md);
  border-left: 4px solid var(--outline-default);
  background-color: var(--surface-default);
  color: var(--text-default);
  margin-bottom: var(--space-md);
  display: flex;
  align-items: flex-start;
}

.alert__icon {
  flex-shrink: 0;
  margin-right: var(--space-md);
  width: 24px;
  height: 24px;
}

.alert__content {
  flex-grow: 1;
}

.alert__title {
  margin-top: 0;
  margin-bottom: var(--space-xs);
  font-weight: var(--font-weight-semibold);
  color: var(--text-overt);
}

.alert__message {
  margin: 0;
}

.alert__close {
  flex-shrink: 0;
  background: none;
  border: none;
  color: var(--text-subtle);
  cursor: pointer;
  padding: 0;
  margin-left: var(--space-sm);
  transition: color var(--animation-duration-fast) var(--ease-in-out);
}

.alert__close:hover {
  color: var(--text-default);
}

.alert--info {
  border-left-color: var(--info);
  background-color: var(--surface-info);
}

.alert--success {
  border-left-color: var(--success);
  background-color: var(--surface-success);
}

.alert--warning {
  border-left-color: var(--warning);
  background-color: var(--surface-warning);
}

.alert--error {
  border-left-color: var(--error);
  background-color: var(--surface-error);
}
```

### Badge Component

The badge component provides small status indicators:

```css
.badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: var(--font-size-xs);
  font-weight: var(--font-weight-semibold);
  line-height: 1;
  padding: 0.25em 0.75em;
  border-radius: var(--radius-full);
  background-color: var(--surface-subtle);
  color: var(--text-default);
  white-space: nowrap;
  vertical-align: middle;
}

.badge--success {
  background-color: var(--surface-success);
  color: var(--text-success);
}

.badge--warning {
  background-color: var(--surface-warning);
  color: var(--text-warning);
}

.badge--error {
  background-color: var(--surface-error);
  color: var(--text-error);
}

.badge--info {
  background-color: var(--surface-info);
  color: var(--text-info);
}

.badge--accent {
  background-color: var(--accent-subtle);
  color: var(--accent);
}

.badge--pill {
  border-radius: var(--radius-full);
  padding-left: 0.75em;
  padding-right: 0.75em;
}

.badge--outline {
  background-color: transparent;
  border: 1px solid currentColor;
}

.badge__dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color: currentColor;
  margin-right: 0.5em;
}
```

### Form Components

Enhanced form styling with validation states:

```css
.form-group {
  margin-bottom: var(--space-md);
}

.form-label {
  display: block;
  margin-bottom: var(--space-xs);
  font-weight: var(--font-weight-medium);
  color: var(--text-default);
}

.form-label--required::after {
  content: "*";
  color: var(--error);
  margin-left: 0.25em;
}

.form-help {
  display: block;
  margin-top: var(--space-xs);
  font-size: var(--font-size-sm);
  color: var(--text-subtle);
}

.form-input {
  display: block;
  width: 100%;
  padding: var(--space-sm) var(--space-md);
  font-family: inherit;
  font-size: var(--font-size-base);
  line-height: var(--line-height-normal);
  color: var(--text-default);
  background-color: var(--surface-default);
  border: 1px solid var(--outline-default);
  border-radius: var(--radius-md);
  transition: border-color var(--animation-duration-fast) var(--ease-in-out),
              box-shadow var(--animation-duration-fast) var(--ease-in-out),
              background-color var(--animation-duration-fast) var(--ease-in-out);
}

.form-input:focus {
  outline: none;
  border-color: var(--outline-focus);
  background-color: var(--input-focus-bg);
  box-shadow: 0 0 0 var(--input-focus-ring-width) var(--focus-ring-color);
}

.form-input::placeholder {
  color: var(--text-muted);
  opacity: 1;
}

.form-input:disabled, .form-input[readonly] {
  background-color: var(--surface-muted);
  color: var(--text-muted);
  cursor: not-allowed;
  opacity: 0.7;
}

.form-input--invalid {
  border-color: var(--outline-error);
}

.form-input--invalid:focus {
  border-color: var(--outline-error);
  box-shadow: 0 0 0 var(--input-focus-ring-width) rgba(var(--error-rgb), 0.25);
}

.form-error {
  display: block;
  margin-top: var(--space-xs);
  font-size: var(--font-size-sm);
  color: var(--text-error);
}

.form-select {
  appearance: none;
  background-image: url("data:image/svg+xml,..."); /* Dropdown arrow SVG */
  background-repeat: no-repeat;
  background-position: right var(--space-sm) center;
  padding-right: var(--space-xl);
}

.form-checkbox, .form-radio {
  display: flex;
  align-items: center;
  margin-bottom: var(--space-xs);
}

.form-checkbox__input, .form-radio__input {
  flex-shrink: 0;
  margin-right: var(--space-xs);
}

.form-checkbox__label, .form-radio__label {
  margin-bottom: 0;
  font-weight: var(--font-weight-normal);
}
```

### Navigation Components

Common navigation patterns:

```css
.nav {
  display: flex;
  gap: var(--space-xs);
  padding: 0;
  margin: 0;
  list-style: none;
}

.nav--vertical {
  flex-direction: column;
}

.nav__item {
  position: relative;
}

.nav__link {
  display: block;
  padding: var(--space-sm) var(--space-md);
  color: var(--text-default);
  text-decoration: none;
  border-radius: var(--radius-md);
  transition: color var(--animation-duration-fast) var(--ease-in-out),
              background-color var(--animation-duration-fast) var(--ease-in-out);
}

.nav__link:hover {
  color: var(--text-overt);
  background-color: var(--surface-subtle);
}

.nav__link:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

.nav__link--active {
  color: var(--accent);
  background-color: var(--accent-subtle);
  font-weight: var(--font-weight-medium);
}

.breadcrumb {
  display: flex;
  flex-wrap: wrap;
  padding: 0;
  margin: 0;
  list-style: none;
}

.breadcrumb__item {
  display: flex;
  align-items: center;
}

.breadcrumb__item:not(:last-child)::after {
  content: "/";
  margin: 0 var(--space-xs);
  color: var(--text-muted);
}

.breadcrumb__link {
  color: var(--text-subtle);
  text-decoration: none;
  transition: color var(--animation-duration-fast) var(--ease-in-out);
}

.breadcrumb__link:hover {
  color: var(--text-default);
}

.breadcrumb__link--active {
  color: var(--text-default);
  font-weight: var(--font-weight-medium);
}
```

### Modal Component

A dialog/modal component:

```css
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-md);
  background-color: oklch(from var(--bedrock) l c h / 0.8);
  z-index: var(--z-index-50);
  opacity: 0;
  visibility: hidden;
  transition: opacity var(--animation-duration-normal) var(--ease-in-out),
              visibility var(--animation-duration-normal) var(--ease-in-out);
}

.modal--active {
  opacity: 1;
  visibility: visible;
}

.modal__dialog {
  width: 100%;
  max-width: 32rem;
  max-height: calc(100vh - var(--space-xl));
  overflow-y: auto;
  background-color: var(--surface-default);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  transform: translateY(20px);
  transition: transform var(--animation-duration-normal) var(--ease-out);
}

.modal--active .modal__dialog {
  transform: translateY(0);
}

.modal__header {
  padding: var(--space-md) var(--space-lg);
  border-bottom: 1px solid var(--outline-subtle);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.modal__title {
  margin: 0;
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  color: var(--text-overt);
  line-height: 1.2;
}

.modal__close {
  background: none;
  border: none;
  color: var(--text-subtle);
  cursor: pointer;
  padding: var(--space-xs);
  transition: color var(--animation-duration-fast) var(--ease-in-out);
  border-radius: var(--radius-full);
}

.modal__close:hover {
  color: var(--text-default);
  background-color: var(--surface-subtle);
}

.modal__close:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

.modal__body {
  padding: var(--space-lg);
}

.modal__footer {
  padding: var(--space-md) var(--space-lg);
  border-top: 1px solid var(--outline-subtle);
  background-color: var(--surface-subtle);
  display: flex;
  gap: var(--space-sm);
  justify-content: flex-end;
}
```

### Accordion Component

A collapsible content component:

```css
.accordion {
  border: 1px solid var(--outline-subtle);
  border-radius: var(--radius-md);
  overflow: hidden;
}

.accordion__item:not(:last-child) {
  border-bottom: 1px solid var(--outline-subtle);
}

.accordion__header {
  margin: 0;
}

.accordion__button {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: var(--space-md) var(--space-lg);
  background-color: var(--surface-default);
  color: var(--text-default);
  border: none;
  text-align: left;
  cursor: pointer;
  transition: background-color var(--animation-duration-fast) var(--ease-in-out);
}

.accordion__button:hover {
  background-color: var(--surface-subtle);
}

.accordion__button:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: calc(-1 * var(--focus-ring-offset));
  position: relative;
  z-index: 1;
}

.accordion__icon {
  flex-shrink: 0;
  width: 20px;
  height: 20px;
  margin-left: var(--space-sm);
  transition: transform var(--animation-duration-fast) var(--ease-in-out);
}

.accordion__item--active .accordion__icon {
  transform: rotate(180deg);
}

.accordion__content {
  padding: var(--space-md) var(--space-lg);
  background-color: var(--surface-subtle);
  display: none;
}

.accordion__item--active .accordion__content {
  display: block;
}
```

### Enhanced Focus State Handling

The Components layer includes focus state handling for components:

```css
/* Focus-visible polyfill */
.js-focus-visible .focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

.js-focus-visible :focus:not(.focus-visible) {
  outline: none;
}

/* Enhanced input focus states */
.form-input:focus-visible, 
.form-select:focus-visible, 
.form-textarea:focus-visible {
  outline: var(--input-focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--input-focus-ring-offset);
  border-color: var(--outline-focus);
}
```

## Using the Components Layer

### Basic Component Usage

Components are used by applying their CSS classes:

```html
<!-- Button component -->
<button class="button">Default Button</button>
<button class="button button--small">Small Button</button>
<button class="button" disabled>Disabled Button</button>

<!-- Card component -->
<div class="card">
  <div class="card__header">
    <h2 class="card__title">Card Title</h2>
    <p class="card__subtitle">Card subtitle or metadata</p>
  </div>
  <div class="card__body">
    <p>Card content goes here.</p>
  </div>
  <div class="card__footer">
    <button class="button">Action</button>
  </div>
</div>

<!-- Alert component -->
<div class="alert alert--success">
  <div class="alert__icon">✓</div>
  <div class="alert__content">
    <h4 class="alert__title">Success!</h4>
    <p class="alert__message">Your changes have been saved successfully.</p>
  </div>
  <button class="alert__close" aria-label="Close">×</button>
</div>
```

### Component Composition

Components can be combined to create more complex UI patterns:

```html
<!-- Card with form -->
<div class="card">
  <div class="card__header">
    <h2 class="card__title">Contact Form</h2>
  </div>
  <div class="card__body">
    <form>
      <div class="form-group">
        <label for="name" class="form-label form-label--required">Name</label>
        <input type="text" id="name" class="form-input" placeholder="Enter your name">
      </div>
      <div class="form-group">
        <label for="email" class="form-label form-label--required">Email</label>
        <input type="email" id="email" class="form-input" placeholder="Enter your email">
        <span class="form-help">We'll never share your email with anyone else.</span>
      </div>
      <div class="form-group">
        <label for="message" class="form-label">Message</label>
        <textarea id="message" class="form-input" rows="4"></textarea>
      </div>
    </form>
  </div>
  <div class="card__footer">
    <button class="button button--filled-accent">Submit</button>
    <button class="button">Cancel</button>
  </div>
</div>
```

### Component Variants

Components often include variants for different states or appearances:

```html
<!-- Button variants -->
<button class="button">Default Button</button>
<button class="button button--filled-accent">Accent Button</button>
<button class="button button--outline-error">Error Outline</button>
<button class="button button--text-success">Success Text</button>

<!-- Card variants -->
<div class="card">Standard Card</div>
<div class="card card--flat">Flat Card</div>
<div class="card card--hover">Hover Card</div>
<div class="card card--borderless">Borderless Card</div>

<!-- Alert variants -->
<div class="alert">Default Alert</div>
<div class="alert alert--info">Info Alert</div>
<div class="alert alert--success">Success Alert</div>
<div class="alert alert--warning">Warning Alert</div>
<div class="alert alert--error">Error Alert</div>
```

## Customizing Components

### Extending Existing Components

To extend an existing component:

```css
@layer components {
  /* Add a new button variant */
  .button--gradient {
    background: linear-gradient(to right, var(--accent), var(--secondary));
    color: white;
    border: none;
  }
  
  .button--gradient:hover:not([disabled]) {
    background: linear-gradient(to right, var(--accent-overt), var(--secondary-overt));
    color: white;
  }
  
  /* Add a new card variant */
  .card--dashboard {
    border-radius: var(--radius-sm);
    box-shadow: none;
    border: 1px solid var(--outline-subtle);
    transition: transform var(--animation-duration-fast) var(--ease-in-out);
  }
  
  .card--dashboard:hover {
    transform: translateY(-4px);
  }
}
```

### Creating New Components

To create a new component:

```css
@layer components {
  /* Create a tooltip component */
  .tooltip {
    position: relative;
    display: inline-block;
  }
  
  .tooltip__content {
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%) translateY(-8px);
    padding: var(--space-xs) var(--space-sm);
    background-color: var(--surface-overt);
    color: var(--text-contrast-on-surface-overt);
    font-size: var(--font-size-sm);
    border-radius: var(--radius-sm);
    white-space: nowrap;
    pointer-events: none;
    opacity: 0;
    visibility: hidden;
    transition: opacity var(--animation-duration-fast) var(--ease-in-out),
                visibility var(--animation-duration-fast) var(--ease-in-out),
                transform var(--animation-duration-fast) var(--ease-in-out);
    z-index: var(--z-index-20);
  }
  
  .tooltip__content::after {
    content: "";
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    border-width: 4px;
    border-style: solid;
    border-color: var(--surface-overt) transparent transparent transparent;
  }
  
  .tooltip:hover .tooltip__content {
    opacity: 1;
    visibility: visible;
    transform: translateX(-50%) translateY(0);
  }
}
```

## Component Documentation

Each component should be documented with:

1. **Purpose**: What problem the component solves
2. **Usage**: When and how to use the component
3. **Variants**: Available modifiers and their purposes
4. **Accessibility**: Accessibility considerations
5. **Examples**: Sample code snippets

### Documentation Example

```md
## Card Component

The Card component is a flexible container for grouping and displaying content in a clean, organized way.

### Usage

Use cards to group related information and actions. Cards can contain text, images, links, and buttons.

### Variants

- `.card`: Standard card with shadow
- `.card--flat`: Card with border instead of shadow
- `.card--borderless`: Card without border or shadow
- `.card--hover`: Card with hover effect

### Subcomponents

- `.card__header`: Contains title and optional subtitle
- `.card__body`: Main card content area
- `.card__footer`: Action area at bottom of card

### Accessibility

- Ensure proper heading hierarchy within cards
- Use appropriate color contrast for all text
- Consider keyboard navigation if card is interactive

### Example

```html
<div class="card">
  <div class="card__header">
    <h3 class="card__title">Card Title</h3>
  </div>
  <div class="card__body">
    <p>Card content here.</p>
  </div>
  <div class="card__footer">
    <button class="button">Action</button>
  </div>
</div>
```
```

## Best Practices

1. **Follow BEM Naming**: Use Block-Element-Modifier convention for component class names
2. **Maintain Accessibility**: Ensure components meet WCAG guidelines
3. **Use Semantic Variables**: Reference semantic variables from the Theme layer
4. **Component Composition**: Design components to work well together
5. **Responsive Design**: Ensure components work well at all screen sizes
6. **Support States**: Account for hover, focus, active, and disabled states
7. **Documentation**: Document components thoroughly