# Power BI HTML Visuals

Use this skill whenever someone asks for a Power BI visual built from HTML/CSS/DAX
(KPI cards, gauges, donuts, custom bar/column charts, conditional-format badges,
country/category card grids, etc.) — whether they name a specific visual style or
just describe what they want to show ("progress to target", "a status badge for
this column", "compare two groups side by side").

## How to use this skill

1. Find the matching row in the **decision table** below by user intent.
2. Open **only** that visual's `visuals/<name>/notes.md` — it has the full DAX
   measure template, required inputs, and gotchas. Don't load other visuals'
   notes.md files unless the request genuinely spans more than one visual.
3. Check `shared/html-visual-binding.md` (full-canvas HTML cards) or
   `shared/conditional-format-binding.md` (single-cell badges) for the binding
   mechanics common to that visual's family — which custom visual it needs (if
   any), the placeholder token convention, and general pitfalls not repeated in
   every notes.md.
4. Check `shared/color-palette.md` before inventing new colors — reuse the
   existing tier/status conventions unless the user has their own brand palette.
5. Ask the user for the key inputs listed below (measure names, dimension/column
   names, thresholds) rather than guessing table/column names — every template
   uses `«MEASURE: ...»` / `«DIMENSION: ...»` placeholder tokens exactly where a
   real binding is needed.
6. If a visual's notes.md flags an ambiguous edge case (e.g. which of two similar
   sub-patterns applies), ask the user before picking one.

## Two visual families (different binding mechanism — see relevant shared doc)

- **Full-canvas HTML cards** — require the **HTML Content** custom visual (by
  Daniel Marsh-Patrick). One measure returns a complete HTML/CSS string.
- **Conditional-format badges** — no custom visual needed. A measure/column
  returns a `data:image/svg+xml` URI, bound via Power BI's native Image URL data
  category on a table/matrix column.

## Decision table

| User intent (examples) | Visual | Key inputs needed | notes.md | Status |
|---|---|---|---|---|
| "KPI card with a target and hover detail", "progress to revenue target" | `kpi-card-target-slide` | current value, target value, attainment %, gap | [visuals/kpi-card-target-slide/notes.md](visuals/kpi-card-target-slide/notes.md) | ✅ Ready |
| Same as above but wants a 3D flip instead of a slide | `kpi-card-target-flip` | same as slide variant | `visuals/kpi-card-target-flip/notes.md` | 🚧 Planned |
| Single KPI, no target — just value + change vs. prior period | `kpi-card-simple-blink` | current value, prior-period value/variance | `visuals/kpi-card-simple-blink/notes.md` | 🚧 Planned |
| "Status badge for this column", "color-code days on market / rating / category" | `cf-status-badge` | column/measure to classify, tier thresholds or category list, colors | [visuals/cf-status-badge/notes.md](visuals/cf-status-badge/notes.md) | ✅ Ready |
| "Row of yes/no amenity icons" | `cf-icon-status-row` | list of boolean columns to show as icons | `visuals/cf-icon-status-row/notes.md` | 🚧 Planned |
| "Pill-style category label in a table" (Customer/Investor/Partner style) | `cf-status-badge` (fixed-width categorical variant) | category list + one color per category | [visuals/cf-status-badge/notes.md](visuals/cf-status-badge/notes.md) | ✅ Ready (see "worked examples") |
| "Card grid, one per country/category, with a split metric" | `category-card-grid` | grouping dimension, total measure, 2+ way split measure | `visuals/category-card-grid/notes.md` | 🚧 Planned |
| "100% stacked horizontal bar by category" | `stacked-bar-100` | category list (fixed), sub-category breakdown measure | `visuals/stacked-bar-100/notes.md` | 🚧 Planned |
| "Horizontal bar list with a track, ranked/sorted" | `horizontal-bar-list` | category list, single measure, optional total for %s | `visuals/horizontal-bar-list/notes.md` | 🚧 Planned |
| "Grouped/clustered bars, 2 series side by side" | `clustered-bar` | 2 series measures, category list | `visuals/clustered-bar/notes.md` | 🚧 Planned |
| "Grouped/clustered vertical columns" | `clustered-column` | 2 series measures, category list | `visuals/clustered-column/notes.md` | 🚧 Planned |
| "Stacked vertical columns" | `stacked-column` | 2+ series measures, category list | `visuals/stacked-column/notes.md` | 🚧 Planned |
| "Donut chart, single, multi-segment" | `donut-single` | 2+ segment measures + total | `visuals/donut-single/notes.md` | 🚧 Planned |
| "Grid of small donuts, one per category" | `donut-grid` | category list, per-category measure + total | `visuals/donut-grid/notes.md` | 🚧 Planned |
| "Line/area trend, switchable metric" | `trend-line-field-param` | Field Parameter, one measure per switchable option | `visuals/trend-line-field-param/notes.md` | 🚧 Planned |
| "Dynamic narrative sentence describing a trend" | `narrative-summary` | comparison measure, base period, comparison period | `visuals/narrative-summary/notes.md` | 🚧 Planned |
| "Stat comparison card (e.g. average vs median, skew)" | `stat-comparison-card` | 2 related measures (avg/median or similar pair) per metric | `visuals/stat-comparison-card/notes.md` | 🚧 Planned |

## Status legend

- ✅ **Ready** — template + notes.md complete, safe to use directly.
- 🚧 **Planned** — identified from the source repo audit but not yet built into
  this skill's structure. If asked for one of these, tell the user it's not
  migrated yet rather than improvising from memory of the old repo file.

## Shared references

- [shared/html-visual-binding.md](shared/html-visual-binding.md) — HTML Content
  visual setup, measure-shape rules, placeholder token convention, general pitfalls
- [shared/conditional-format-binding.md](shared/conditional-format-binding.md) —
  Image URL data category setup, percent-encoding rules, sizing
- [shared/color-palette.md](shared/color-palette.md) — fonts, base colors, tier/status
  color conventions, sizing defaults
