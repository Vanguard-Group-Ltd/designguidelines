# Vanguard UI Design Guidelines

Vanguard's design system for **all** digital projects — customer-facing and internal tools. Structured
in three layers: **Method** (universal, mandatory), **Brand** (Portal-authoritative colour/type/motion),
**Application** (customer-facing vs internal-tool patterns and density). See `index.html` §0 for the
full framing, and `AGENTS.md` for a machine-readable version built for AI build agents.

## 🌐 Live Site

View the guidelines at: `https://[your-username].github.io/vanguard-ui-guidelines/`

## 📋 What's Included

- **Design Tokens**: Colours, typography, spacing (8pt system), icons
- **Navigation Patterns**: Global nav, command palette, tabs & segmented controls
- **Components**: Buttons, tags, inputs, tables, cards, alerts
- **Patterns**: Settings modals, interactive panels, dashboards
- **Accessibility**: WCAG AA compliance guidelines

## 🚀 Quick Start

### Option 1: GitHub Pages (Recommended)

1. Fork or clone this repository
2. Go to **Settings** → **Pages**
3. Under "Source", select **main** branch and **/ (root)** folder
4. Click **Save**
5. Your site will be live at `https://[username].github.io/vanguard-ui-guidelines/`

### Option 2: Local Development

Simply open `index.html` in your browser - no build step required.

## 📁 File Structure

```
vanguard-ui-guidelines/
├── index.html      # Complete guidelines, human-readable (self-contained)
├── AGENTS.md       # Same rules, machine-readable — for AI build agents
├── styles.css      # Design tokens + component CSS
├── README.md       # This file
└── .nojekyll       # Tells GitHub Pages not to process with Jekyll
```

## 🧭 The three layers

1. **Method** — mandatory on every project, no exceptions: derived status (never hand-written),
   search-first navigation with column filter+search as a required table capability, one semantic
   status set, radius by role, five interaction states + focus ring, AA, one icon system, reuse
   before you build.
2. **Brand** — colour, type, motion. **Portal-authoritative**: source of truth is the shipped
   `vanguard-portal-prototype` (`docs/design-system.md` + `public/assets/styles.css`). If this repo
   and the Portal ever disagree, the Portal wins.
3. **Application** — pick one per project: **customer-facing** (comfortable density, e.g. the
   Portal) or **internal tool** (compact density, dense tables, operational data-viz, e.g. WMS 2.0).
   WMS 2.0's current teal/Oracle Sans is a documented legacy exception to the Brand layer, pending a
   dedicated re-scope — not a second brand to copy into new projects.

## 🎨 Design Tokens Reference

### Brand Colours
- **Brand Blue** `#004674` — the primary colour. Buttons, active nav, headers, focus rings.
- **Brand Red** `#ED2124` — **logo only, never used in the UI.** Not for errors, not for
  destructive actions, not as an accent. This was a deliberate correction from the old site,
  which used red as its primary CTA colour.
- **Secondary — Sky Teal** `#6FBED9` (text/border variant `#1F6F8F`) — secondary CTAs, accents,
  links, hover/focus borders.
- **Danger / error** `#DC2626` — a distinct crimson, intentionally different from brand red.

### Spacing (4px base)
```css
--space-0: 4px;
--space-1: 8px;
--space-2: 12px;
--space-3: 16px;
--space-4: 20px;
--space-5: 24px;
--space-6: 32px;
--space-7: 40px;
--space-8: 48px;
```

### Radius (three named roles, not a numeric scale)
```css
--radius-interactive: 3px;   /* buttons, inputs, chips */
--radius-structural:  5px;   /* cards, tables, panels */
--radius-overlay:     6px;   /* modals, dropdowns, popovers */
--radius-full:        9999px; /* avatars, radio dots, pill badges */
```

### Typography
- **Font**: Plus Jakarta Sans (fallback: system-ui) — the closest free web match to the Vanguard
  brand font Gilroy, which isn't web-licensed. Inter was evaluated and rejected as not
  Gilroy-like enough.
- **Headings**: 700 weight
- **Body**: 400 weight
- **Labels**: 600 weight, 12px (uppercase micro-labels: 700 weight, 11px, letter-spacing)
- Every monetary/counting figure uses `font-variant-numeric: tabular-nums`.

## 🖨️ Printing

Click the "Print Guidelines" button in the bottom-right corner to print a clean version with table of contents (sidebar hidden).

## 📝 Version History

- **v5.2** - Locked the toolbar-layout criterion after review: the split is **not** informational vs.
  consequential in the abstract, it's **does this fire a command that mutates data/state** — if yes,
  right, always, however minor (New, Approve, Export, Columns); if no, left, always, however big or
  important (search, filters, scope controls). This fixes v5.1, which still had the wrong call on
  scope switches: a page-wide control like a branch/subsidiary switch is big and important but
  mutates nothing, so it stays left — it does **not** earn a spot on the right just because it's
  significant. Added the distinction between a page-level "Page Filters" row (scope + search,
  governs every table/KPI on the page, sits above the table area) and each table's own local
  toolbar (compact, scoped to just that dataset) — corrected `AGENTS.md`'s table-toolbar row, which
  still had "branch select" on the right from the pre-v5.1 Portal doc description.
- **v5.1** - Codified the toolbar layout rule as an explicit Method pattern: `Search + Filters` (left,
  informational/reversible) vs `Actions/Views` (right, consequential) — never interleaved. Corrected
  the §14 Tables demo, which was missing the Filters button the canonical pattern already has
  elsewhere, and corrected `AGENTS.md`'s table-toolbar row, which had copied the Portal's older
  "filter chips on the right" layout verbatim.
- **v5.0** - Restructured into three layers (Method / Brand / Application) so the guide honestly
  covers both a customer-facing site and an internal operational tool, not just the Portal. Added:
  the "How to use this guide" front-door, the derived-status and search+filter-on-column Method
  patterns, the internal-tool Application section (compact-by-default density, dense tables,
  operational data-viz palette), the `»` full-width primary CTA flourish as an explicit Brand rule,
  the WMS 2.0 teal/Oracle Sans documented-legacy-exception note, and `AGENTS.md` — a machine-readable
  version of this whole system for AI build agents.
- **v4.0** - Realigned to the shipped `vanguard-portal-prototype` design system: corrected brand
  red (was `#ff0000`, is `#ED2124`, logo-only — never UI), added the secondary teal colour
  (previously missing entirely), corrected font to Plus Jakarta Sans (was Inter), reframed radius
  as three named roles instead of a numeric scale, corrected button hierarchy (secondary = teal,
  danger = outlined not solid fill), corrected status tags to the {bg, border, text} triple
  pattern, added the "informational never salesy" voice rule and the reuse-before-you-build
  principle.
- **v2.0** - Customer portal focus, global navigation, command palette, settings modals
- **v1.1** - Expanded colours, segmented controls, tags, progress bars
- **v1.0** - Initial release

## 📄 License

Internal use only - Vanguard Group NZ
