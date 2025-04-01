# Palette Layer

The Palette layer defines comprehensive color palettes and scales for UI elements and data visualization. While the Theme layer provides semantic color roles, the Palette layer offers a complete range of color options for more specific use cases.

## Core Concept

The Palette layer creates systematic color scales with consistent steps in lightness and chroma, making it easy to represent hierarchies, states, and data. These color scales are implemented using OKLCH color space for perceptual uniformity and better color harmony.

## Color Scales

### Gray Scales

The framework provides multiple grayscale options with different undertones:

```css
/* Cool Gray Scale (default) */
--gray-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--gray-h));
--gray-1: oklch(var(--scale-l-1) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--gray-h));
--gray-2: oklch(var(--scale-l-2) var(--scale-c-1) var(--gray-h));
/* ... continuing to --gray-12 */

/* Neutral Gray Scale (no undertone) */
--neutral-0: oklch(var(--scale-l-0) 0 var(--neutral-h));
--neutral-1: oklch(var(--scale-l-1) 0 var(--neutral-h));
--neutral-2: oklch(var(--scale-l-2) 0 var(--neutral-h));
/* ... continuing to --neutral-12 */
```

### Brand Color Scales

Complete scales for brand colors with 13 steps (0-12):

```css
/* Accent Color Scale (Primary Brand) */
--accent-palette-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--primary-h));
--accent-palette-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--primary-h));
--accent-palette-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--primary-h));
--accent-palette-3: oklch(var(--scale-l-3) var(--scale-c-4) var(--primary-h));
--accent-palette-4: oklch(var(--scale-l-4) var(--scale-c-5) var(--primary-h));
--accent-palette-5: oklch(var(--scale-l-5) var(--scale-c-6) var(--primary-h));
--accent-palette-6: oklch(var(--scale-l-6) var(--scale-c-7) var(--primary-h));
--accent-palette-7: oklch(var(--scale-l-7) var(--scale-c-8) var(--primary-h));
--accent-palette-8: oklch(var(--scale-l-8) var(--scale-c-9) var(--primary-h));
--accent-palette-9: oklch(var(--scale-l-9) var(--scale-c-8) var(--primary-h));
--accent-palette-10: oklch(var(--scale-l-10) var(--scale-c-7) var(--primary-h));
--accent-palette-11: oklch(var(--scale-l-11) var(--scale-c-6) var(--primary-h));
--accent-palette-12: oklch(var(--scale-l-12) min(var(--scale-c-5), var(--clamp-max-c-12)) var(--primary-h));
```

### Status Color Scales

Complete scales for status indicators with 13 steps (0-12):

```css
/* Success Palette */
--success-palette-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--success-h));
--success-palette-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--success-h));
--success-palette-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--success-h));
/* ... continuing to --success-palette-12 */

/* Warning Palette */
--warning-palette-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--warning-h));
--warning-palette-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--warning-h));
--warning-palette-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--warning-h));
/* ... continuing to --warning-palette-12 */

/* Error Palette */
--error-palette-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--error-h));
--error-palette-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--error-h));
--error-palette-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--error-h));
/* ... continuing to --error-palette-12 */

/* Info Palette */
--info-palette-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--info-h));
--info-palette-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--info-h));
--info-palette-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--info-h));
/* ... continuing to --info-palette-12 */
```

### Extended Color Palette

A comprehensive set of color scales for data visualization and UI design:

```css
/* Red */
--red-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 0);
--red-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 0);
--red-2: oklch(var(--scale-l-2) var(--scale-c-3) 0);
/* ... continuing to --red-12 */

/* Orange */
--orange-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 30);
--orange-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 30);
--orange-2: oklch(var(--scale-l-2) var(--scale-c-3) 30);
/* ... continuing to --orange-12 */

/* Yellow */
--yellow-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 85);
--yellow-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 85);
--yellow-2: oklch(var(--scale-l-2) var(--scale-c-3) 85);
/* ... continuing to --yellow-12 */

/* Green */
--green-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 140);
--green-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 140);
--green-2: oklch(var(--scale-l-2) var(--scale-c-3) 140);
/* ... continuing to --green-12 */

/* Cyan */
--cyan-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 195);
--cyan-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 195);
--cyan-2: oklch(var(--scale-l-2) var(--scale-c-3) 195);
/* ... continuing to --cyan-12 */

/* Blue */
--blue-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 240);
--blue-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 240);
--blue-2: oklch(var(--scale-l-2) var(--scale-c-3) 240);
/* ... continuing to --blue-12 */

/* Purple */
--purple-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 280);
--purple-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 280);
--purple-2: oklch(var(--scale-l-2) var(--scale-c-3) 280);
/* ... continuing to --purple-12 */

/* Pink */
--pink-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 320);
--pink-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 320);
--pink-2: oklch(var(--scale-l-2) var(--scale-c-3) 320);
/* ... continuing to --pink-12 */
```

### Specialized Color Scales

Additional color scales for specific use cases:

```css
/* Slate - Blue-gray variant */
--slate-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 225);
--slate-1: oklch(var(--scale-l-1) min(var(--scale-c-1), var(--clamp-max-c-0)) 225);
--slate-2: oklch(var(--scale-l-2) var(--scale-c-1) 225);
/* ... continuing to --slate-12 */

/* Amber - Yellow-orange variant */
--amber-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 65);
--amber-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 65);
--amber-2: oklch(var(--scale-l-2) var(--scale-c-3) 65);
/* ... continuing to --amber-12 */

/* Teal - Blue-green variant */
--teal-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) 175);
--teal-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) 175);
--teal-2: oklch(var(--scale-l-2) var(--scale-c-3) 175);
/* ... continuing to --teal-12 */
```

## Color Palette Design

### Scale Structure

Each color scale follows a consistent pattern:

1. **Steps 0-2**: Very light shades (subtle backgrounds, highlights)
2. **Steps 3-5**: Light shades (backgrounds, subtle UI elements)
3. **Steps 6-8**: Mid-range shades (primary UI elements, borders)
4. **Steps 9-11**: Dark shades (text, prominent elements)
5. **Step 12**: Darkest shade (headings, emphasizing text)

### Color Scale Design Principles

The palette follows these key principles:

1. **Perceptual Uniformity**: Each step in the scale represents a similar perceptual difference
2. **Consistent Lightness**: The same lightness values are used across different hues
3. **Systematic Chroma**: Color intensity increases in the middle of the scale and decreases at the extremes
4. **Gamut Mapping**: Colors are clamped to ensure they're displayable on standard screens
5. **Accessibility**: The scale is designed to provide sufficient contrast options

### Special Considerations

#### Near-White and Near-Black Colors

The palette uses special handling for the extremes of the scale:

- **Near-White Colors (0-1)**: Limited chroma to prevent "off-white" appearances
- **Near-Black Colors (11-12)**: Limited chroma to prevent overly saturated dark colors

```css
/* Clamping chroma at the extremes */
--clamp-max-c-0: 0.03;  /* Max chroma for near-whites */
--clamp-max-c-12: 0.04; /* Max chroma for near-blacks */
```

#### Neutral vs. Tinted Grayscale

The framework provides both neutral and tinted grayscales:

- **Neutral**: True gray with zero chroma (pure grayscale)
- **Gray**: Slightly tinted grayscale with a cool undertone (default)

This allows more design flexibility while maintaining a cohesive look.

## Using the Palette Layer

### Direct Usage

The palette can be used directly for specific design needs:

```css
.data-visualization-element-1 {
  background-color: var(--blue-6);
}

.data-visualization-element-2 {
  background-color: var(--orange-6);
}

.data-visualization-element-3 {
  background-color: var(--green-6);
}
```

### In Data Visualizations

The palette is particularly useful for data visualizations:

```css
.chart-category-1 { background-color: var(--blue-6); }
.chart-category-2 { background-color: var(--green-6); }
.chart-category-3 { background-color: var(--purple-6); }
.chart-category-4 { background-color: var(--orange-6); }
.chart-category-5 { background-color: var(--red-6); }
```

### For Sequential Data

For sequential or gradient data, use steps from the same hue:

```css
.heat-map-level-1 { background-color: var(--red-2); }
.heat-map-level-2 { background-color: var(--red-4); }
.heat-map-level-3 { background-color: var(--red-6); }
.heat-map-level-4 { background-color: var(--red-8); }
.heat-map-level-5 { background-color: var(--red-10); }
```

### Creating Color Harmonies

The palette makes it easy to create color harmonies:

```css
/* Complementary Color Pair */
.primary { color: var(--blue-8); }
.complementary { color: var(--orange-8); }

/* Analogous Colors */
.primary { color: var(--blue-8); }
.analogous-1 { color: var(--cyan-8); }
.analogous-2 { color: var(--purple-8); }

/* Triadic Colors */
.triadic-1 { color: var(--blue-8); }
.triadic-2 { color: var(--red-8); }
.triadic-3 { color: var(--green-8); }
```

## Extending the Palette

### Adding Custom Colors

To add a new color to the palette:

```css
@layer palette {
  :root {
    /* Adding a custom "Rose" palette */
    --rose-h: 345; /* Define the hue */
    
    /* Generate the scale */
    --rose-0: oklch(var(--scale-l-0) min(var(--scale-c-1), var(--clamp-max-c-0)) var(--rose-h));
    --rose-1: oklch(var(--scale-l-1) min(var(--scale-c-2), var(--clamp-max-c-0)) var(--rose-h));
    --rose-2: oklch(var(--scale-l-2) var(--scale-c-3) var(--rose-h));
    /* ... and so on */
  }
}
```

### Creating Custom Palette Variants

For special needs, you can create palette variants:

```css
@layer palette {
  /* High saturation palette variant for vibrant designs */
  .high-saturation {
    --scale-c-3: 0.09;
    --scale-c-4: 0.12;
    --scale-c-5: 0.15;
    --scale-c-6: 0.18;
    --scale-c-7: 0.21;
    --scale-c-8: 0.24;
    --scale-c-9: 0.27;
  }
  
  /* Pastel palette variant for softer designs */
  .pastel {
    --scale-c-3: 0.04;
    --scale-c-4: 0.06;
    --scale-c-5: 0.08;
    --scale-c-6: 0.10;
    --scale-c-7: 0.12;
    --scale-c-8: 0.14;
    --scale-c-9: 0.16;
  }
}
```

## Complete Palette Reference

The palette includes these complete color scales (each with steps 0-12):

### Grayscale
- `--gray-{0-12}`: Cool gray (default)
- `--neutral-{0-12}`: True neutral gray

### Primary Palettes
- `--accent-palette-{0-12}`: Primary brand color scale
- `--success-palette-{0-12}`: Success color scale
- `--warning-palette-{0-12}`: Warning color scale
- `--error-palette-{0-12}`: Error color scale
- `--info-palette-{0-12}`: Info color scale

### Extended Color Palette
- `--red-{0-12}`: Red scale
- `--orange-{0-12}`: Orange scale
- `--amber-{0-12}`: Amber scale (yellow-orange)
- `--yellow-{0-12}`: Yellow scale
- `--lime-{0-12}`: Lime scale (yellow-green)
- `--green-{0-12}`: Green scale
- `--emerald-{0-12}`: Emerald scale (blue-green)
- `--teal-{0-12}`: Teal scale
- `--cyan-{0-12}`: Cyan scale
- `--sky-{0-12}`: Sky blue scale
- `--blue-{0-12}`: Blue scale
- `--indigo-{0-12}`: Indigo scale
- `--violet-{0-12}`: Violet scale
- `--purple-{0-12}`: Purple scale
- `--fuchsia-{0-12}`: Fuchsia scale
- `--pink-{0-12}`: Pink scale
- `--rose-{0-12}`: Rose scale (red-pink)

## Best Practices

1. **Use Semantic Variables**: For interface elements, prefer semantic variables from the Theme layer
2. **Consistent Step Usage**: Use the same step numbers across different hues for consistent visual weight
3. **Consider Accessibility**: Ensure sufficient contrast, especially for text elements
4. **Color Harmony**: Use related colors within the palette for harmony
5. **Dark Mode Considerations**: Test palette usage in both light and dark modes
6. **Data Visualization**: Reserve direct palette usage primarily for data visualization
7. **Document Custom Additions**: When extending the palette, document new colors and their intended use