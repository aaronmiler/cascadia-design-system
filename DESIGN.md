# Cascadia Design System

## 1. Visual identity

Cascadia is a design system rooted in the Pacific Northwest. The palette comes from the Cascadia Doug Flag (forest green, deep blue, white), the Oregon state flag (navy, gold), and the Portland city flag (green, blue, yellow). These are identity colors, not decorative ones.

Cascadia is a **foundation, not a personality**. It gives a collection of apps connective tissue — shared tokens, components, and rules — while each app carries its own accent and layers its own feel on top (see Section 10, Extending Cascadia). Think of a well-run Portland coffee shop: intentional without being precious, warm without being cluttered.

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
- Every app gets one accent color from the palette (see Section 9)
- Components read **semantic tokens** (`--color-*`), never raw palette values

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

### Semantic tokens

Components never reference palette values directly — they read role tokens. This is the theming seam: the dark theme (Section 3) and any app-level retheme work by overriding these.

| Token | Light | Dark | Role |
|-------|-------|------|------|
| `--color-bg` | Snow | `#101823` | Page background |
| `--color-surface` | `#FFFFFF` | `#182231` | Cards, inputs, modals, menus |
| `--color-surface-alt` | Overcast | `#1F2B3C` | Table headers, sunken areas, ghost hover |
| `--color-text` | PNW Ink | `#E9EEF4` | Primary text |
| `--color-text-secondary` | Timber | `#A9B7C6` | Labels, supporting text |
| `--color-text-muted` | Driftwood | `#6E7E92` | Placeholders, disabled |
| `--color-border` | Fog | `#2C3A4E` | Borders, dividers |
| `--color-border-strong` | Driftwood | `#3D4E66` | Hovered borders, control outlines |
| `--color-brand` | Cascadia Green | unchanged | Structural surfaces (nav) |
| `--color-brand-fg` | Cascadia Green | `#4FB08F` | Green as text/border on the page |
| `--color-on-accent` | PNW Ink | unchanged | Text on `--app-accent` surfaces |
| `--color-focus` | Portland Blue | unchanged | Focus rings |
| `--color-destructive` | `#C53030` | unchanged | Destructive surfaces (buttons) |
| `--color-destructive-fg` | `#C53030` | `#F08C8C` | Destructive as text |
| `--color-code-fg` | Cascadia Blue | `#9FBEE8` | Inline code |
| `--color-backdrop` | `rgba(26,35,50,0.4)` | `rgba(0,0,0,0.6)` | Modal backdrop |

Semantic tints power badges and alerts — five pairs (`--tint-{positive,warning,negative,neutral,info}-bg/-fg`), each retuned for dark. All text/background pairs in both themes pass WCAG AA (4.5:1).

### Interactive states
| State | Color | Notes |
|-------|-------|-------|
| Default | Oregon Gold `#E4A520` | Or the app's accent color via `--app-accent` |
| Hover | Portland Yellow `#FFB81C` | Or `--app-accent-hover` |
| Focus | Portland Blue `#418FDE` | Always Portland Blue, 2px offset ring |
| Active/pressed | Cascadia Green `#00573F` | Plus a 1px downward press on buttons |
| Disabled | 50% opacity, `cursor: not-allowed` | Inputs use `--color-surface-alt` fill |
| Destructive | `#C53030` | Muted red — not neon |

### Shadows
Shadows are theme-aware tokens — blue-black in light, deeper black in dark:
| Level | Light value | Use |
|-------|-------------|-----|
| 1 | `0 1px 3px rgba(26, 35, 50, 0.08)` | Hovered cards, dropdowns, menus |
| 2 | `0 4px 12px rgba(26, 35, 50, 0.12)` | Modals, popovers, toasts, FAB |
| 3 | `0 8px 24px rgba(26, 35, 50, 0.16)` | Full-screen overlays |

Prefer borders and background shifts over shadows. Shadows are a last resort for depth.

## 3. Theming & dark mode

Dark mode is **opt-in per app** — some tools' personalities don't want it, and some accents read differently on dark. Nothing changes for an app that does nothing.

```html
<html data-theme="dark">   <!-- always dark -->
<html data-theme="auto">   <!-- follows the system -->
<html>                     <!-- always light (default) -->
```

- Dark values are hand-picked from the PNW night side (ink-blue surfaces, spruce-green brand text), not inverted. Every pair passes WCAG AA.
- The nav stays Cascadia Green in both themes — it is already a dark surface.
- Accent colors don't change between themes. If an app's accent underperforms on dark, either skip dark mode for that app or override tokens in the app stylesheet.
- Apply the attribute before first paint (server-side or an inline script) to avoid a flash when using a stored preference.

## 4. Typography

### Font stack
```
'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
```

### Type scale

| Role | Size | Weight | Line Height | Tracking | CSS class |
|------|------|--------|-------------|----------|-----------|
| Display hero | 48px / 3rem | 300 | 1.20 | −0.02em | `.display-hero` |
| Page heading | 32px / 2rem | 400 | 1.30 | −0.01em | `.page-heading` |
| Section heading | 24px / 1.5rem | 500 | 1.40 | 0 | `.section-heading` |
| Card title | 18px / 1.125rem | 500 | 1.40 | 0 | `.card-title` |
| Body | 16px / 1rem | 400 | 1.65 | 0 | `.body-text` |
| Body small | 14px / 0.875rem | 400 | 1.50 | 0 | `.body-small` |
| Caption / meta | 12px / 0.75rem | 500 | 1.50 | 0 | `.caption` |

### Rules
- **Sentence case only.** No uppercase transforms anywhere except table headers and badge text.
- **Size creates hierarchy**, not weight. Step through the size scale rather than reaching for bolder weights.
- **Three weights max**: 300, 400, 500. Nothing heavier, ever.
- **16px minimum for inputs** — prevents iOS zoom on focus.
- **Tabular figures for data.** Tables and stat values use `font-variant-numeric: tabular-nums` (also available as the `.tabular` utility) so columns of numbers align.

## 5. Motion

| Token | Value | Use |
|-------|-------|-----|
| `--duration-fast` | 120ms | Hovers, presses, color shifts |
| `--duration-base` | 180ms | Cards, progress fills, larger surfaces |
| `--ease` | `cubic-bezier(0.2, 0, 0, 1)` | Everything — quick start, soft landing |

- Transition **specific properties**, never `all`.
- Motion is quiet: color shifts, 1px lifts and presses, a skeleton shimmer. No bounces, no slides.
- `prefers-reduced-motion: reduce` flattens every transition and animation globally — this is built into `cascadia.css`.

## 6. Components

### Buttons
| Variant | Background | Text | Border | CSS class |
|---------|-----------|------|--------|-----------|
| Primary | `--app-accent` | `--color-on-accent` | `--app-accent` | `.btn--primary` |
| Secondary | transparent | `--color-brand-fg` | `--color-brand-fg` | `.btn--secondary` |
| Ghost | transparent | `--color-brand-fg` | none | `.btn--ghost` |
| Destructive | `--color-destructive` | white | `--color-destructive` | `.btn--destructive` |

- Border-radius: 6px
- Padding: `10px 20px` standard, `8px 14px` compact (`.btn--compact`)
- Font: 14px / weight 500
- Primary hover: shifts to `--app-accent-hover`, adds Level 1 shadow
- Secondary hover: fills with Cascadia Green, text goes white
- Active: 1px downward press
- Disabled: 50% opacity, no hover response

### Floating action button (`.fab`)
- 56px circle (a sanctioned pill exception), `--app-accent` background, Level 2 shadow
- Fixed bottom-right; automatically clears the tab bar on mobile when `<body>` has `.has-tab-bar`
- Use for the single primary action on mobile — always reachable

### Cards
- Background: `--color-surface` or `--color-surface-alt` (`.card--surface`)
- Border: `1px solid --color-border`
- Border-radius: 8px
- Padding: 20–24px
- Interactive cards (`.card--interactive`): Level **1** shadow + stronger border + 1px lift on hover

### Navigation
- Background: Cascadia Green (default) or Cascadia Blue (`.nav-bar--dark`) — both themes
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

### Tab bar (`.tab-bar`) — mobile bottom navigation
- Fixed to the bottom edge, shown only below 640px; `--color-surface` background, top border
- Items: icon over a 12px / weight 500 label, secondary text color; active item gets primary text color and a 2px accent indicator at the top edge
- Respects `env(safe-area-inset-bottom)`; add `.has-tab-bar` to `<body>` so content, FABs, and toasts clear it

### Inputs & forms
- Border: `1px solid --color-border`
- Border-radius: 6px
- Focus: `2px` ring in Portland Blue
- Background: `--color-surface`
- Padding: `10px 12px`
- Font: 16px / weight 400
- Disabled: `--color-surface-alt` fill, muted text, `cursor: not-allowed`

**Checkboxes, radios, switches** — wrap in `.form-check` (a `<label>` row with a 44px minimum tap target):
- `.form-checkbox`: 20px, 4px radius, fills with `--app-accent` and an ink checkmark when checked
- `.form-radio`: 20px circle, thick accent ring when checked
- `.switch`: 40×24px pill track, accent when on

### Tables
- Header row: `--color-surface-alt` background, secondary text, 12px / weight 500, **uppercase** (this is the one exception)
- Body rows: alternating `--color-surface`-transparent / `--color-bg`
- Dividers: `--color-border`, horizontal only
- Cell padding: `12px 16px`
- Tabular figures throughout

### Badges & tags
- Border-radius: 9999px (pill)
- Font: 12px / weight 500
- Variants map to the semantic tints: `.badge--positive`, `--warning`, `--negative`, `--neutral`, plus `.badge--accent` (`--app-accent` background)

### Alerts (`.alert`)
- Inline banners for persistent context; 8px radius, 14px text
- Neutral by default (`--color-surface-alt`); `.alert--info`, `--positive`, `--warning`, `--negative` use the tint pairs
- Optional `.alert-title` (weight 500) followed by body text
- Alerts explain what happened and what to do next — never vague, never apologetic

### Toasts (`.toast` in `.toast-stack`)
- Transient confirmations; inverted surface (ink in light, near-white in dark) so they read above any page
- Fixed bottom-right, full-width on mobile, clears the tab bar with `.has-tab-bar`
- Optional `.toast-action` (accent-colored) for undo-style follow-ups
- A toast confirms in the same words as the action: "Publish" → "Published"

### Tabs (`.tabs` / `.tab`)
- In-page section switching; same accent-underline language as nav active links
- Inactive: secondary text; hover: primary text; active (`.active` or `aria-selected="true"`): primary text + 2px accent underline
- Scrolls horizontally when it runs out of room

### Menu (`.menu` / `.menu-item`)
- Dropdown panel: `--color-surface`, 8px radius, Level 1 shadow, 8px padding
- Items: 14px, full-width, `--color-surface-alt` on hover; `.menu-item--destructive` for delete actions; `.menu-divider` to group
- Pairing with `<details>`, the Popover API, or app JS is the app's choice

### Progress (`.progress` / `.progress-fill`)
- 8px pill track on `--color-surface-alt` with a hairline border; accent fill
- Set the fill's inline `width`; it animates at `--duration-base`

### Skeleton (`.skeleton`)
- `--color-surface-alt` blocks with a slow shimmer; `.skeleton--text` and `.skeleton--circle` variants
- Shimmer stops under `prefers-reduced-motion`
- Match the skeleton's shape to the content it stands in for

### Empty state (`.empty-state`)
- Centered icon slot, title (18px / 500), one-sentence description, and a primary action
- An empty screen is an invitation to act — always give it a next step

### Breadcrumbs (`.breadcrumbs`)
- 14px inline path with muted `/` separators; links in secondary text, current page in primary
- Use `<ol>` with `aria-current="page"` on the last item

### Tooltips — deliberately omitted
CSS-only tooltips are hostile to touch, and Cascadia is mobile-first. Put the information in visible text, a caption, or an alert instead.

## 7. Layout

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
| `--radius-sm` | 4px | Small inline elements, checkboxes |
| `--radius-md` | 6px | Buttons, inputs |
| `--radius-lg` | 8px | Cards, containers |
| `--radius-pill` | 9999px | Badges, tags, switches, FAB |

Never go below 6px or above 8px for standard components. Pills are the only exception.

## 8. Depth & elevation

| Level | Shadow | Use |
|-------|--------|-----|
| 0 (Flat) | None — border only | Default state for cards, inputs |
| 1 (Raised) | `--shadow-1` | Hovered cards, dropdowns, menus |
| 2 (Floating) | `--shadow-2` | Modals, popovers, toasts, FAB |
| 3 (Overlay) | `--shadow-3` | Full-screen overlays |

When you need depth, first try a border or background color shift. Only add a shadow if those aren't enough.

## 9. Per-app accent system

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

## 10. Extending Cascadia

Cascadia is the connective tissue; personality belongs to the app. The boundary:

**The foundation owns** the palette, the neutral/semantic tokens, type scale, spacing, radius and weight constraints, and the component library. These stay identical across apps — that's what makes separate apps feel like they belong together.

**The app owns** its accent, its content and voice, and any feel layered on top — a texture, a motif, a custom hero. That work lives in the app's own stylesheet, *after* `cascadia.css`.

**The mechanism is token override, not selector fighting.** Components read `--color-*` tokens, so an app can retheme globally by redefining tokens — exactly how the accent system and the dark theme already work:

```css
/* the app's stylesheet, after cascadia.css */
:root {
  --app-accent: #2A9D8F;
  --color-bg: #F6FAF8;   /* example: a slightly green-cast page */
}
```

Add new app-specific components alongside Cascadia's, following the same constraints (radius 6–8px, weight ≤ 500, semantic tokens). Never edit your copy of `cascadia.css` — overrides survive the next copy-paste upgrade; edits don't.

## 11. Rules

### Always
- Cascadia Green for navigation and structural elements — it's the constant
- App accent for interactive elements: buttons, links, highlights
- Semantic tokens (`--color-*`) in every component and app style — never raw palette values
- Border-radius 6–8px on all standard components
- Sentence case for every heading
- Line-heights at 1.50+ for all readable text
- Mobile-first layout, desktop as progressive enhancement
- Fog / Overcast / Snow for creating depth without shadows
- Transition specific properties at `--duration-fast`/`--duration-base` with `--ease`

### Never
- Cascadia Green or Blue as button or interactive surface backgrounds — they're structural only
- Uppercase text (except table headers and badges)
- Border-radius below 6px or above 8px (except 9999px pills)
- Font weight above 500
- Colors outside the defined palette
- Drop shadows as a first choice for depth — use borders or background shifts first
- `transition: all` — name the properties
- Hardcoded hex values where a semantic token exists

## 12. Responsive behavior

### Breakpoints
| Name | Width | Behavior |
|------|-------|----------|
| Mobile | < 640px | Single column, `.tab-bar` bottom nav, compact forms, full-width inputs |
| Tablet | 640–1024px | Two columns, side nav optional |
| Desktop | > 1024px | Full layout, 1024px max-width centered |

### Collapsing rules
- Navigation: top bar → `.tab-bar` on mobile (add `.has-tab-bar` to `<body>`)
- Cards: grid → single stack
- Tables: horizontal scroll or card-per-row transformation
- Forms: full-width inputs on mobile, inline groups on desktop
- Primary action: always reachable — use `.fab` on mobile if needed
- Toasts: bottom-right stack → full-width above the tab bar

## 13. Quick reference

### Color lookup
| Role | Token | Light | Dark |
|------|-------|-------|------|
| Page background | `--color-bg` | Snow `#F8FAFB` | `#101823` |
| Surface (cards) | `--color-surface` | `#FFFFFF` | `#182231` |
| Alt surface | `--color-surface-alt` | Overcast `#F1F5F9` | `#1F2B3C` |
| Primary text | `--color-text` | PNW Ink `#1A2332` | `#E9EEF4` |
| Secondary text | `--color-text-secondary` | Timber `#4A5568` | `#A9B7C6` |
| Placeholder text | `--color-text-muted` | Driftwood `#A0AEC0` | `#6E7E92` |
| Border | `--color-border` | Fog `#E2E8F0` | `#2C3A4E` |
| Brand / nav | `--color-brand` | Cascadia Green `#00573F` | unchanged |
| Green as text | `--color-brand-fg` | Cascadia Green `#00573F` | `#4FB08F` |
| Default accent | `--app-accent` | Oregon Gold `#E4A520` | unchanged |
| Focus ring | `--color-focus` | Portland Blue `#418FDE` | unchanged |
| Destructive | `--color-destructive` | `#C53030` | unchanged |

### Adding Cascadia to a new app

1. Copy `cascadia.css` from this repo into the project's stylesheet directory
2. Link it in the HTML before any app-specific styles: `<link rel="stylesheet" href="cascadia.css">`
3. Pick an accent color from Section 9
4. Set `--app-accent` and `--app-accent-hover` on `:root` or `body`
5. If the accent doesn't contrast against the green nav, override `--nav-bg`, `--nav-app-name`, and `--nav-active` (see Section 6, Navigation)
6. Decide on dark mode: add `data-theme="dark"` or `"auto"` to `<html>`, or leave it off for always-light
7. Everything else — nav, typography, layout, neutrals — stays identical across apps
8. App icon/favicon: accent color on a Cascadia Green or Blue background
