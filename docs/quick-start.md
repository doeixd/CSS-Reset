# Quick Start Guide

This guide will help you get started with our CSS framework quickly and efficiently.

## Installation

### Option 1: Use the CDN

The fastest way to get started is to include the framework via CDN:

```html
<link rel="stylesheet" href="https://cdn.example.com/css-framework/index.css">
```

### Option 2: Download the Files

You can download the complete framework or individual layer files from our GitHub repository:

1. Download the entire package from the [releases page](https://github.com/yourusername/css-framework/releases)
2. Extract the files to your project directory
3. Link to the CSS in your HTML

```html
<link rel="stylesheet" href="path/to/css-framework/index.css">
```

### Option 3: Use Individual Layers

If you only need specific features, you can import individual layers:

```html
<!-- Base layers -->
<link rel="stylesheet" href="path/to/css-framework/src/reset.css">
<link rel="stylesheet" href="path/to/css-framework/src/tokens.css">

<!-- Only what you need -->
<link rel="stylesheet" href="path/to/css-framework/src/utilities.css">
<link rel="stylesheet" href="path/to/css-framework/src/layouts.css">
```

## Basic Usage

### HTML Structure

The framework doesn't require any specific HTML structure, but here's a simple template to get started:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Project</title>
  <link rel="stylesheet" href="path/to/css-framework/index.css">
</head>
<body>
  <header>
    <nav>
      <!-- Navigation content -->
    </nav>
  </header>
  
  <main>
    <!-- Main content -->
  </main>
  
  <footer>
    <!-- Footer content -->
  </footer>
</body>
</html>
```

### Using Utility Classes

Utility classes are the core of the framework. They provide a way to apply styles directly in your HTML:

```html
<div class="bg-surface-default p-md rounded-md shadow-md">
  <h2 class="text-lg font-bold text-default mb-sm">Card Title</h2>
  <p class="text-subtle mb-md">Card description goes here.</p>
  <button class="button button-filled-accent">Action</button>
</div>
```

### Using Layout Components

Layout components provide structured ways to organize content:

```html
<div class="l-grid">
  <div class="bg-surface-subtle p-md rounded-md">Grid Item 1</div>
  <div class="bg-surface-subtle p-md rounded-md">Grid Item 2</div>
  <div class="bg-surface-subtle p-md rounded-md">Grid Item 3</div>
</div>

<div class="l-stack gap-lg">
  <h2>Stack Layout</h2>
  <p>Items stacked vertically with consistent spacing.</p>
  <button>Action</button>
</div>
```

## Dark Mode

The framework automatically supports dark mode based on user preference:

```html
<!-- This will automatically adapt to dark mode -->
<div class="bg-surface-default text-default p-md">
  Content adapts to dark mode automatically
</div>

<!-- Force dark mode regardless of user preference -->
<div class="dark bg-surface-default text-default p-md">
  Always in dark mode
</div>

<!-- Force light mode regardless of user preference -->
<div class="light bg-surface-default text-default p-md">
  Always in light mode
</div>
```

## Common Components

The framework includes several pre-styled components:

### Buttons

```html
<!-- Default button -->
<button class="button">Default Button</button>

<!-- Accent buttons -->
<button class="button button-filled-accent">Filled Accent</button>
<button class="button button-outline-accent">Outline Accent</button>
<button class="button button-text-accent">Text Accent</button>

<!-- Status buttons -->
<button class="button button-filled-success">Success</button>
<button class="button button-filled-warning">Warning</button>
<button class="button button-filled-error">Error</button>
```

### Form Elements

```html
<form class="l-stack gap-md">
  <div>
    <label for="name">Name</label>
    <input type="text" id="name" placeholder="Enter your name">
  </div>
  
  <div>
    <label for="email">Email</label>
    <input type="email" id="email" placeholder="Enter your email">
  </div>
  
  <div>
    <label for="message">Message</label>
    <textarea id="message" rows="4" placeholder="Your message"></textarea>
  </div>
  
  <button type="submit" class="button button-filled-accent">Submit</button>
</form>
```

## Customization

### Overriding CSS Variables

You can customize the framework by overriding CSS variables:

```css
:root {
  /* Customize colors */
  --accent-h: 250;
  --accent-s: 100%;
  --accent-l: 50%;
  
  /* Customize spacing */
  --space-md: 1.5rem;
  
  /* Customize typography */
  --font-family-sans: 'Montserrat', sans-serif;
  --font-size-base: 1.125rem;
}
```

### Creating Custom Components

Compose new components using existing utilities:

```css
.card {
  @apply bg-surface-default p-md rounded-md shadow-md;
}

.card__title {
  @apply text-lg font-bold text-default mb-sm;
}

.card__content {
  @apply text-subtle;
}
```

## Next Steps

- Explore the [Architecture](./architecture.md) to understand the layer system
- Learn about the [Tokens Layer](./layers/tokens.md) to customize design tokens
- Check out the [Utilities Layer](./layers/utilities.md) for all available utility classes
- Discover the [Layouts Layer](./layers/layouts.md) for layout patterns