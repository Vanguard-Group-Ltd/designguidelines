# AGENTS.md — Vanguard Design System, machine-readable

This file is for AI build agents (Claude Code or otherwise) scaffolding or refactoring a Vanguard
digital product. It states the same rules as `index.html` as flat facts, no prose to interpret. If
this file and `index.html` ever disagree, `index.html` is the source of rationale — regenerate this
file from it, do not hand-edit around a conflict.

Full narrative version with rationale: `index.html`. Brand source of truth:
`vanguard-portal-prototype/docs/design-system.md`.

## 0. Decision tree — run this first

```
1. Is this screen customer-facing (a customer signs in / buys / views their own data)?
     YES → Application = customer-facing. Density = comfortable. §5.
     NO  → Application = internal-tool. Density = compact. §6.
2. Every rule in §1 (Method) applies regardless of the answer above.
3. Every token in §2 (Brand) applies regardless of the answer above,
   EXCEPT: WMS 2.0 currently overrides primary colour + typeface — §7 (do not copy this override
   into a NEW project; it is a legacy exception, not a pattern).
```

## 1. Method — mandatory, every project, no exceptions

- Status is computed via one mapping function → one shared badge component. Never hand-write a
  status label next to hand-picked colours. New status = one line in the map.
- Every data table has both column-level filter AND column-level search. Never global-search-only.
- Global search / command palette is the primary navigation method, not deep nav trees.
- Zero hardcoded colour/spacing/radius values in component code — every value is a token reference.
- Exactly one semantic status set: success / warning / danger / info / neutral. Each is a
  `{background, border, text}` triple, always used together. Status is never colour-alone: always
  pill shape + colour + text label (WCAG SC 1.4.1).
- Radius has exactly three roles, never a fourth arbitrary value: `interactive` (buttons/inputs/
  chips) = 3px, `structural` (cards/tables/panels) = 5px, `overlay` (modals/dropdowns/popovers) =
  6px. Fully-round elements (avatars, radio dots, pill badges) use 50%/9999px, not a role token.
- Every interactive element implements five states: default, hover, active/pressed, disabled, and a
  visible keyboard focus ring. Never `outline:none` without a replacement.
- One icon system only: Lucide. No emoji as icons. No bespoke one-off inline SVGs.
- WCAG 2.2 AA minimum: 4.5:1 text contrast, visible focus indicators, keyboard-operable everything.
- Every UI pattern (a "selectable option card," a "status pill," a "data table toolbar") exists
  exactly once in the codebase. Before building a new one, search for an existing implementation.
- Voice: informational, never salesy. State a fact + offer a neutral action. No manufactured
  urgency, no exclamation-driven CTAs.
- Motion: 100–300ms, `ease`/`ease-out`. Animate only `transform`/`opacity`/`background`/
  `border-color`/`box-shadow`. Always add a `prefers-reduced-motion` guard.
- Every monetary or counting figure uses `font-variant-numeric: tabular-nums`.

## 2. Brand tokens — Portal-authoritative, apply everywhere unless §7 overrides

```css
--color-brand-blue: #004674;      /* primary — buttons, active nav, focus rings, headers */
--color-brand-red:  #ED2124;      /* LOGO ONLY. Never in UI — not error, not accent, not CTA. */
--color-primary: var(--color-brand-blue);
--color-primary-hover: #003A60;
--color-primary-active: #002F4D;
--color-primary-light: #EBF3FA;
--color-secondary: #6FBED9;       /* sky teal — secondary CTAs, accents, links, hover/focus borders */
--color-secondary-dark: #1F6F8F;  /* text/border variant, used on white, not as a fill */
--color-secondary-light: #EAF6FB;
--color-neutral-900: #0F172A;  --color-neutral-800: #1E293B;  --color-neutral-700: #334155;
--color-neutral-600: #475569;  --color-neutral-500: #64748B;  --color-neutral-400: #94A3B8;
--color-neutral-300: #CBD5E1;  --color-neutral-200: #E2E8F0;  --color-neutral-100: #F1F5F9;
--color-neutral-50:  #F8FAFC;  --color-white: #FFFFFF;
--color-success: #15803D;  --color-success-light: #F0FDF4;  --color-success-border: #BBF7D0;
--color-warning: #B45309;  --color-warning-light: #FFFBEB;  --color-warning-border: #FDE68A;
--color-danger:  #DC2626;  --color-danger-light:  #FEF2F2;  --color-danger-border:  #FECACA;
--color-info:    #1D4ED8;  --color-info-light:    #EFF6FF;  --color-info-border:    #BFDBFE;

--radius-interactive: 3px;  --radius-structural: 5px;  --radius-overlay: 6px;  --radius-full: 9999px;

--space-0: 4px;  --space-1: 8px;  --space-2: 12px;  --space-3: 16px;
--space-4: 20px; --space-5: 24px; --space-6: 32px;  --space-7: 40px; --space-8: 48px;

--font-family: "Plus Jakarta Sans", system-ui, -apple-system, sans-serif;
/* Headings: 700. Body: 400. Labels: 600, 12px. Uppercase micro-labels: 700, 11px, letter-spacing .04–.06em. */

--elevation-1: 0 1px 3px rgba(0,0,0,.04);
--elevation-2: 0 4px 6px rgba(0,0,0,.07);
--elevation-3: 0 8px 28px rgba(15,23,42,.16);
--shadow-lift: 0 10px 24px rgba(31,111,143,.18);
```

Buttons — exactly four kinds, one `btn-primary` per screen:
```css
.btn-primary   { background: var(--color-brand-blue); color: #fff; }
.btn-secondary { background: #fff; color: var(--color-secondary-dark); border: 1px solid var(--color-secondary); }
.btn-ghost     { background: #fff; color: var(--color-neutral-600); border: 1px solid var(--color-neutral-200); }
.btn-danger    { background: #fff; color: var(--color-danger); border: 1px solid var(--color-danger-border); }
```
`.btn-primary.btn-block` (full-width primary CTA, **customer-facing only**) gets a trailing `»` via
`::after`. Suppressed on `.btn-primary.btn-block.btn-send` and never applied to small in-card or
modal-confirm buttons.

## 3. Component → class lookup (build from these, don't invent new ones)

| Need | Use |
|---|---|
| Status indicator | `.badge.{ok,info,warn,neu,err}` — pill, `{bg,border,text}` triple, icon+label |
| Selectable option (radio-style) card | `.co-method-card` (2-col grid) or `.payopt` (compact list) |
| Data table | `.tbl` + `.tbl-toolbar` (search left, filter chips + branch select right) |
| Table column filter | `.th-flt` (funnel icon) → `.colflt-pop` (body-mounted popover) |
| Modal | `.modal-backdrop` → `.modal` → `.mtop`/`.mbody`/`.mfoot`, auto-injected close (`.modal-x`) |
| Slide-out panel | `.qbackdrop`/`.qpanel`, fixed right, `translateX` transform |
| Toast | `#toast-host` → `.toast` (`.err` variant), success auto-dismiss ~2.6s, error ~4.2s |
| Empty state | `.empty` — dashed border, icon + heading + body + CTA |
| Form field | `label` + `.field`, focus = `border-color: var(--color-primary)` + 3px navy-tinted ring |
| Searchable dropdown | `.combo`/`.combo-input`/`.combo-pop`/`.combo-opt`; plain `<select>` if ≤5 options |

## 4. Method rules with no shortcut

- Do not add a fourth radius value "just this once."
- Do not render a status with a hardcoded colour — go through the shared badge/mapping.
- Do not ship a table without column filter + search.
- Do not use `--color-brand-red` for anything except the literal logo mark.

## 5. Application: customer-facing

- Density: comfortable (default). Table padding ~12px. Touch targets 36–44px.
- Voice: informational, never salesy (§1).
- `.btn-primary.btn-block::after` flourish applies.

## 6. Application: internal tool

- Density: compact **by default**, not a secondary mode. Table padding 6–8px. Touch targets 28–32px.
- Column filter + search is a required table capability (§1), not optional.
- Operational data-viz: fill level and weight capacity map onto the semantic success/warning/danger
  ramp (§2) — never a bespoke hue. Zone type and shelf type use dedicated tokens on the neutral ramp,
  documented once, reused across every view (plan/floor/elevation).
- No brand CTA flourish (§2) on internal-tool buttons.

## 7. Known legacy exception — do not replicate

WMS 2.0 currently uses its own established primary colour (teal, `hsl(192 65% 29%)`) and typeface
(Oracle Sans stack) instead of §2's brand tokens, under a signed-off decision to preserve its existing
UX rather than reskin mid-flight. This is tracked as a pending brand re-scope, not a second valid
brand. **A new internal-tool project uses §2's Brand tokens, not WMS's current teal/Oracle Sans.**
