# Defaults Layer

The Defaults layer defines the base styling for HTML elements, creating a consistent baseline appearance throughout your application. This layer applies semantic theme variables to raw HTML elements without requiring additional classes.

## Core Concept

While the Reset layer ensures consistent behavior by neutralizing browser defaults, the Defaults layer builds upon this by establishing a thoughtful set of default styles. Elements are styled using semantic variables from the Theme layer, creating an immediate connection to your design system right from the HTML foundation.

## Key Features

### Typography Defaults

The Defaults layer establishes a comprehensive typography system:

```css
body {
  font-family: var(--font-family-sans);
  font-size: var(--font-size-base);
  line-height: var(--line-height-normal);
  color: var(--text-default);
  background-color: var(--base);
}

h1, h2, h3, h4, h5, h6 {
  margin-top: var(--space-lg);
  margin-bottom: var(--space-sm);
  line-height: var(--line-height-tight);
  color: var(--text-overt);
  font-weight: var(--font-weight-bold);
}

h1 { font-size: var(--font-size-4xl); }
h2 { font-size: var(--font-size-3xl); }
h3 { font-size: var(--font-size-2xl); }
h4 { font-size: var(--font-size-xl); }
h5 { font-size: var(--font-size-lg); }
h6 { font-size: var(--font-size-md); }

p {
  margin-bottom: var(--space-md);
}

small {
  font-size: var(--font-size-sm);
}

strong, b {
  font-weight: var(--font-weight-bold);
  color: var(--text-overt);
}

em, i {
  font-style: italic;
}
```

### Link Styling

The Defaults layer includes comprehensive link styling with explicit states:

```css
a {
  color: var(--text-link);
  text-decoration-color: var(--text-link-underline, var(--text-link));
  text-decoration-thickness: var(--link-underline-width, 1px);
  text-underline-offset: var(--link-underline-offset, 0.15em);
  transition: color var(--animation-duration-fast) var(--ease-in-out),
              text-decoration-color var(--animation-duration-fast) var(--ease-in-out);
}

a:hover {
  color: var(--text-link-hover);
  text-decoration-color: var(--text-link-hover);
}

a:active {
  color: var(--text-link-active);
  text-decoration-color: var(--text-link-active);
}

a:visited {
  color: var(--text-link-visited);
  text-decoration-color: var(--text-link-visited);
}

a:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
  text-decoration: none;
}
```

### List Styling

Lists receive appropriate styling:

```css
ul, ol {
  margin-top: var(--space-sm);
  margin-bottom: var(--space-md);
  padding-left: var(--space-lg);
}

ul {
  list-style-type: disc;
}

ol {
  list-style-type: decimal;
}

li {
  margin-bottom: var(--space-xs);
}

li > ul, li > ol {
  margin-top: var(--space-xs);
  margin-bottom: var(--space-xs);
}
```

### Table Styling

Tables receive clean, accessible styling:

```css
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: var(--space-md);
  margin-bottom: var(--space-md);
  border: 1px solid var(--outline-subtle);
}

th {
  background-color: var(--surface-subtle);
  color: var(--text-default);
  font-weight: var(--font-weight-semibold);
  text-align: left;
  padding: var(--space-sm);
  border-bottom: 2px solid var(--outline-default);
}

td {
  padding: var(--space-sm);
  border-bottom: 1px solid var(--outline-subtle);
}

tr:last-child td {
  border-bottom: none;
}

tr:nth-child(even) {
  background-color: var(--surface-muted);
}

caption {
  margin-bottom: var(--space-xs);
  font-style: italic;
  color: var(--text-subtle);
  text-align: left;
}
```

### Form Element Styling

Form elements receive careful styling for consistency and accessibility:

```css
label {
  display: block;
  margin-bottom: var(--space-xs);
  font-weight: var(--font-weight-medium);
  color: var(--text-default);
}

input, select, textarea {
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

input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: var(--outline-focus);
  background-color: var(--input-focus-bg);
  box-shadow: 0 0 0 var(--input-focus-ring-width) var(--focus-ring-color);
}

input::placeholder, textarea::placeholder {
  color: var(--text-muted);
  opacity: 1;
}

input:disabled, select:disabled, textarea:disabled {
  background-color: var(--surface-muted);
  color: var(--text-muted);
  cursor: not-allowed;
  opacity: 0.7;
}

/* Button Styling */
button, input[type="button"], input[type="submit"], input[type="reset"] {
  display: inline-block;
  padding: var(--space-button-y, 0.7em) var(--space-button-x, 1.3em);
  font-family: inherit;
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
              box-shadow var(--animation-duration-fast) var(--ease-in-out);
}

button:hover:not([disabled]), 
input[type="button"]:hover:not([disabled]), 
input[type="submit"]:hover:not([disabled]), 
input[type="reset"]:hover:not([disabled]) {
  background-color: var(--surface-subtle);
  border-color: var(--outline-overt);
}

button:focus-visible, 
input[type="button"]:focus-visible, 
input[type="submit"]:focus-visible, 
input[type="reset"]:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

button:disabled, 
input[type="button"]:disabled, 
input[type="submit"]:disabled, 
input[type="reset"]:disabled {
  background-color: var(--surface-muted);
  color: var(--text-muted);
  border-color: var(--outline-muted);
  cursor: not-allowed;
  opacity: 0.7;
}
```

### Miscellaneous Elements

Other HTML elements also receive appropriate styling:

```css
/* Horizontal Rule */
hr {
  height: 1px;
  background-color: var(--outline-subtle);
  border: none;
  margin: var(--space-lg) 0;
}

/* Blockquote */
blockquote {
  padding: var(--space-md) var(--space-lg);
  margin: var(--space-md) 0;
  border-left: 4px solid var(--outline-default);
  background-color: var(--surface-subtle);
  color: var(--text-subtle);
  font-style: italic;
}

/* Code and Pre */
code {
  font-family: var(--font-family-mono);
  font-size: 0.9em;
  color: var(--text-highlight-overt);
  background-color: var(--highlight-bg-subtle);
  padding: 0.2em 0.4em;
  border-radius: var(--radius-sm);
}

pre {
  font-family: var(--font-family-mono);
  background-color: var(--surface-subtle);
  padding: var(--space-md);
  margin: var(--space-md) 0;
  border-radius: var(--radius-md);
  overflow-x: auto;
  border: 1px solid var(--outline-subtle);
}

pre code {
  background-color: transparent;
  padding: 0;
  color: var(--text-default);
}

/* Images */
img {
  max-width: 100%;
  height: auto;
  display: block;
  border-radius: var(--radius-sm);
}

figure {
  margin: var(--space-md) 0;
}

figcaption {
  margin-top: var(--space-xs);
  font-size: var(--font-size-sm);
  color: var(--text-subtle);
}
```

## Enhanced Accessibility Features

### Focus States

The Defaults layer includes enhanced focus state handling:

```css
/* Global focus style for keyboard navigation */
:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

/* Remove default focus style for mouse users */
:focus:not(:focus-visible) {
  outline: none;
}
```

### Custom Form Element States

Form elements receive accessible styling for all states:

```css
/* Custom checkbox styling */
input[type="checkbox"], input[type="radio"] {
  width: auto;
  margin-right: var(--space-xs);
}

input[type="checkbox"]:focus-visible, input[type="radio"]:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
}

/* Custom select styling */
select {
  appearance: none;
  background-image: url("data:image/svg+xml,..."); /* Dropdown arrow SVG */
  background-repeat: no-repeat;
  background-position: right var(--space-sm) center;
  padding-right: var(--space-xl);
}
```

### Screen Reader Utilities

The Defaults layer includes necessary screen reader utilities:

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

## Using the Defaults Layer

### Default HTML Elements

The Defaults layer applies styling to HTML elements automatically, without requiring additional classes:

```html
<h1>Page Title</h1>
<p>This is a paragraph with a <a href="#">link</a> and <strong>strong text</strong>.</p>

<ul>
  <li>List item one</li>
  <li>List item two</li>
</ul>

<table>
  <caption>Sample Table</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>Developer</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>Designer</td>
    </tr>
  </tbody>
</table>

<form>
  <div>
    <label for="name">Name</label>
    <input type="text" id="name" placeholder="Enter your name">
  </div>
  <button type="submit">Submit</button>
</form>
```

### Combining with Components and Utilities

The Defaults layer provides a solid foundation that can be enhanced with Components and Utilities layers:

```html
<!-- Default styles applied automatically -->
<h2>Product Features</h2>

<!-- Enhanced with component classes -->
<div class="card">
  <h3>Feature Name</h3>
  <p>Feature description goes here.</p>
</div>

<!-- Enhanced with utility classes -->
<button class="button-filled-accent mt-md">Get Started</button>
```

## Customizing the Defaults Layer

### Extending Default Styles

To extend or modify default styles, add to the Defaults layer:

```css
@layer defaults {
  /* Modify existing default styles */
  h1 {
    font-size: var(--font-size-5xl);
    letter-spacing: var(--letter-spacing-tight);
  }
  
  /* Add styling for additional elements */
  details {
    border: 1px solid var(--outline-subtle);
    border-radius: var(--radius-md);
    padding: var(--space-sm);
    margin-bottom: var(--space-md);
  }
  
  summary {
    font-weight: var(--font-weight-semibold);
    cursor: pointer;
    padding: var(--space-xs) 0;
  }
  
  details[open] summary {
    margin-bottom: var(--space-sm);
    border-bottom: 1px solid var(--outline-subtle);
  }
}
```

### Creating Variations

For significant variations, consider using cascade layers:

```css
@layer defaults.print {
  @media print {
    body {
      font-size: 12pt;
      color: black;
      background: none;
    }
    
    a {
      color: black;
      text-decoration: underline;
    }
    
    table, th, td {
      border: 1px solid #ddd;
    }
  }
}
```

## Complete Reference

### Typography Elements
- `body`: Base typography
- `h1`-`h6`: Headings
- `p`: Paragraphs
- `small`, `strong`, `b`, `em`, `i`: Text formatting
- `a`: Links (with states)
- `code`, `pre`: Code blocks
- `blockquote`: Quotes

### List Elements
- `ul`, `ol`: Lists
- `li`: List items

### Table Elements
- `table`: Tables
- `th`, `td`: Table cells
- `caption`: Table caption
- `tr`: Table rows

### Form Elements
- `form`: Form container
- `label`: Form labels
- `input`: Text inputs
- `input[type="checkbox"]`, `input[type="radio"]`: Checkboxes and radio buttons
- `select`, `option`: Dropdown menus
- `textarea`: Multi-line text input
- `button`, `input[type="button"]`, `input[type="submit"]`, `input[type="reset"]`: Buttons

### Miscellaneous Elements
- `hr`: Horizontal rule
- `img`: Images
- `figure`, `figcaption`: Image with caption
- `details`, `summary`: Accordion elements

## Best Practices

1. **Use Semantic HTML**: The Defaults layer is designed to work best with semantic HTML elements
2. **Preserve Default Styling**: Avoid overriding the Defaults layer for specific components; use the Components layer instead
3. **Maintain Accessibility**: When customizing, ensure you maintain or enhance accessibility features
4. **Test Responsively**: Default styles should work well at all viewport sizes
5. **Consider Print Styles**: Include print-specific adjustments for better printed output