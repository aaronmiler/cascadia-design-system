# Cascadia

A CSS design system drawn from the Pacific Northwest — the Cascadia Doug Flag, the Oregon state flag, and the Portland city flag.

One stylesheet. One font (Inter). Seven accent colors. Drop it into any project and it looks like yours.

## What's in here

- **`cascadia.css`** — The stylesheet. Copy this into your project.
- **`index.html`** — Visual reference showing every token, component, and variant. Open it in a browser or [view it on GitHub Pages](#) if enabled.
- **`DESIGN.md`** — Full specification: colors, typography, spacing, components, and rules. Written to be useful to both humans and coding assistants — feed it to your LLM and it'll know what to build.

## Quick start

1. Copy `cascadia.css` into your project
2. Link it before your app styles:
   ```html
   <link rel="stylesheet" href="cascadia.css">
   ```
3. Pick an accent color and set it:
   ```css
   :root {
     --app-accent: #2A9D8F;
     --app-accent-hover: #35B5A5;
   }
   ```
4. Build your UI with the provided classes (`.btn--primary`, `.card`, `.form-input`, etc.)

See [DESIGN.md](DESIGN.md) for the full spec and component reference.

## Accent colors

| Name | Hex |
|------|-----|
| Oregon Gold | `#E4A520` |
| Portland Yellow | `#FFB81C` |
| Portland Blue | `#418FDE` |
| Portland Green | `#046A38` |
| Madrone | `#B87333` |
| Trout | `#2A9D8F` |
| Huckleberry | `#8B5A8A` |

## Distribution

Copy the file. That's it. No package manager, no build step, no CDN. When you update the design system, copy the new version into your projects.
