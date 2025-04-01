# Engine Layer

The Engine layer is the computational heart of our CSS framework, containing the complex calculations and functions that power dynamic color manipulation, contrast calculations, and other mathematical operations.

## Core Concept

While the Tokens layer defines raw values and the Theme layer applies semantic meaning, the Engine layer provides the mathematical machinery to dynamically compute values based on context. This enables powerful features like automatic contrast adjustment, color transformations, and theme adaptations.

The Engine layer leverages modern CSS functions including:
- `calc()` for numerical computations
- `clamp()` for value constraints
- `oklch()` for color manipulation
- Color adjustment functions for transforms

## Key Features

### Auto-Contrast Calculation

The most prominent feature of the Engine layer is the automatic contrast calculation system. This dynamically adjusts text color based on background color to ensure readability:

```css
--auto-contrast-text: oklch(
  from var(--bg, var(--base))
  clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
  min(c, var(--c-threshold, 0.08))
  h
);
```

This complex calculation:
1. Takes the background color (`--bg` or falls back to `--base`)
2. Calculates an appropriate lightness value that contrasts with the background
3. Constrains the chroma (color intensity) to prevent vibrating text
4. Maintains the same hue for color harmony

### Color Transformations

The Engine provides systematic color transformations for creating consistent color variants:

```css
/* Muted variant - reduced chroma, slightly adjusted lightness */
--color-to-muted: oklch(
  from var(--color-base)
  calc(l * 0.97)
  calc(c * 0.3)
  h
);

/* Subtle variant - higher lightness, much lower chroma */
--color-to-subtle: oklch(
  from var(--color-base)
  calc(l * 1.15)
  calc(c * 0.12)
  h
);

/* Overt variant - slightly lower lightness, higher chroma */
--color-to-overt: oklch(
  from var(--color-base)
  calc(l * 0.85)
  calc(c * 1.2)
  h
);
```

### Dark Mode Adaptations

The Engine includes calculations for automatically adapting colors to dark mode:

```css
/* Dark mode color inversion - maintains similar perceived contrast */
--color-dark-mode: oklch(
  from var(--color-base)
  calc(1 - l * 0.85)
  calc(c * 0.85)
  calc(h)
);
```

### Responsive Value Scaling

The Engine provides calculations for contextually scaling values based on viewport size:

```css
/* Fluid typography scaling */
--responsive-text: clamp(
  var(--min-size, 1rem),
  calc(var(--min-size, 1rem) + (var(--max-size, 1.5rem) - var(--min-size, 1rem)) * 
    ((100vw - var(--min-viewport, 20rem)) / (var(--max-viewport, 80rem) - var(--min-viewport, 20rem)))),
  var(--max-size, 1.5rem)
);
```

## How the Engine Works

### Color Space Explanation

The Engine primarily uses OKLCH color space, which offers significant advantages:

- **Perceptual Uniformity**: Equal steps in OKLCH values correspond to equal perceived changes in color
- **Intuitive Control**: Separate control over lightness, chroma, and hue
- **Wider Gamut**: Access to colors outside sRGB
- **Better Interpolation**: More natural-looking transitions between colors

OKLCH parameters:
- **L (Lightness)**: 0-1 value representing perceptual lightness
- **C (Chroma)**: 0+ value representing color intensity (similar to saturation)
- **H (Hue)**: 0-360 degree value representing the color

### Contrast Calculation Details

The automatic contrast formula works as follows:

1. It extracts the lightness (l) from the background color
2. Compares it against a threshold (defaults to 0.65)
3. If the background is lighter than the threshold, it chooses a dark text color
4. If the background is darker than the threshold, it chooses a light text color
5. The chroma is reduced to improve readability
6. The hue is maintained for design consistency

```css
clamp(0.1, (var(--l-threshold, 0.65) / l - 1) * 999, 0.98)
```

This formula:
- Returns a value near 0.1 (dark) for light backgrounds
- Returns a value near 0.98 (light) for dark backgrounds
- Creates a sharp transition around the threshold value

### Color Mathematics in CSS

The Engine makes extensive use of CSS's color math capabilities:

```css
/* Extracting components from colors */
oklch(from var(--color) l c h)

/* Mathematical operations on components */
oklch(from var(--color) calc(l + 0.1) c h) /* Lighten */
oklch(from var(--color) calc(l - 0.1) c h) /* Darken */
oklch(from var(--color) l calc(c * 1.5) h) /* Saturate */
oklch(from var(--color) l calc(c * 0.5) h) /* Desaturate */
oklch(from var(--color) l c calc(h + 180)) /* Complement */
```

## Using the Engine Layer

### Direct Usage (Advanced)

The Engine layer is primarily used internally by the framework, but advanced users can leverage its capabilities directly:

```css
.custom-element {
  background-color: var(--custom-bg, var(--surface-default));
  color: oklch(
    from var(--custom-bg, var(--surface-default))
    clamp(0.1, (0.65 / l - 1) * 999, 0.98)
    min(c, 0.08)
    h
  );
}
```

### Extending the Engine

To add new calculations to the Engine layer:

```css
@layer engine {
  :root {
    /* Custom calculation for semi-transparent overlay */
    --overlay-color: oklch(
      from var(--base)
      calc(l * 0.8)
      calc(c * 0.5)
      h / 0.85
    );
    
    /* Custom calculation for text shadow color */
    --text-shadow-color: oklch(
      from var(--text-default)
      calc(l * 0.7)
      c
      h / 0.6
    );
  }
}
```

## Engine Variables Reference

### Contrast Calculations

```css
--auto-contrast-text
--auto-contrast-border
--high-contrast-text
--high-contrast-border
```

### Color Transformations

```css
--color-to-muted
--color-to-subtle
--color-to-overt
--color-to-dark-mode
--color-to-high-contrast
```

### Mathematical Helpers

```css
--l-delta-1-up
--l-delta-2-up
--l-delta-3-up
--l-delta-1-down
--l-delta-2-down
--l-delta-3-down
--c-delta-1-up
--c-delta-1-down
```

## Technical Limitations

While the Engine layer is powerful, it has some limitations:

1. **Browser Support**: Advanced color calculations require modern browsers
2. **Computation Cost**: Complex calculations may impact performance
3. **Debugging Complexity**: Dynamic calculated values can be harder to debug

## Best Practices

1. Use the Engine calculations through semantic variables from the Theme layer
2. Reserve direct usage of Engine calculations for advanced scenarios
3. Test across browsers to ensure calculations behave consistently
4. Consider providing fallbacks for browsers that don't support advanced calculations
5. Document custom calculations thoroughly