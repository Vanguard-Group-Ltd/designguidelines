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
   **Internal tools use Inter as their typeface, not the Brand layer's Plus Jakarta Sans** — see
   Typography below; this is the standard for every internal tool, not a WMS-specific exception.
   WMS 2.0's current teal primary colour remains a documented legacy exception to the Brand layer's
   colour tokens, pending a dedicated re-scope — that part (colour only) is not a pattern to copy
   into new projects.

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

### Typography — Brand layer (customer-facing, e.g. the Portal)
- **Font**: Plus Jakarta Sans (fallback: system-ui) — the closest free web match to the Vanguard
  brand font Gilroy, which isn't web-licensed.
- **Headings**: 700 weight
- **Body**: 400 weight
- **Labels**: 600 weight, 12px (uppercase micro-labels: 700 weight, 11px, letter-spacing)
- Every monetary/counting figure uses `font-variant-numeric: tabular-nums`.

### Typography — Application layer (internal tools, e.g. WMS 2.0)
**Internal tools use Inter**, not Plus Jakarta Sans — load it as a variable font (weight range
100–900) so intermediate weights render precisely, not just the fixed Google Fonts buckets. Inter
reads visually heavier than Plus Jakarta Sans/Helvetica at an equal nominal weight (larger x-height,
more stroke contrast), so the weight scale is deliberately tuned down rather than reusing the Brand
layer's numbers verbatim:
- **Body / paragraph**: 400 (`font-normal`) — table cell values, descriptions, general text.
- **Subtle emphasis**: 450 (`font-medium`) — secondary labels, muted captions.
- **UI chrome**: 500 (`font-semibold`) — badges, nav bar (location/user), filter chips, form labels.
- **Headings / strong emphasis**: 600 (`font-bold`) — page titles, section headings, primary column
  values, location bar.
- **Rare / hero**: 700 (`font-extrabold`) — large KPI numbers only.
- **Buttons are an explicit exception at 400** (`font-normal`), even though they're interactive UI
  chrome that would otherwise sit at 500 — bold button text reads as visually "loud" in a
  high-frequency operational tool where the same button is clicked dozens of times a shift.
- Every monetary/counting figure still uses `font-variant-numeric: tabular-nums`.

## 🖨️ Printing

Click the "Print Guidelines" button in the bottom-right corner to print a clean version with table of contents (sidebar hidden).

## 📝 Version History

- **v7.0** - Internal tools now use **Inter** as their Application-layer typeface, not Plus Jakarta
  Sans — decided during a live WMS 2.0 design-conformance sweep, comparing Oracle Sans, Helvetica,
  Plus Jakarta Sans, and Inter directly in the running app. This overrides §7's prior framing (WMS's
  Oracle Sans as a "legacy exception... pending re-scope"): the typeface question for internal tools
  is now settled as Inter, for every internal tool, not just WMS. Added the internal-tool weight
  scale (400/450/500/600/700, deliberately tuned down from the Brand layer's numbers since Inter
  reads heavier than Plus Jakarta Sans/Helvetica at an equal nominal weight) and the explicit
  buttons-stay-at-400 exception. Removed the "Inter... rejected as not Gilroy-like enough" line —
  that was a Brand-layer (Portal) typeface-matching criterion and doesn't apply to the Application
  layer's internal-tool typeface question; leaving it in read as a blanket rejection of Inter, which
  is no longer accurate. WMS's teal *colour* remains the only actual legacy exception (§7).
- **v6.0** - Corrected the table-toolbar model against the actual shipped Portal source
  (`public/assets/app.js`, `styles.css`) and its own ADR
  (`docs/decisions/0005-transaction-tables-nav-and-branch-model.md`), not just its docs. v5.1–v5.2
  built an entire left/right "informational vs. consequential" toolbar theory, including a fabricated
  page-level "scope switch" concept for Branch — none of it matches the real app. What's actually
  shipped: **two separate rows**, not one split row — an optional page-level action (its own row,
  above the table, left-aligned, never paired with filters/search) and, inside the table, its own
  toolbar with filters rendering left and search growing to fill the remaining width to the right
  (no action buttons in that row at all). Branch is explicitly, per Louis's own ADR-0005, a plain
  per-table filter — "no context switching... branch becomes a filter, not a global mode" — never a
  page-wide scope control. Rewrote the toolbar rule, the Tables (§14) and Search & filters demos, and
  the page-hierarchy "Rules by Row" list to match. `AGENTS.md` corrected to match.
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
