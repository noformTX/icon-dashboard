# ICON Brand 2026 — Quickref

A compact reference for generating ICON-aligned letter documents, 16:9 slides, and live operational dashboards. Companion to `claude.md` (working notes).

---

## 1. Sub-brand (always confirm at chat start)

Sub-brand determines palette and default body surface. Typography, grid, composition, and spacing are identical across all three. Color carries audience-semantic meaning, not aesthetic preference — pick by **who the document is for**, not by what looks nice.

| Sub-brand          | Audience                                 | Neutral     | Accent       | Token prefix   | Body default |
|--------------------|------------------------------------------|-------------|--------------|----------------|--------------|
| Design + Build     | Commercial construction industry         | Neutral Gray | Orange (O50) | `--g*` `--o*`  | Light (G90)  |
| PRIME              | Military, Off-World, Government work     | Neutral Gray | Orange (O50) | `--g*` `--o*`  | Dark (G10)   |
| Technology / Titan | Tech industry, BuildOS, software         | Slate Blue  | Cyan (C50)   | `--s*` `--c*`  | Dark (S10)   |

**Pairing discipline:** one neutral per document; only its paired accent may appear with it. No mixing.

**D+B and PRIME share a palette but not a default surface.** D+B reads as commercial/civilian on a light surface; PRIME reads as govt/defense/space on a dark one. The palette pairing is identical because audience is construction-adjacent for both — the surface tier carries the register difference.

**Logo:** pure black on light, pure white on dark. Never tinted.

**ICON wordmark:** Full logotype, aspect ratio ~1.88:1. Pure black on light surfaces, pure white on dark. Never tinted.

**ICON Orbital:** Icon-only mark (orbital symbol — solid disc above concentric ring), aspect ratio ~0.667:1. Use where the wordmark would be redundant or space-constrained — dashboard chrome, app icons, social avatars. Same color rules as the wordmark.

Implementation for both: use `fill: currentColor` on the paths and set the parent's `color` to `#000` or `#fff` based on the surface.

**ICON wordmark:**

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 425.19">
  <g fill="currentColor">
    <path d="M399.92,112.07c31.31,0,56.11-24.63,56.2-55.82C456.21,25.49,431.28.03,401.05,0c-31.87-.03-57.01,24.6-57.08,55.91-.07,31.16,24.82,56.15,55.94,56.16Z"/>
    <path d="M403.31,141.36c-79.97-1.79-145.13,62.68-145.24,140.92-.11,79.63,62.79,142.9,141.87,142.9,78.85,0,141.86-63.08,142.07-141.83.2-76.84-61.68-140.27-138.7-141.99ZM400.05,341.68c-32.22,0-58.53-26.31-58.46-58.43.07-32.09,26.6-58.5,58.64-58.36,31.92.13,58.11,26.38,58.21,58.32.09,32.1-26.25,58.48-58.38,58.47Z"/>
    <path d="M783.96,226.21c-27.03-48.82-68.62-74.81-124.61-76.23-32.15-.81-64.35-.15-96.52-.15h-4.88v267.11h83.19v-183.74c5.29,0,10.13-.05,14.96.01,10.45.13,20.53,1.99,29.68,7.28,20.8,12.01,30.72,30.3,30.74,54.1.04,39.11,0,78.21,0,117.32v5.04h83.45v-5.17c0-39.94-.11-79.88.02-119.83.08-23.28-4.79-45.44-16.04-65.75Z"/>
    <path d="M183.9,284.49c-.72-27.59,20.47-58.55,58.07-60.31v-82.72c-38.56-1.41-92.58,18.51-122.91,71.03-28.18,48.81-24.56,111.01,9.98,156.01,28.35,36.94,66.31,55.33,113.1,56.63v-83.27c-37.81-2.11-57.56-31.66-58.24-57.37Z"/>
    <path d="M0,416.59h82.77V149.93H0v266.65Z"/>
  </g>
</svg>
```

**ICON Orbital:**

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 283.39 425.19">
  <g fill="currentColor">
    <circle cx="141.69" cy="56.68" r="56.68"/>
    <path d="M141.69,141.8C63.44,141.8,0,205.24,0,283.5s63.44,141.69,141.69,141.69,141.69-63.44,141.69-141.69-63.44-141.69-141.69-141.69ZM141.69,340.18c-31.3,0-56.68-25.38-56.68-56.68s25.38-56.68,56.68-56.68,56.68,25.38,56.68,56.68-25.38,56.68-56.68,56.68Z"/>
  </g>
</svg>
```

---

## 2. Body surface defaults

Each sub-brand has **one** default body surface. There is no mid tier and no opt-in surface alternates — the surface tier is fixed by sub-brand.

| Sub-brand          | Body surface | Token | Notes                                               |
|--------------------|--------------|-------|-----------------------------------------------------|
| Design + Build     | Light (G90)  | `--g90` | `#E6E6E6` — neutral light                         |
| PRIME              | Dark (G10)   | `--g10` | `#1A1A1A` — neutral dark, evokes deep space       |
| Technology / Titan | Dark (S10)   | `--s10` | Slate dark, distinct from G10 by hue              |

Within a body surface, panels can sit on either lighter or darker tiers (e.g. G80 panels on G90 body for D+B, G12-G15 panels on G10 body for PRIME). Panel choice is editorial — see §6.10 (live vs static register).

---

## 3. Token system

Each sub-brand exposes the same semantic tokens; only the underlying values differ.

### 3.1 Neutral palette — Gray (D+B, PRIME)

The shared D+B/PRIME gray ramp is **neutral** (no warmth). It mimics FormCrete (the structural/printing material) — flat gray with no temperature shift. All warmth in the brand comes from the orange accent; the neutrals are deliberately uninflected so the orange reads cleanly against any step.

Stepped by HSL lightness (%L), constant hue and chroma at zero:

| Token  | Hex      | %L   | Use                                            |
|--------|----------|------|------------------------------------------------|
| `--g10` | #1A1A1A | 10%  | PRIME body                                     |
| `--g20` | #333333 | 20%  | Heavy text on light, dark panel surface        |
| `--g30` | #4D4D4D | 30%  | Body text on light                             |
| `--g40` | #666666 | 40%  | Muted text                                     |
| `--g50` | #808080 | 50%  | Mid-gray, hairlines                            |
| `--g60` | #999999 | 60%  | Subtle text on dark                            |
| `--g70` | #B3B3B3 | 70%  | Faint text on dark, muted                      |
| `--g80` | #CCCCCC | 80%  | Panel surface on light, separator on dark      |
| `--g90` | #E6E6E6 | 90%  | D+B body                                       |

PRIME on G10 typically uses G12-G15 (`#1F1F1F`-`#262626`) for panel surfaces — half-step interpolations between G10 and G20. These are not pre-tokenized; declare locally as needed.

### 3.2 Accent — Orange (D+B, PRIME)

| Token   | Hex       | Use                                                          |
|---------|-----------|--------------------------------------------------------------|
| `--o50` | `#FF4F00` | Canonical brand orange — the only orange. Use for accents, status indicators, dividers, focal callouts. |

The canonical brand orange is **#FF4F00** (RGB 255, 79, 0). Do not substitute alternates like #E85A1F or other "brand-orange-feeling" hexes; the canonical value is exact.

### 3.3 Slate Blue palette — Tech/Titan

Stepped similarly by %L on a slate-blue hue. Token prefix `--s*`. S10 is the dark body for Tech sub-brand; S40-S60 cover hairlines and muted text.

### 3.4 Cyan accent — Tech/Titan

| Token   | Use                                       |
|---------|-------------------------------------------|
| `--c50` | Cyan accent — focal element, status pip   |

### 3.5 On-surface tokens (theme-aware)

```
--text          full strength body text
--text-muted    secondary text — labels, captions
--text-subtle   tertiary — backgrounds, watermarks
--rule-chrome   strong divider — header/footer separators
--rule-interior weak divider — table rows, list separators
--logo          black on light surfaces, white on dark
--accent        the sub-brand accent (orange or cyan)
```

Implement on-surface as opacity steps off the foreground color (white on dark, black on light) rather than dedicated hexes. Recommended steps:

- `--text`: 0.92 (dark) / 1.0 (light)
- `--text-muted`: 0.66 (dark) / 0.66 (light)
- `--text-subtle`: 0.34 (dark) / 0.34 (light) — see §6.11 for AA-mode adjustments
- `--rule-chrome`: 0.18-0.22 (both)
- `--rule-interior`: 0.08-0.12 (both)

---

## 4. Status palette

Three states. Used for status dots, status text, and any health/health-like indicator.

| State    | Live dark      | Live light       | Default mode    |
|----------|----------------|------------------|-----------------|
| On       | `#4ade80` (vivid green) | `#16a34a` (vivid green) | Same         |
| At risk  | `#facc15` (true yellow) | `#f59e0b` (vivid amber) | Same         |
| Off      | `#ef4444` (red) | `#ef4444` (red) | Same         |

Vivid status hues do not strictly clear AA on every panel surface — the yellow is ~2.2:1 on white panels, the red ~4.0:1. This is acceptable on **live** dashboard surfaces (instrument-panel register, scanned at distance). For static reports, prefer the §6.9 accent-at-opacity scale instead of vivid status colors. See §6.10.

When status text and dots co-exist, color them together via shared `--status-on/risk/off` tokens — never decouple them.

---

## 5. Spacing & grid

Standard spacing scale: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128px. Compose layouts on multiples of 8 unless tight type setting requires 4. Avoid 10/14/18/22 — they're invisible on inspection but compound into off-grid drift.

Page grids:
- Letter: 8 cols × 10 rows, 32px margin, 16px gutters, stretch, at 612×792 (1632×2112 @2x). Default Figma layout grid for all letter-format documents — overlay renders as FF0000 @ 10% (non-printing).
- Slides: 12-col, 24px gutters at 1920×1080.
- Dashboard: free-form panel grid at 1920×1080. The dashboard is a fixed 80px header / sliding viewport / 80px ticker stack; panels sit inside the viewport in CSS grid.

---

## 6. Typography

Three families:

| Role    | Family stack                                              |
|---------|-----------------------------------------------------------|
| Display | `'Lightspeed', 'DM Sans', 'Helvetica Neue', sans-serif`   |
| Body    | `'Helvetica Neue', 'Inter', sans-serif`                   |
| Mono    | `'Roboto Mono', 'Courier New', monospace`                 |

Lightspeed is the flagship custom display. DM Sans is the Google Fonts fallback that approximates Lightspeed's silhouette closely enough for production use when Lightspeed isn't available.

### 6.1 Scale (display)

| Tier          | Size      | Use                                              |
|---------------|-----------|--------------------------------------------------|
| Hero          | 256px     | Single dominant numeral (countdown, KPI hero)    |
| Title         | 64-88px   | Page title, section opener                       |
| Subtitle      | 36-48px   | Sub-title, big numbers in ticker                 |
| Lead          | 24-28px   | Lead paragraph, panel title                      |
| Body          | 16-18px   | Standard body                                    |
| Small         | 13-14px   | Caption, dense data                              |
| Mono label    | 10-13px   | Eyebrow, status label                            |

### 6.2 Editorial vs working register

Two registers carry different content goals:

- **Editorial:** narrative voice, long-form reading, generous spacing. Letters and slide intros are editorial.
- **Working:** dense information, tables, systems content. Project tracker, KPI table, OKRs are working.

The same typography scale serves both; what shifts is line-height, white space, and panel rhythm.

### 6.3 Display weights

Lightspeed weight defaults:

| Weight   | Use                                                 |
|----------|-----------------------------------------------------|
| Regular  | Body in display family, lead paragraphs             |
| SemiBold (600) | **Default for hero and large display.** Reads confident without shouting. |
| Heavy (800) | Use **only when explicitly requested** — reads as shouting at default sizes |
| Black (900) | Reserved — never use without explicit request      |

Old defaults that called for Heavy on display heros are deprecated. SemiBold is the new default; reach for Heavy only when a piece is meant to feel emphatic and the editorial direction calls for it.

### 6.4 Display tracking

**Display letter-spacing tightens as size grows.** This is the conventional typographic rule — bigger sizes need negative tracking; smaller sizes can sit at zero or slightly positive. Reference scale:

| Size       | letter-spacing |
|------------|----------------|
| 256px      | -0.02em        |
| 64-88px    | -0.01em to 0   |
| 36-48px    | 0              |
| 24px       | -0.01em or 0   |

Interpolate for sizes in between. The old fallback-tuned scale that had positive tracking on Hero is deprecated.

### 6.5 Body type

Helvetica Neue (or Inter as fallback). Standard weights 400/500/600/700. Body type uses default tracking (0); never apply letter-spacing to body type.

### 6.6 Mono usage

Mono is for: data values, labels, eyebrows, timestamps, IDs, status text, anything that benefits from monospace alignment or "system telemetry" register.

**Mono is always uppercase.** Apply `text-transform: uppercase` on every mono usage. Lowercase mono is reserved for code blocks (which the brand md doesn't address) — in branded surfaces, mono is uppercase.

### 6.7 Mono weight (irradiation effect)

Mono weight depends on surface:

- **Mono on dark:** weight 400 (Regular)
- **Mono on light:** weight 500 (Medium)

This compensates for the optical "irradiation" effect — light-on-dark glyphs visually thicken, dark-on-light glyphs visually thin. Adjusting weight to match keeps mono looking the same actual width across both modes.

### 6.8 Hairline tier system

Hairlines are the connective tissue of the design system. They have three distinct roles, each with a different opacity/weight:

| Tier    | Opacity range  | Use                                              |
|---------|----------------|--------------------------------------------------|
| Chrome  | 0.18-0.22      | Strong dividers — header bottom, footer top, panel separators |
| Interior| 0.08-0.12      | Weak dividers — table rows, list separators, sub-section dividers |
| Heading | 0.10-0.15      | Section heading underlines — between chrome and interior |

Don't mix tiers within one viewing context (e.g. don't use Chrome-strength rules between table rows; that's Interior territory).

### 6.9 Status text at density (live dashboards)

When a live surface needs status indicators in tight rows (table rows, list items, dense dashboards), prefer **mono uppercase colored text** over chip pills. The pattern uses brand accent at three opacity steps:

| State    | Opacity (live, dark) | Opacity (live, light)  |
|----------|----------------------|------------------------|
| On track | 1.0 (full --accent)  | 1.0 (full --accent)    |
| At risk  | ~0.55                | ~0.55                  |
| Off      | ~0.28                | ~0.28                  |

Same logic applies to all sub-brands: orange-on-gray for D+B/PRIME, cyan-on-slate for Tech. Live surfaces can use slightly higher floors for the lower steps; static surfaces can recede further (drop "Off" to 0.20 if the floor reads too prominent).

Chips still apply on **less-dense** surfaces (cards, full-width banners, single-row callouts) where the chip's enclosed shape carries semantic weight.

The dashboard implementation diverges from this default by using **vivid status colors** (green/amber/red) directly. This is a deliberate live-register exception — the radar/instrument-panel context expects color-coded alerts. Both patterns are valid; pick by surface register.

### 6.10 Live vs static register

A second axis orthogonal to §6.2 (editorial vs working). **Register reflects viewing context, not content type.**

- **Live:** updating surfaces scanned at distance and speed. Dashboards, instrument panels, status monitors. Tolerates more chrome, denser hairlines, motion (pulses, cascades, transitions). Vivid status colors permitted.
- **Static:** read deliberately at close range. Reports, slides, printed letters. Demands restraint — chrome must justify itself; motion is absent; status uses the §6.9 opacity ramp.

A KPI table can be live (on a TV dashboard) or static (in a printed quarterly report). Same vocabulary, calibrated for viewing context.

### 6.11 AA mode (accessibility re-routing)

When a piece needs to clear WCAG AA contrast (4.5:1 for body text, 3:1 for large text), three principles override the default sub-brand discipline:

1. **D+B-light routes to PRIME (G10 body).** Orange #FF4F00 fails AA on any surface lighter than ~#212121. Switching to G10 body satisfies contrast without losing the brand register.
2. **Cyan-on-slate keeps §6.9 accent-at-opacity** (it clears AA on S10 body). Orange contexts cannot sustain the at-opacity ramp at AA — replace with neutral-fade: on=accent, risk=body text, off=text-subtle.
3. **Text-subtle floors lift.** From 0.34 to 0.50 on dark, from 0.34 to 0.55 on light. PRIME panels need ~G12 (`#1F1F1F`) instead of G10 to give orange enough contrast headroom.

Apply AA mode when explicitly required (deliverable for accessibility audit, public-facing site, regulated industry comm). Default sub-brand discipline is **not** AA-compliant by default; the accent palette and surface pairings are tuned for editorial impact, not accessibility minimums.

### 6.12 Mono tracking cap

**Mono letter-spacing is capped at 0.04em (4%).** Never exceed this regardless of size. Mono stays tight (0 to 0.04em). The old "0.14-0.20em uppercase mono for legibility" pattern is deprecated — modern mono fonts (Roboto Mono, DM Mono) have enough internal spacing that they don't need wide tracking, and tight tracking reads more contemporary.

---

## 7. Composition patterns

### 7.1 Panels

Panels are rectangles with internal padding (typically 24px) sitting on the body surface. Panel surface is one step lighter or darker than body:

- D+B (G90 body): panel = white (`#FFFFFF`) for clean elevation, or G80 for panel-on-body
- PRIME (G10 body): panel = G12-G15 (`#1F1F1F`-`#262626`)
- Tech (S10 body): panel = S12-S15

Avoid borders on panels; rely on surface contrast. If a border is needed (e.g. for an outlined card variant), use `--rule-chrome` opacity, not the accent.

### 7.2 Dividers

Use `<hr>` or border-bottom. Color from the hairline tier system (§6.8). Never use the accent for dividers — accent is for focal elements only.

### 7.3 Status indicators

Default: filled circle (status dot) + mono uppercase text (status label), color-matched. Both color tokens reference the same semantic state.

Dot size: 8px diameter for default density, 6px for tight rows, 10px for prominent rows.

### 7.4 Callouts

Reserve callouts for genuine focal moments — one or two per page, not per row. A callout is a slightly elevated panel (typically with an accent stripe on the leading edge or a panel-on-panel surface bump) with leading hierarchy emphasis.

### 7.5 Self-review (default process)

After composing, stand back and check:
- One focal element per page? If two compete, demote one.
- Consistent hairline tier within each viewing context?
- Mono is always uppercase?
- Status colors paired (dot + text reference same token)?
- Sub-brand discipline maintained (no orange in Tech, no cyan in PRIME)?

Mitchell handles visual review himself for dashboard work; this checklist applies primarily to slides and letters where review-and-iterate is harder once delivered.

---

## 8. Vocabulary & nomenclature

- **FormCrete** — the canonical name for the structural/printing material. Always use this name. Legacy names "CarbonX" and "Lavacrete" are deprecated and should be replaced wherever encountered (slides, decks, reports, dashboards, OKR copy, KPI descriptors, marketing). Update source documents rather than quote legacy names verbatim.
- **Vulcan** — the second-generation printer. (Successor to original printer line; specific terminology subject to product team.)
- **Titan** — the printer line under the Tech/Titan sub-brand.
- **D+B** — internal shorthand for Design + Build.
- **PRIME** — Off-World, military, government work sub-brand.
- **Orbital** — the icon-only logo mark.
- **Wordmark** — the full ICON logotype.

---

## 9. Don't

- Don't mix sub-brand palettes within a single document.
- Don't use the accent for dividers or hairlines — accent is for focal elements only.
- Don't use lowercase mono on branded surfaces — mono is uppercase.
- Don't apply tracking to body type — body uses default 0 spacing.
- Don't exceed 0.04em mono tracking.
- Don't use positive tracking on display sizes ≥ 64px — they want negative.
- Don't use Heavy or Black display weight without explicit direction.
- Don't substitute alternate orange hexes — the canonical orange is #FF4F00, exactly.
- Don't refer to FormCrete as CarbonX or Lavacrete; replace those names wherever encountered.

---

## 10. Last updated

This brand md captures decisions through May 2026 dashboard work. Major updates this cycle:

- Canonical orange corrected to **#FF4F00** (was incorrectly #E85A1F in some prior versions).
- Display tracking rule corrected: **tightens as size grows** (was inverted in earlier versions).
- Mono tracking cap: **0.04em max**. The old 0.14-0.20em uppercase-mono pattern is deprecated.
- Display weight default: **SemiBold** for hero (was Heavy).
- Material naming: **FormCrete** replaces CarbonX/Lavacrete.
- Gray palette: **neutral** (no warmth), stepped by HSL %L — G10 through G90.
- Live vs static register added as an orthogonal axis to editorial vs working.
- AA mode discipline added (§6.11).
- Status-at-density opacity scale added (§6.9).
- Hairline tier system formalized (§6.8).

Updates should be reflected in `claude.md` working notes and userMemories, in addition to this file.
