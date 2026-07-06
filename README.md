# Vanguard UI Design Guidelines

A comprehensive design system and UI guidelines for Vanguard customer portals.

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
├── index.html      # Complete guidelines (self-contained)
├── README.md       # This file
└── .nojekyll       # Tells GitHub Pages not to process with Jekyll
```

## 🎨 Design Tokens Reference

Source of truth: the shipped `vanguard-portal-prototype` (`docs/design-system.md` +
`public/assets/styles.css`). If this repo and the prototype ever disagree, the prototype wins.

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
