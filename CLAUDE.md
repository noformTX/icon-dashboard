# claude.md — ICON dashboard working notes

How I approach the ICON live operations dashboard for Mitchell. Companion to `icon-brand.md`. Focused on the dashboard build specifically — `icon-dashboard.html` — distinct from slide and letter work which has its own conventions.

## Working style

Mitchell developed the brand template with me over hundreds of iterations and trusts the call on design judgment. That shapes how I work:

- **Commit to one recommendation.** Don't enumerate options to defer the decision. He'll redirect if he wants something different.
- **Prefer the bigger structural move.** Restructure the layout, swap an algorithm, or change a paradigm — *before* reaching for padding/margin/font-size tweaks. Stacking small fixes makes things noisy; the right answer is usually one larger change.
- **No pre-hedging.** State the call. Caveats only when there's genuine uncertainty.
- **Source-of-truth precedence.** Uploaded reference files (PDFs, screenshots, Drive docs) override stale brand md content. When you spot a mismatch, queue the brand md correction explicitly — don't silently use the new info while letting the old md text stand.
- **Memory hygiene.** When brand decisions change (canonical color shifts, typography rules update, etc.), update userMemories immediately. The next session won't have this conversation.

## Output infrastructure

The dashboard is a single 1920×1080 HTML file designed to display fullscreen on a TV. It scales to any viewport via JavaScript `transform: scale()` — never CSS `zoom`, which silently rejects length values and produces broken layouts. The scaling is computed at runtime from `window.innerWidth / 1920` and re-applied on resize.

When iterating, ship the `.html` directly via `present_files`. Mitchell opens it in his browser at full fidelity. No PNG export needed unless requested.

The file is large (~1MB+) due to embedded base64 images for the slideshow. Performance is fine on modern hardware; just be aware that view operations on the file are slow due to size.

## Architecture

The dashboard layout is the canonical free-form panel grid from brand md §5: 1920×1080, 80px fixed header, sliding viewport, 80px fixed ticker. Internal structure below applies to *this* dashboard build.

**Two-page slide system.** Header (80px, fixed) + pages-viewport (sliding) + ticker (80px, fixed). Pages slide horizontally via CSS transform with a 900ms cubic-bezier transition.

**Page 1** is a 3-column grid of business intel: countdown panel (left, hero), OKR scroller (top right), KPI table (bottom left), upcoming events (bottom middle), field imagery slideshow (bottom right).

**Page 2** is a 60/40 split: project tracker (60%) and globe with print network (40%).

**Auto-cycle.** OKRs rotate 5 entries × 15s on Page 1 → slide to Page 2 → hold for 2 full globe rotations (~96s) → return to Page 1. Manual page-toggle button in header chrome interrupts auto-cycle.

**Theme cycle.** Light (D+B) and dark (PRIME) modes auto-switch at 12 noon and 12 midnight via `getExpectedMode()`. Manual toggle uses View Transitions API for a circular reveal animation; falls back to instant on unsupported browsers.

## Brand-md companion notes

`icon-brand.md` is the primary reference for sub-brand discipline, palette tokens, typography rules, and component patterns. Things specific to dashboard work that aren't in the brand md:

- **Live register applies.** The dashboard is a live surface (§6.10 of brand md) — updating, scanned at distance, instrument-panel ambitions. This relaxes some chrome-density rules and permits motion patterns (radar bloop, cascade animations, pulse halos).
- **Status text and dots travel together.** Both color-driven by `--status-on/risk/off` tokens. Don't decouple them. (Reinforces brand md §4 — applies brand-wide; called out here because dashboard density makes it especially tempting to violate.)
- **Mono numeric cells stay tabular at heart even when the loaded font isn't strictly monospace.** Roboto Mono is the canonical choice; switching to a non-monospace font for experimentation breaks column alignment.
- **Animation timing is deliberate.** Cascade fills run ~3 seconds, leading-edge dots appear at ~1s after their line completes, radar pulses every 2s. The whole rhythm is tuned to feel "alive but not anxious."

## Decision defaults

When the brand md doesn't fully prescribe an answer:

- **For layout misalignment between header and body grids:** draw one element that spans both, computed once. Per-row gradients sub-pixel-drift from grid columns; an overlay at the parent level shares the parent's exact pixel calculation.
- **For animation language unification:** if two panels both have "pulsing" elements, make them use the same pulse pattern (same easing, same duration, same color treatment). The radar bloop on the globe and the leading-edge dots on the project tracker share the exact same animation — that's what makes Page 2 feel like one panel rather than two adjacent ones.
- **For font fallback chains:** primary font, then 1-2 system fallbacks. Don't list 5+ — it bloats the chain without practical benefit.
- **For feature-experimental requests** (like temporary font swaps): make the change cleanly, note what will visibly shift, and remember to revert if asked.

## Dashboard-specific gotchas

- The ICON wordmark and Orbital are both available. Wordmark = full logotype, ~1.88:1 ratio. Orbital = icon-only, ~0.667:1 ratio. Either can sit in the dashboard chrome via the `#wordmark` element. Both use `fill: currentColor` driven by `--logo` token.
- The KPI table uses `table-layout: fixed` with explicit colgroup widths. When data overflows or truncates, rebalance column widths; don't rely on `auto`.
- The globe IIFE has a hardcoded SITES array of `[lat, lng, label]` tuples. Adding/removing sites requires updates to both SITES and `LOCATION_COLORS` (if location colors are in use).
- Date string parsing is timezone-fragile. Use `new Date(year, monthIndex, day)` with explicit numeric args, never `new Date('Month DD, YYYY')` strings — the latter parses as UTC in some browsers and slips a day in non-UTC timezones.

## What `icon-brand.md` already covers (don't re-explain)

§1 sub-brand discipline, palettes, logo+orbital paths.
§2 surface defaults per sub-brand.
§3 token system — surfaces, accent, status, on-surface, hairlines.
§4 status palette + dot/text co-color rule.
§5 page grids — canonical Letter / Slides / Web (3-tier responsive: desktop 768+, tablet 480–767, mobile <480) / Dashboard defaults. Apply automatically when generating a new document of the corresponding type.
§6 typography — scale, weights, tracking rules, mono cap.
§6.3 — Lightspeed display weight defaults: mixed-case = SemiBold, uppercase = Bold; accent-colored display steps up one weight (mixed-in-accent → Bold). Stat-row figures override and are always Bold per §7.6.
§6.5 — body default weight is Medium (500), not Regular.
§6.6 — mono is always uppercase; mono is the system-telemetry register (data values, labels, eyebrows, timestamps, IDs, status text).
§6.7 — mono weight on light surfaces is Medium; mono on dark is Regular (irradiation rule).
§6.8 — hairline tier system.
§6.9 — status-at-density opacity scale.
§6.10 — live vs static register.
§6.11 — AA mode discipline.
§6.12 — mono tracking cap (0.04em max).
§6.13 — data table typography: body face for narrative content, mono for categorical/identifier/timestamp; 10pt body cell content at line-height 1.2; no top rule on `<thead>`; units belong in label cell, not value cell; accent NOT used in data tables.
§7.5 — chrome economy (every chrome element earns its presence).
§7.6 — stat-row: figures are single text element, all Bold (700), unit suffix inline at same size/weight; reduce size before tracking when overflowing.
§10 — charts, diagrams & technical illustration. Explicitly applies to live dashboards. §10.1 general principles (minimal chrome, horizontal-only gridlines, single focal accent, mono-caps labels, source attribution required); §10.2 line charts with plan/actual; §10.3 bar/column; §10.4 combo/dual-axis; §10.5 inline callouts and event markers.

When in doubt, read the brand md before improvising. When the brand md is wrong, fix it (and update userMemories).
