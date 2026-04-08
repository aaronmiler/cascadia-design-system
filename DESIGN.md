# Cascadia Design System

## 1. Visual identity

Cascadia is a design system rooted in the Pacific Northwest. The palette comes from the Cascadia Doug Flag (forest green, deep blue, white), the Oregon state flag (navy, gold), and the Portland city flag (green, blue, yellow). These are identity colors, not decorative ones.

The system should feel recognizable across apps while letting each carry its own accent personality. Think of a well-run Portland coffee shop: intentional without being precious, warm without being cluttered.

**Typography** uses **Inter** — one family, three weights:
- **300** (Light): display headings only
- **400** (Regular): body text, inputs
- **500** (Medium): UI labels, emphasis, card titles

**Core constraints:**
- Forest green (`#00573F`) is always the primary brand color
- Border-radius stays between 6px and 8px (except pills at 9999px)
- Maximum font weight is 500 — never use 600, 700, or bold
- Sentence case everywhere — never uppercase (except table headers)
- Line-heights are generous: 1.50 minimum for readable text, 1.65 for body
- Every app gets one accent color from the palette (see Section 7)

## 2. Color palette

### Primary brand
| Name | Hex | Role |
|------|-----|------|
| Cascadia Green | `#00573F` | Navigation, headers, structural brand. Never use for interactive surfaces. |
| Cascadia Blue | `#002B5C` | Secondary brand, dark surfaces, depth |
| Cascadia Snow | `#F8FAFB` | Primary page background |

### Warm accents (flag-derived)
| Name | Hex | Role |
|------|-----|------|
| Oregon Gold | `#E4A520` | Default interactive accent — buttons, highlights |
| Portland Yellow | `#FFB81C` | Hover states, secondary accent, attention |
| Portland Green | `#046A38` | Alternative green accent |
| Portland Blue | `#418FDE` | Focus rings, alternative blue accent |

### Tertiary accents (PNW-derived)
| Name | Hex | Role |
|------|-----|------|
| Madrone | `#B87333` | Warm earth tone — Pacific madrone bark |
| Trout | `#2A9D8F` | Muted teal — steelhead iridescence |
| Huckleberry | `#8B5A8A` | Muted purple — mountain wildflowers |

### Neutral scale
| Name | Hex | Role |
|------|-----|------|
| PNW Ink | `#1A2332` | Primary text (near-black, slight blue undertone) |
| Timber | `#4A5568` | Secondary text, labels |
| Driftwood | `#A0AEC0` | Placeholders, disabled text, muted elements |
| Fog | `#E2E8F0` | Borders, dividers |
| Overcast | `#F1F5F9` | Subtle surface differentiation, card backgrounds |

### Interactive states
| State | Color | Notes |
|-------|-------|-------|
| Default | Oregon Gold `#E4A520` | Or the app's accent color via `--app-accent` |
| Hover | Portland Yellow `#FFB81C` | Or `--app-accent-hover` |
| Focus | Portland Blue `#418FDE` | Always Portland Blue, 2px offset ring |
| Active/pressed | Cascadia Green `#00573F` | |
| Destructive | `#C53030` | Muted red — not neon |

### Shadows
All shadows use `rgba(26, 35, 50, ...)` — a cool blue-black base:
| Level | Value | Use |
|-------|-------|-----|
| 1 | `0 1px 3px rgba(26, 35, 50, 0.08)` | Hovered cards, dropdowns |
| 2 | `0 4px 12px rgba(26, 35, 50, 0.12)` | Modals, popovers |
| 3 | `0 8px 24px rgba(26, 35, 50, 0.16)` | Full-screen overlays |

Prefer borders and background shifts over shadows. Shadows are a last resort for depth.

## 3. Typography

### Font stack
```
'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
```

### Type scale

| Role | Size | Weight | Line Height | CSS class |
|------|------|--------|-------------|-----------|
| Display hero | 48px / 3rem | 300 | 1.20 | `.display-hero` |
| Page heading | 32px / 2rem | 400 | 1.30 | `.page-heading` |
| Section heading | 24px / 1.5rem | 500 | 1.40 | `.section-heading` |
| Card title | 18px / 1.125rem | 500 | 1.40 | `.card-title` |
| Body | 16px / 1rem | 400 | 1.65 | `.body-text` |
| Body small | 14px / 0.875rem | 400 | 1.50 | `.body-small` |
| Caption / meta | 12px / 0.75rem | 500 | 1.50 | `.caption` |

### Rules
- **Sentence case only.** No uppercase transforms anywhere except table headers and badge text.
- **Size creates hierarchy**, not weight. Step through the size scale rather than reaching for bolder weights.
- **Three weights max**: 300, 400, 500. Nothing heavier, ever.
- **16px minimum for inputs** — prevents iOS zoom on focus.

## 4. Components

### Buttons
| Variant | Background | Text | Border | CSS class |
|---------|-----------|------|--------|-----------|
| Primary | `--app-accent` | PNW Ink | `--app-accent` | `.btn--primary` |
| Secondary | transparent | Cascadia Green | Cascadia Green | `.btn--secondary` |
| Ghost | transparent | Cascadia Green | none | `.btn--ghost` |
| Destructive | `#C53030` | white | `#C53030` | `.btn--destructive` |

- Border-radius: 6px
- Padding: `10px 20px` standard, `8px 14px` compact (`.btn--compact`)
- Font: 14px / weight 500
- Primary hover: shifts to `--app-accent-hover`, adds Level 1 shadow
- Secondary hover: fills with Cascadia Green, text goes white

### Cards
- Background: white or Overcast (`#F1F5F9`)
- Border: `1px solid` Fog
- Border-radius: 8px
- Padding: 20–24px
- Interactive cards (`.card--interactive`): Level 2 shadow on hover

### Navigation
- Background: Cascadia Green (default) or Cascadia Blue (`.nav-bar--dark`)
- Text: Cascadia Snow, 14px / weight 500
- Active link: accent-colored bottom border
- App name: displayed in the accent color
- **Always sticky** (`position: sticky; top: 0`)

**Accent navbar override:** When the app accent doesn't contrast well against green (Trout and Huckleberry need this), override the nav background to use the accent color:

| Variable | Default | Override for accent nav |
|----------|---------|----------------------|
| `--nav-bg` | Cascadia Green | `--app-accent` |
| `--nav-text` | Cascadia Snow | Cascadia Snow (unchanged) |
| `--nav-app-name` | `--app-accent` | `#fff` |
| `--nav-active` | `--app-accent` | `#fff` |

### Inputs & forms
- Border: `1px solid` Fog
- Border-radius: 6px
- Focus: `2px` ring in Portland Blue
- Background: white
- Padding: `10px 12px`
- Font: 16px / weight 400

### Tables
- Header row: Overcast background, Timber text, 12px / weight 500, **uppercase** (this is the one exception)
- Body rows: alternating white / Cascadia Snow
- Dividers: Fog, horizontal only
- Cell padding: `12px 16px`

### Badges & tags
- Border-radius: 9999px (pill)
- Font: 12px / weight 500
- Semantic colors: green (positive), gold (warning), muted red (negative), Fog (neutral), `--app-accent` (accent)

## 5. Layout

### Spacing
Base unit: **4px**. All spacing values are multiples of 4:

`4 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48 · 64 · 80`

CSS variables: `--space-1` (4px) through `--space-20` (80px).

### Grid
- Max content width: **1024px**, centered
- Side padding: 16px (mobile), 24px (tablet), 32px (desktop)
- Card grid: 1 column → 2 columns at 640px → 3 columns at 1024px

### Whitespace
- Generous between sections, dense where data lives (tables, forms, logs)
- Minimum tap target: **44px**
- Mobile-first: most daily use happens on a phone

### Border radius
| Token | Value | Use |
|-------|-------|-----|
| `--radius-sm` | 4px | Small inline elements |
| `--radius-md` | 6px | Buttons, inputs |
| `--radius-lg` | 8px | Cards, containers |
| `--radius-pill` | 9999px | Badges, tags |

Never go below 6px or above 8px for standard components. Pills are the only exception.

## 6. Depth & elevation

| Level | Shadow | Use |
|-------|--------|-----|
| 0 (Flat) | None — border only | Default state for cards, inputs |
| 1 (Raised) | `0 1px 3px rgba(26,35,50,0.08)` | Hovered cards, dropdowns |
| 2 (Floating) | `0 4px 12px rgba(26,35,50,0.12)` | Modals, popovers |
| 3 (Overlay) | `0 8px 24px rgba(26,35,50,0.16)` | Full-screen overlays |

When you need depth, first try a border or background color shift. Only add a shadow if those aren't enough.

## 7. Per-app accent system

Each app claims one accent as its identity color. The accent drives primary buttons, active nav indicators, key highlights, and the app icon tint.

| Accent | Hex | Source |
|--------|-----|--------|
| Oregon Gold | `#E4A520` | Oregon flag |
| Portland Yellow | `#FFB81C` | Portland flag |
| Portland Blue | `#418FDE` | Portland flag |
| Portland Green | `#046A38` | Portland flag |
| Madrone | `#B87333` | PNW-derived |
| Trout | `#2A9D8F` | PNW-derived |
| Huckleberry | `#8B5A8A` | PNW-derived |

Set the accent with two CSS custom properties on `:root` or `body`:
```css
--app-accent: #2A9D8F;       /* Trout */
--app-accent-hover: #35B5A5;  /* Lighter variant for hover */
```

## 8. Rules

### Always
- Cascadia Green for navigation and structural elements — it's the constant
- App accent for interactive elements: buttons, links, highlights
- Border-radius 6–8px on all standard components
- Sentence case for every heading
- Line-heights at 1.50+ for all readable text
- Mobile-first layout, desktop as progressive enhancement
- Fog / Overcast / Snow for creating depth without shadows

### Never
- Cascadia Green or Blue as button or interactive surface backgrounds — they're structural only
- Uppercase text (except table headers and badges)
- Border-radius below 6px or above 8px (except 9999px pills)
- Font weight above 500
- Colors outside the defined palette
- Drop shadows as a first choice for depth — use borders or background shifts first

## 9. Responsive behavior

### Breakpoints
| Name | Width | Behavior |
|------|-------|----------|
| Mobile | < 640px | Single column, bottom nav, compact forms, full-width inputs |
| Tablet | 640–1024px | Two columns, side nav optional |
| Desktop | > 1024px | Full layout, 1024px max-width centered |

### Collapsing rules
- Navigation: top bar → bottom tab bar on mobile
- Cards: grid → single stack
- Tables: horizontal scroll or card-per-row transformation
- Forms: full-width inputs on mobile, inline groups on desktop
- Primary action: always reachable — use a floating action button on mobile if needed

## 10. Quick reference

### Color lookup
| Role | Color | Hex |
|------|-------|-----|
| Page background | Cascadia Snow | `#F8FAFB` |
| Surface (cards) | White | `#FFFFFF` |
| Primary text | PNW Ink | `#1A2332` |
| Secondary text | Timber | `#4A5568` |
| Placeholder text | Driftwood | `#A0AEC0` |
| Border | Fog | `#E2E8F0` |
| Alt surface | Overcast | `#F1F5F9` |
| Brand / nav | Cascadia Green | `#00573F` |
| Default accent | Oregon Gold | `#E4A520` |
| Focus ring | Portland Blue | `#418FDE` |
| Destructive | — | `#C53030` |

### Adding Cascadia to a new app

1. Copy `cascadia.css` from this repo into the project's stylesheet directory
2. Link it in the HTML before any app-specific styles: `<link rel="stylesheet" href="cascadia.css">`
3. Pick an accent color from Section 7
4. Set `--app-accent` and `--app-accent-hover` on `:root` or `body`
5. If the accent doesn't contrast against the green nav, override `--nav-bg`, `--nav-app-name`, and `--nav-active` (see Section 4, Navigation)
6. Everything else — nav, typography, layout, neutrals — stays identical across apps
7. App icon/favicon: accent color on a Cascadia Green or Blue background
