# Design

Captured from `../karm/lib/theme/design_tokens.dart` and `../karm/lib/theme/app_colors.dart` — the canonical source of truth.

## Aesthetic direction

Organic Utility. Calm, grounded, purposeful. Like a well-worn field notebook.
Dark theme: deep forest night. Light theme: stone sage morning.
One accent per theme — never both at once.

## Color

### Backgrounds

| Role | Light | Dark |
|------|-------|------|
| Background | `#F3F5F2` — stone sage | `#141F16` — deep forest night |
| Surface (cards, sheets) | `#FFFFFF` | `#1E3022` |
| Sheet gradient top | `#FFFFFF` | `#253C28` |
| Sheet gradient bottom | `#EDF0EB` | `#1C2E1F` |

### Text

| Role | Light | Dark |
|------|-------|------|
| Primary text | `#1A2A1E` — deep sage ink | `#F2F6F3` — greenish white |

Alpha hierarchy (applied to primary text color):

| Level | Alpha | Use |
|-------|-------|-----|
| Primary | 1.00 | Body text |
| Secondary | 0.60 | Dates, sub-labels |
| Tertiary | 0.45 | Placeholders, footer |
| Disabled | 0.50 | Completed/inactive |
| Hairline | 0.08 | Dividers |

### Accent

| | Light | Dark |
|-|-------|------|
| Accent | `#4E8C60` — sage green | `#E8923C` — forest amber |
| On-accent text | `#FFFFFF` | `#1A0C00` |

Accent is theme-dependent. Never use the green in dark mode or amber in light mode.

### Status / Semantic

| | Light | Dark |
|-|-------|------|
| Done | `#3A7D44` | `#5DB36A` |
| Missed | `#D64045` | `#D46060` |
| Priority: High | `#D64045` | `#E85050` |
| Priority: Medium | `#CC7A00` | `#EAA020` |
| Priority: Low | `#5A7FDD` | `#6B9EFF` |

### Borders

| Light | Dark |
|-------|------|
| `#DFE8E0` | `#3E5444` |

### Age tier system (task urgency)

4 tiers by days carried. Gold → Amber → Orange → Coral Red. Full values in `app_colors.dart`.

## Typography

Two-family system. Fraunces for landmark/display text; Figtree for body and UI.

> Note: the landing page (`index.html`) currently uses DM Sans (Google Fonts). This diverges from the app. Align to Fraunces + Figtree when reshaping the landing.

| Role | Family | Size | Weight | Use |
|------|--------|------|--------|-----|
| Display | Fraunces | 26px | 600 | Date headers, empty state |
| Section title | Fraunces | 18px | 600 | Tab labels, nav |
| Task input | Fraunces | 22px | 500 | Add/edit task field |
| Task body | Figtree | 15px | 500 | Task title in list |
| Sheet row | Figtree | 15px | 400 | Options sheet rows |
| Label | Figtree | 13px | 600 | Chips, priority/tag labels |
| Caption | Figtree | 12px | 500 | Dates, badge text |
| Eyebrow | Figtree | 11px | 600 | Section caps (tracking: 0.8) |
| Micro | Figtree | 10px | 500 | Tag micro-labels (tracking: 0.5) |

Letter-spacing convention: negative tracking on display (-0.5), section titles (-0.3), task input (-0.2), task body (-0.1). Positive tracking only on eyebrow/micro labels.

## Spacing

4-point base unit. Named semantic levels:

| Token | Value | Use |
|-------|-------|-----|
| xs | 4px | Icon gaps, inline nudges |
| sm | 8px | Between related elements |
| md | 12px | Between grouped sections |
| lg | 20px | Screen/sheet horizontal padding (most common) |
| xl | 24px | Large section gaps |
| xxl | 32px | Between major layout zones |

## Border radius

| Token | Value | Use |
|-------|-------|-----|
| chip | 8px | Priority/tag chips |
| card | 12px | Small action buttons |
| sheet | 20px | Bottom sheets, context menus |
| full | 999px | Pills, FAB, avatars |
| handle | 2px | Drag handle bar |
| badge | 4px | Age badge accent strip |

## Motion

| Token | Duration | Use |
|-------|----------|-----|
| fast | 140ms | Button/chip state flips |
| normal | 200ms | Panel expand/collapse |
| slow | 300ms | Modal/page transitions |
| xslow | 400ms | Pulse, atmospheric |

Default curve: `easeInOut`. Entering: `easeOut`. Exiting: `easeIn`. No bounce. No elastic.

Always provide `prefers-reduced-motion` alternatives.

## Shadows / Elevation

- Sheets: blur 22, y-offset -3, black at 8% (light) / 32% (dark)
- Cards: blur 8, y-offset 2, black at 5% (light) / 20% (dark)

## Components

### Task tile
Background: surface color. Border radius: card (12px). Optional age-tier background/border tint. Task text at taskBody style. Secondary meta (date, tags) at caption with secondary alpha.

### Pills / chips
Border radius: full (999px). Label style (13px w600). Accent bg for "today"; selectedPill bg for other selected dates.

### Bottom sheets
Gradient from sheetTop → sheetBottom. Border radius: sheet (20px) top corners. Shadow: KarmShadow.sheet.

### App icon (landing)
96×96px, border-radius: 22px (iOS icon approximation).

## Landing page specifics

The landing (`index.html`) is a single centered viewport. No scroll intended. Current CSS vars:

```css
--bg: #141F16 / #F3F5F2
--text: #F2F6F3 / #1A2A1E
--text-60: rgba(text, 0.6)
--text-45: rgba(text, 0.45)
```

Driven by `prefers-color-scheme`. No JS. App Store badge: Apple Media Services SVG, height 44px, theme-switched via `<picture>` element.

**Contrast risk**: `--text-45` (footer text) at 0.45 opacity on `--bg` dark is approximately 3.2:1 — below WCAG AA for body text. Acceptable for 12px/500 only if treated as decorative; fails for meaningful content. Monitor.
