- Specification for Missing Features in new.css

## 1. Enhanced High Contrast Mode Handling

Add the following to the `@layer theme` section:

```css
/* High Contrast Mode Enhancements */
@media (prefers-contrast: high) {
  :root {
    /* Refine existing contrast settings */
    --contrast-factor: 1.3;
    --l-threshold: 0.6;
    --c-threshold: 0.05;
    --surface-c: 0.005;
    
    /* Enhanced focus states */
    --focus-ring-width: 3px;
    --outline-focus: oklch(0.5 0.3 var(--accent-h));
    
    /* Increase border contrast */
    --border-width: 1.5px;
    --border-width-thick: 3px;
    
    /* Enhance text contrast */
    --text-subtle: oklch(0.3 0.03 var(--neutral-h));
    --text-muted: oklch(0.25 0.02 var(--neutral-h));
    
    /* Form elements */
    --outline-overt: oklch(0.4 0.1 var(--accent-h));
    --indicator-color: oklch(0 0 0);
  }
  
  @media (prefers-color-scheme: dark) {
    :root {
      --contrast-factor: 1.3;
      --l-threshold: 0.55;
      --c-threshold: 0.05;
      --surface-c: 0.01;
      
      /* Dark-specific high contrast adjustments */
      --text-subtle: oklch(0.85 0.02 var(--neutral-h));
      --text-muted: oklch(0.9 0.01 var(--neutral-h));
      --outline-overt: oklch(0.8 0.1 var(--accent-h));
      --indicator-color: oklch(1 0 0);
    }
  }
  
  /* Enhanced component contrast */
  input, select, textarea {
    border-width: var(--border-width-thick);
  }
  
  input[type="checkbox"], input[type="radio"] {
    border-width: 2px;
  }
}
```

## 2. Comprehensive Shadow System

Add to the `@layer tokens` or `@layer theme` section:

```css
/* Enhanced Shadow System */
:root {
  /* Shadow color base using HSL format for easier adjustments */
  --shadow-color-base: 220 10% 10%;
  --shadow-color-dark: 220 20% 90%;
  
  /* Light mode shadows */
  --shadow-sm: 0 1px 2px oklch(from hsl(var(--shadow-color-base)) l c h / 7%);
  --shadow-md: 0 4px 6px -1px oklch(from hsl(var(--shadow-color-base)) l c h / 10%), 
               0 2px 4px -2px oklch(from hsl(var(--shadow-color-base)) l c h / 10%);
  --shadow-lg: 0 10px 15px -3px oklch(from hsl(var(--shadow-color-base)) l c h / 10%), 
               0 4px 6px -4px oklch(from hsl(var(--shadow-color-base)) l c h / 10%);
  --shadow-xl: 0 20px 25px -5px oklch(from hsl(var(--shadow-color-base)) l c h / 10%), 
               0 8px 10px -6px oklch(from hsl(var(--shadow-color-base)) l c h / 10%);
  --shadow-inner: inset 0 2px 4px 0 oklch(from hsl(var(--shadow-color-base)) l c h / 5%);
  
  /* Semantic shadow assignments */
  --shadow-button: var(--shadow-sm);
  --shadow-button-hover: var(--shadow-md);
  --shadow-button-active: var(--shadow-inner);
  --shadow-card: var(--shadow-md);
  --shadow-dropdown: var(--shadow-lg);
  --shadow-modal: var(--shadow-xl);
}

@media (prefers-color-scheme: dark) {
  :root {
    /* Dark mode shadow adjustments */
    --shadow-color-base: var(--shadow-color-dark);
    --shadow-sm: 0 1px 2px oklch(from hsl(var(--shadow-color-base)) l c h / 10%);
    --shadow-md: 0 4px 6px -1px oklch(from hsl(var(--shadow-color-base)) l c h / 12%), 
                 0 2px 4px -2px oklch(from hsl(var(--shadow-color-base)) l c h / 12%);
    --shadow-lg: 0 10px 15px -3px oklch(from hsl(var(--shadow-color-base)) l c h / 12%), 
                 0 4px 6px -4px oklch(from hsl(var(--shadow-color-base)) l c h / 12%);
    --shadow-xl: 0 20px 25px -5px oklch(from hsl(var(--shadow-color-base)) l c h / 12%), 
                 0 8px 10px -6px oklch(from hsl(var(--shadow-color-base)) l c h / 12%);
    --shadow-inner: inset 0 2px 4px 0 oklch(from hsl(var(--shadow-color-base)) l c h / 7%);
  }
}
```

Add to `@layer utilities`:

```css
/* Enhanced Shadow Utilities */
.shadow-sm { box-shadow: var(--shadow-sm); }
.shadow-md { box-shadow: var(--shadow-md); }
.shadow-lg { box-shadow: var(--shadow-lg); }
.shadow-xl { box-shadow: var(--shadow-xl); }
.shadow-inner { box-shadow: var(--shadow-inner); }
.shadow-none { box-shadow: none; }
.shadow-card { box-shadow: var(--shadow-card); }
.shadow-dropdown { box-shadow: var(--shadow-dropdown); }
.shadow-modal { box-shadow: var(--shadow-modal); }
```

## 3. Enhanced Focus State Handling

Update the focus state handling:

```css
/* Add to @layer theme */
:root {
  /* Existing variables plus new ones */
  --focus-ring-width: 2px;
  --focus-ring-offset: 2px;
  --focus-ring-color: var(--outline-focus);
  --focus-ring-style: solid;
  
  /* Form element specific focus states */
  --input-focus-ring-width: var(--focus-ring-width);
  --input-focus-ring-offset: 0px;
  --input-focus-bg: transparent;
  --input-hover-border-color: var(--outline-overt);
}

/* Add to @layer components */
/* Enhanced Form Focus States */
input:focus-visible, select:focus-visible, textarea:focus-visible {
  outline: var(--input-focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--input-focus-ring-offset);
  background-color: var(--input-focus-bg);
  border-color: var(--outline-focus);
}

button:focus-visible, 
a:focus-visible,
[tabindex]:focus-visible {
  outline: var(--focus-ring-width) var(--focus-ring-style) var(--focus-ring-color);
  outline-offset: var(--focus-ring-offset);
  box-shadow: none;
}
```

## 4. More Explicit Link Styling

```css
/* Add to @layer theme */
:root {
  /* Enhanced link styling variables */
  --link-decoration: none;
  --link-decoration-hover: underline;
  --link-underline-thickness: 1.5px;
  --link-underline-offset: 0.15em;
  --link-transition-duration: var(--transition-duration, 150ms);
  --link-transition-timing: var(--transition-timing, ease-out);
}

/* Update in @layer components */
a {
  color: var(--text-link);
  text-decoration: var(--link-decoration);
  text-decoration-thickness: var(--link-underline-thickness);
  text-underline-offset: var(--link-underline-offset);
  transition: color var(--link-transition-duration) var(--link-transition-timing),
              text-decoration-color var(--link-transition-duration) var(--link-transition-timing);
}

a:hover, a:focus-visible {
  color: var(--text-link-hover);
  text-decoration: var(--link-decoration-hover);
  text-decoration-thickness: var(--link-underline-thickness);
  text-underline-offset: var(--link-underline-offset);
}
```

## 5. Named Container Query Breakpoints

```css
/* Add to @layer tokens or an appropriate section */
:root {
  /* Standardized container query breakpoints */
  --cq-bp-xs: 20em;  /* ~320px */
  --cq-bp-sm: 30em;  /* ~480px */
  --cq-bp-md: 45em;  /* ~720px */
  --cq-bp-lg: 60em;  /* ~960px */
  --cq-bp-xl: 80em;  /* ~1280px */
  --cq-bp-2xl: 96em; /* ~1536px */
  
  /* Container query configuration */
  --cq-type: inline-size;
  --cq-name: default;
}

/* Container query utilities, add to @layer utilities */
.cq-type-inline { container-type: inline-size; }
.cq-type-size { container-type: size; }
.cq-type-normal { container-type: normal; }

.cq-name-card { container-name: card; }
.cq-name-sidebar { container-name: sidebar; }
.cq-name-layout { container-name: layout; }
.cq-name-section { container-name: section; }
```

## Integration Instructions

1. These additions should be integrated carefully to maintain the cascade structure of new.css
2. Keep the additions consistent with the existing OKLCH-based color system
3. When implementing, be careful to check for any existing conflicting styles
4. Test thoroughly with high contrast mode and focus state testing
5. Update any documentation to reflect these new features
6. Consider documenting the enhanced shadow system with examples for developers

These changes will complement the advanced color system already in new.css while adding the missing features from reset.css.