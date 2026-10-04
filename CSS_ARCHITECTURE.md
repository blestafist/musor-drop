# CSS Architecture & Design System

## Overview
This project uses a **brutalist design aesthetic** with a dark gaming/case-opening theme. The CSS follows a custom property (CSS variables) approach for consistent theming and maintainability.

---

## Design Philosophy

### Brutalist Style Principles
- **Sharp corners** (`border-radius: 0`) for containers and UI elements
- **Bold borders** (3px solid) for clear visual separation
- **High contrast** colors with vibrant accents on dark backgrounds
- **No smooth transitions** (most elements use `transition: none`)
- **Grid-based layouts** with no gaps for a dense, structured appearance
- **Monospace/gaming fonts** (Russo One, Chakra Petch)

---

## CSS Variables (Custom Properties)

### Color System

```css
:root {
    /* Primary Brand Colors */
    --color-primary: #7C3AED;          /* Purple - main brand color */
    --color-on-primary: #FFFFFF;        /* Text on primary background */
    
    /* Secondary Colors */
    --color-secondary: #A78BFA;         /* Lighter purple */
    --color-on-secondary: #0F172A;      /* Text on secondary background */
    
    /* Accent Colors */
    --color-accent: #F43F5E;            /* Rose/Pink - CTAs and highlights */
    --color-on-accent: #000000;         /* Text on accent (black for contrast) */
    
    /* Background Colors */
    --color-background: #0F0F23;        /* Main page background - dark purple */
    --color-foreground: #E2E8F0;        /* Main text color */
    
    /* Surface Colors */
    --color-card: #1E1C35;              /* Card backgrounds */
    --color-card-foreground: #E2E8F0;   /* Text on cards */
    
    /* Muted Colors */
    --color-muted: #27273B;             /* Secondary backgrounds */
    --color-muted-foreground: #94A3B8;  /* Secondary text */
    
    /* Border & Focus */
    --color-border: #4C1D95;            /* Border color - purple */
    --color-ring: #7C3AED;              /* Focus ring color */
    
    /* Semantic Colors */
    --color-destructive: #EF4444;       /* Error/danger - red */
    --color-on-destructive: #000000;    /* Text on destructive */
    --color-success: #10B981;           /* Success/money - green */
    --color-warning: #F59E0B;           /* Warning/prices - amber */
    
    /* Utility Colors */
    --color-price: #FFD700;             /* Gold for prices */
    --color-secondary-text: #AAAAAA;    /* Tertiary text */
    --color-black: #000000;             /* Pure black */
}
```

### Color Usage Guidelines

| Variable | Use Case |
|----------|----------|
| `--color-primary` | Primary buttons, active states, focus indicators |
| `--color-accent` | CTA buttons, highlights, hover states, important elements |
| `--color-success` | Money/balance displays, success messages, sell buttons |
| `--color-warning` | Price displays, warning messages |
| `--color-destructive` | Error states, dangerous actions |
| `--color-border` | All borders throughout the interface |

---

## Typography

### Font Stack

```css
font-family: 'Chakra Petch', sans-serif;  /* Body text */
font-family: 'Russo One', sans-serif;     /* Headings, buttons, emphasis */
```

### Font Weights
- **Light**: 300
- **Regular**: 400
- **Medium**: 500
- **Semi-Bold**: 600
- **Bold**: 700

### Typography Patterns
- **Uppercase text**: Used for buttons, labels, and headings (`text-transform: uppercase`)
- **Letter spacing**: 1-2px for emphasis (`letter-spacing: 1px`)
- **Large numbers**: Balance and prices use large font sizes (32-48px) with `Russo One`

---

## Spacing System

### Borders
- **Standard border**: `3px solid var(--color-border)`
- **Thin border**: `2px solid var(--color-border)`

### Padding Patterns
- **Button padding**: `12px 28px` (nav), `16px 32px` (primary buttons)
- **Card padding**: `20px` (standard), `40px` (large containers)
- **Grid padding**: `40px` (main containers)

### Margin
- **Section spacing**: `40px` between major sections
- **Element spacing**: `16px`, `20px` between elements

---

## Layout Patterns

### Grid System
- **Cases grid**: `repeat(auto-fit, minmax(320px, 1fr))`
- **Collection grid**: `repeat(auto-fill, minmax(220px, 1fr))`
- **No gaps**: `gap: 0` with borders creating visual separation

### Border-Based Grid Effect
The layout uses a clever technique where adjacent items share borders:
```css
.case-card {
    border: 3px solid var(--color-border);
    border-right: none;
    border-bottom: none;
}

.case-card:nth-child(3n) {
    border-right: 3px solid var(--color-border);
}

.case-card:nth-last-child(-n+3) {
    border-bottom: 3px solid var(--color-border);
}
```

### Sticky Header
```css
.header {
    position: sticky;
    top: 0;
    z-index: 100;
}
```

---

## Component Styles

### Buttons

#### Primary Button (`.open-btn`)
```css
background: var(--color-primary);
border: none;
border-top: 3px solid var(--color-border);
padding: 16px 32px;
color: var(--color-on-primary);
text-transform: uppercase;
letter-spacing: 2px;
```

#### Hover State
```css
background: var(--color-accent);
color: var(--color-on-accent);
```

#### Secondary Button (`.open-btn-x20`)
```css
background: var(--color-warning);
color: var(--color-black);
```

### Cards

#### Case Card (`.case-card`)
```css
background: var(--color-card);
border: 3px solid var(--color-border);
text-align: center;
cursor: pointer;
transition: none;  /* Instant feedback */
```

#### Hover State
```css
background: var(--color-muted);
```

### Rarity Classes

Items have rarity-based styling with gradient backgrounds:

| Rarity | Gradient Colors |
|--------|----------------|
| Common | `#71717A` → `#52525B` (Gray) |
| Uncommon | `#22C55E` → `#16A34A` (Green) |
| Rare | `#3B82F6` → `#2563EB` (Blue) |
| Epic | `#A855F7` → `#9333EA` (Purple) |
| Legendary | `#F59E0B` → `#D97706` (Gold) |
| Mythic | `#EF4444` → `#DC2626` (Red) |
| Divine | `#06B6D4` → `#0891B2` → `#F43F5E` (Cyan to Rose) |

#### Divine Animation
```css
@keyframes divine-glow {
    0%, 100% {
        box-shadow: 0 0 30px rgba(6, 182, 212, 0.6), 
                    0 0 50px rgba(244, 63, 94, 0.4);
    }
    50% {
        box-shadow: 0 0 40px rgba(6, 182, 212, 0.8), 
                    0 0 70px rgba(244, 63, 94, 0.6);
    }
}
```

---

## Interaction Patterns

### Hover States
- **Instant feedback**: No transitions (`transition: none`)
- **Color change**: Primary → Accent or muted → highlighted
- **Scale**: Active states use `transform: scale(0.98)`

### Focus States
```css
select:focus, input:focus {
    outline: none;
    border-color: var(--color-primary);
}
```

### Scrollbar Styling
```css
::-webkit-scrollbar {
    height: 8px;
}

::-webkit-scrollbar-track {
    background: var(--color-background);
    border: 2px solid var(--color-border);
}

::-webkit-scrollbar-thumb {
    background: var(--color-primary);
    border: 2px solid var(--color-border);
}
```

---

## Modal & Overlay Patterns

### Modal Structure
```css
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(15, 15, 35, 0.95);
    z-index: 3000;
    display: flex;
    justify-content: center;
    align-items: center;
}
```

### Modal Content
```css
.modal-content {
    background: var(--color-card);
    border: 3px solid var(--color-border);
    box-shadow: 0 0 50px rgba(124, 58, 237, 0.3);
}
```

---

## Animation Patterns

### Opening Animation
- **Duration**: 4s
- **Easing**: `cubic-bezier(0.25, 0.1, 0.25, 1)` (ease-out)
- **Transform**: Horizontal slide (`translateX`)

### Progress Bar
```css
.progress-fill {
    transition: width 0.3s ease;
}
```

---

## Responsive Design

### Breakpoints
- Uses `auto-fit` and `auto-fill` for fluid grids
- Minimum card width: `220px` (collection), `320px` (cases)

### Mobile Considerations
- Sticky header remains visible
- Horizontal scroll for inventory/library in upgrader
- Touch-friendly button sizes

---

## Best Practices

### DO ✅
- Use CSS variables for all colors
- Maintain sharp corners (`border-radius: 0`)
- Use bold borders (3px) for structure
- Apply instant hover states (no transitions)
- Keep high contrast between text and backgrounds
- Use uppercase text for emphasis

### DON'T ❌
- Add rounded corners (breaks brutalist aesthetic)
- Use smooth transitions on interactive elements
- Use low-contrast color combinations
- Apply subtle shadows (use bold glows instead)
- Mix too many accent colors in one view

---

## File Structure

All styles are embedded in `<style>` tag within `index.html`:
```
index.html
├── <style>
│   ├── CSS Variables (root)
│   ├── Base Styles (*, body)
│   ├── Layout Components (.header, .container)
│   ├── UI Components (.button, .card, .modal)
│   ├── Rarity Classes (.common, .rare, etc.)
│   └── Utility Classes
└── <script> (JavaScript logic)
```

---

## Performance Considerations

- **No external CSS files**: Reduces HTTP requests
- **Minimal transitions**: Better performance, instant feedback
- **Simple gradients**: No complex background images
- **System fonts with fallbacks**: Google Fonts with `preconnect`

---

## Accessibility

### Color Contrast
- Text on dark backgrounds: Light colors (#E2E8F0)
- Text on light/accent backgrounds: Black (#000000)

### Interactive Elements
- Large click targets (min 44px height)
- Clear hover states
- Visible focus indicators

### Screen Readers
- Alt text on all images
- Semantic HTML structure
- ARIA labels where needed

---

## Maintenance Notes

### Adding New Colors
1. Add variable to `:root`
2. Document usage in this file
3. Apply consistently across components

### Modifying Rarity Colors
1. Update the specific rarity class
2. Ensure gradient colors maintain contrast
3. Test with white text overlay

### Adding New Components
1. Follow existing naming conventions
2. Use CSS variables (no hardcoded colors)
3. Maintain border-based grid system
4. Keep brutalist aesthetic (sharp corners, bold borders)

---

## Known Issues & Solutions

### Issue: Border Overlap in Grid
**Problem**: Adjacent items have double borders
**Solution**: Use `border-right: none` + `:nth-child()` to apply borders selectively

### Issue: Horizontal Scroll Not Working
**Problem**: Vertical scroll on horizontal containers
**Solution**: Use JavaScript wheel event handler with `preventDefault()`

### Issue: Modal Not Centering
**Problem**: Modal content offset
**Solution**: Use `display: flex` + `justify-content: center` + `align-items: center`

---

## Future Improvements

1. **Extract to separate CSS file** for better caching
2. **Add CSS custom properties for spacing** (e.g., `--spacing-md: 16px`)
3. **Implement dark/light theme toggle** using CSS variables
4. **Add print styles** for collection pages
5. **Optimize animations** using `will-change` property

---

## Quick Reference

### Common Patterns

```css
/* Standard card */
background: var(--color-card);
border: 3px solid var(--color-border);

/* Primary button */
background: var(--color-primary);
color: var(--color-on-primary);

/* Hover state */
background: var(--color-accent);
color: var(--color-on-accent);

/* Price display */
color: var(--color-warning);
font-family: 'Russo One', sans-serif;

/* Grid item */
border: 3px solid var(--color-border);
border-right: none;
border-bottom: none;
```

---

**Last Updated**: October 2026
**Version**: 1.0
**Maintainer**: Development Team
