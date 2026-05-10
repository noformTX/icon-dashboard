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

Each sub-brand has **one** default body surface for screen and digital deliverables (web, dashboards, slides viewed on a display). There is no mid tier and no opt-in surface alternates — the screen surface tier is fixed by sub-brand.

| Sub-brand          | Screen body  | Token | Notes                                               |
|--------------------|--------------|-------|-----------------------------------------------------|
| Design + Build     | Light (G90)  | `--g90` | `#E6E6E6` — neutral light                         |
| PRIME              | Dark (G10)   | `--g10` | `#1A1A1A` — neutral dark, evokes deep space       |
| Technology / Titan | Dark (S10)   | `--s10` | Slate dark, distinct from G10 by hue              |

**For deliverables created to be printed, default to white body (`#FFFFFF`)** regardless of sub-brand, unless another surface color is explicitly requested. The screen surfaces above are tuned for backlit display: G90 reads muddy on paper, and the dark surfaces (G10, S10) waste toner without a clear editorial reason. Sub-brand identity carries through the accent and the type — only the body changes from screen-light/screen-dark to paper-white.

Print is the default for physical formats — letter, tabloid, A4/A3 — and anything where a printed copy is the intended primary form. The screen body is the default for dashboards, web pages, in-product surfaces, and slides shown live.

**PDF export does not auto-trigger print body.** A PDF is a delivery format, not a deliverable type — it inherits the source surface of whatever is being exported. A dashboard exported to PDF stays on its dark screen body; a slide deck exported to PDF stays on its sub-brand screen body; a letter exported to PDF was already on print body because it's a letter, not because it's a PDF. The only thing that flips a PDF to print body is the deliverable being explicitly destined for print (the user says it's getting printed, or it's a physical format per the list above). When unclear, ask.

PRIME or Tech can still print on their dark surface when the editorial direction calls for it — e.g. a PRIME pitch printed for stakeholders who expect the dark register, or a launch announcement where the dark surface is the visual signature. That's an opt-in override per deliverable, not the default. Ask "is this getting printed?" before specifying a body surface.

Within a body surface, panels can sit on either lighter or darker tiers — see §7.1 for the per-sub-brand and per-mode (screen vs print) panel rules.

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
| `--o50` | `#FF4F00` | Canonical brand orange — the only orange. Reserved for focal elements (see canonical uses below). |

The canonical brand orange is **#FF4F00** (RGB 255, 79, 0). Do not substitute alternates like #E85A1F or other "brand-orange-feeling" hexes; the canonical value is exact.

**Canonical accent uses** (use the accent for these; nothing else):

- Megafig — single hero figure or two-tone substring of one (§7.7).
- Single-word or single-clause color highlight in a display title — e.g. `**Installations** are weapon systems` (focal word) or `Installations are **weapon systems.**` (focal clause). Both treatments are in the vocabulary; pick by which fragment is the actual headline.
- Pull-quote curly quotes (§7.9) — the punctuation, not the body text.
- Aside-card / callout leading edge (§7.8) — 2pt left border.
- Current-period column highlight in financial tables (§7.12).
- Status dot for "on track / achieved" on editorial surfaces (§4).
- One focal cell per stat-row, when one stat is the headline (§7.6).
- Cover-page focal element — vanishing point, plumb line, accent dot.

**What accent is not for:** dividers, hairlines, body text, large fields of color, or two-plus competing focal elements on the same page. One focal moment per page.

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

**Editorial-only-positive alternative.** On static editorial surfaces (letters, slides) where every status item is "on track / achieved / launched" and contrast between states is not the actual signal, the green/amber/red palette can read as alarmist or instrument-panel. Substitute a **single accent dot + mono-caps text** for the achieved state — e.g. an objectives summary page with three cards each closing with `● TRACKING AHEAD`, `● LAUNCHED`, `● ESTABLISHED` in pure accent. This collapses the §4 palette to one color when only the positive state is shown, keeping the page single-accent and reserving the vivid §4 hues for surfaces where state contrast is meaningful (live dashboards, multi-state status tables).

---

## 5. Spacing & grid

Standard spacing scale: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128px. Compose layouts on multiples of 8 unless tight type setting requires 4. Avoid 10/14/18/22 — they're invisible on inspection but compound into off-grid drift.

**Page grids — canonical defaults.** Apply these whenever starting a new document of the listed type (letter, slide deck, website) unless the user explicitly specifies otherwise. All overlays use Figma's `Stretch` type and render as `FF0000` at 10% opacity (non-printing).

- **Letter** (612×792, 1632×2112 @2x): 8 cols × 10 rows, 32px margin, 16px gutters.
- **Slides** (1920×1080): 8 cols × 6 rows, 80px margin, 32px gutters.
- **Web** (responsive, columns only — no rows). Three breakpoints, applied per viewport width:
  - Desktop (≥768px): 8 cols, 80px margin, 32px gutters.
  - Tablet (480–767px): 6 cols, 48px margin, 24px gutters.
  - Mobile (<480px): 4 cols, 24px margin, 16px gutters.
- **Dashboard** (1920×1080): free-form panel grid. The dashboard is a fixed 80px header / sliding viewport / 80px ticker stack; panels sit inside the viewport in CSS grid.

---

## 6. Typography

Three families:

| Role    | Family stack                                              |
|---------|-----------------------------------------------------------|
| Display | `'Lightspeed', 'Wix Madefor Display', sans-serif`         |
| Body    | `'Helvetica Neue', 'Inter', sans-serif`                   |
| Mono    | `'Roboto Mono', 'Courier New', monospace`                 |

Lightspeed is the flagship custom display. **Wix Madefor Display is the production fallback** when Lightspeed isn't available — open-source SIL OFL, with letter shapes that read close enough to Lightspeed's silhouette to preserve brand character. Earlier guidance specified DM Sans (geometric/rounded silhouette drifted brand character) and then Helvetica Neue (workhorse but visually too neutral to carry Lightspeed's display register) as the fallback; both are deprecated for the display stack. Do **not** load DM Sans or set Helvetica Neue as the display fallback. (Helvetica Neue remains the body face — see §6.5.)

Canonical font files live in Drive — see §11.6. Install Lightspeed locally before producing any ICON deliverable; the display stack only resolves correctly when Lightspeed is on the rendering machine.

**Tables use Helvetica Neue + Roboto Mono only.** Lightspeed (display) is reserved for display-tier focal moments outside table contexts — hero copy (§7.13, §7.14), stat-row figures (§7.6), megafigs (§7.7). Inside table cells — registries, income statements (§7.12), financial tables, multi-row data tables — body cells use Helvetica Neue and label/identifier/date columns use Roboto Mono. The intent: tables read as data, not display. A table value at Lightspeed pulls editorial weight that the data doesn't warrant.

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
| Medium (500) | Default for sub-titles, panel titles, section captions, smaller display |
| SemiBold (600) | **Default for mixed-case hero and large display.** Reads confident without shouting. |
| Bold (700) | **Default for uppercase titles, headings, and ALL-CAPS display.** Uppercase glyphs lack the ascender/descender rhythm of mixed case, so they need an extra step of weight to read with the same presence. Step up from SemiBold whenever a display title is set in uppercase. |
| Heavy (800) | Use **only when explicitly requested** — reads as shouting at default sizes |
| Black (900) | Reserved — never use without explicit request      |

The pairing is the rule: **mixed-case display = SemiBold; uppercase display = Bold.** Old defaults that called for Heavy on display heros are deprecated. Reach for Heavy only when a piece is meant to feel emphatic and the editorial direction calls for it. **One override:** stat-row figures are always Bold regardless of case — see §7.6 for the rationale.

**Accent-colored display text steps up one weight.** Bright accent colors (orange `#FF4F00`, cyan `--c50`) visually weigh less than black at the same weight, so an accent figure at SemiBold reads thinner than its black counterparts on the same page. Bumping up equalizes the visual mass. Practical effect:

- Mixed-case display in accent → Bold (was SemiBold)
- Uppercase display in accent → stays at Bold (don't double-bump to Heavy without explicit direction)

Applies to stat figures in accent (§7.6), megafigs (§7.7), display-title color highlights (§3.2), and any display-tier text set in `--accent`. Does **not** apply to mono labels in accent (e.g., aside-card eyebrows §7.8) — mono follows §6.7 weight rules. Does not apply to the punctuation glyphs of pull-quote curly quotes (§7.9), since they're decorative and don't compete with body text on a weight basis.

### 6.4 Display tracking

**Display letter-spacing tightens as size grows.** This is the conventional typographic rule — bigger sizes need negative tracking; smaller sizes can sit at zero. Display sans at hero sizes always wants noticeable negative tracking; the previous scale was too conservative and made hero/title type read airy. Reference scale:

| Size       | letter-spacing |
|------------|----------------|
| 256px+     | -0.04em to -0.05em |
| 96-128px   | -0.035em to -0.04em |
| 64-88px    | -0.03em to -0.04em |
| 48-56px    | -0.025em to -0.035em |
| 36-44px    | -0.02em to -0.025em |
| 24-32px    | -0.015em to -0.02em |
| 18-21px    | -0.005em to -0.01em |
| ≤16px      | 0              |

Interpolate for sizes in between. Earlier versions of this scale capped negative tracking at -0.02em on Hero and -0.01em on Title — both too loose. The values above produce display type that reads tight and confident at scale, which is the brand register.

### 6.5 Body type

Helvetica Neue (or Inter as fallback). **Default weight is Medium (500)** — pairs better with the SemiBold display register and gives body type the presence ICON's editorial register expects. Drop to Regular (400) only when explicitly de-emphasizing (footnotes, disclaimers, captions where Medium would compete with surrounding text). Use SemiBold (600) for inline emphasis (`<strong>`); reserve Bold (700) for cases that need a third weight step. Body type uses default tracking (0); never apply letter-spacing to body type.

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

**Hairline grid as a deliberate field.** When hairlines compose into a full grid mesh used as a design element rather than a divider (cover/hero compositions, architectural backgrounds — see §7.13 and §10.7), they sit at **chrome tier** (0.18–0.22), not interior. The default reading of "hairline" is "weak divider", but a chrome-tier hairline mesh covering a whole panel reads as deliberate architecture, not faint bleed-through — the higher opacity is required to register as a field and not as a divider artifact.

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

### 6.13 Data table typography

Tables use **Helvetica Neue (body)** and **Roboto Mono (mono)** only — Lightspeed is banned in tables (§6, §9). The face split:

- **Body face** for narrative cell content — names, addresses, descriptions, summary values. Anything where the content is read as text or as a numeric quantity that summarizes data (totals, sums).
- **Mono face** for categorical, identifier, timestamp, or status content — medallion numbers (`#000205`), dates (`12.22.25`), status labels (`TOWNHOUSE`, `BUNGALOW`), column headers, sequential indices. Mono content is uppercase per §6.6.

Sizes (per §6.1 tiers):

- **Body cell content:** Small tier — 10pt minimum, ~10–11pt typical. Line-height 1.2 (working register, tightened from default 1.5 per §6.2).
- **Mono content inside cells:** 8–9pt, slightly smaller than body so mono doesn't visually compete with the data values it labels.
- **Header row** (`<thead>`): mono caps, 8pt, `--text-subtle` color.

Weights:

- Body cell content: Medium (500) default per §6.5; SemiBold (600) for emphasized columns or primary identifier columns; Bold (700) for totals/subtotal values.
- Mono content: Medium on light surfaces, Regular on dark per §6.7.

Structural conventions:

- **Header row:** hairline rule **below only** — no top rule. The header reads as a label band, not a boxed-in element.
- **Body rows:** hairline interior rules at 0.08–0.12 opacity (§6.8). Vertical padding 12px default; 8px for very dense tables. Horizontal padding 12px.
- **Subtotal/total row** (`<tfoot>`): mono caps label spanning multiple columns + body-Bold value in the data column. Hairline rule above at heading-tier strength (§6.8).
- **Units belong in the label cell, not the value cell.** Write `Total Floor Area · 10 Units · Sq Ft` in the label and `18,139` in the value column — not `18,139 SF` in the value column. This keeps the digits in the value column right-aligned with the rows above; appending units breaks digit alignment.
- **Numeric columns are right-aligned.** Use the body face at consistent weight across the column.

**Accent is not used in data tables** except for the current-period column block in financial tables (§7.12). All hierarchy comes from weight, case (mono vs mixed), and hairline structure — not from color. Coloring data cells in accent reads as a stat-row treatment; data tables and stat-rows are different patterns.

---

## 7. Composition patterns

The underlying ICON visual idiom is **engineering-drawing / construction-blueprint**: axonometric volumes, hairline grids as fields, mono-caps callouts, single-accent focal moments. This register threads through every composition pattern below — when in doubt about a layout choice, ask "would this read as a clean blueprint or as polished marketing?" The brand answer is always blueprint.

### 7.1 Panels

Panels are rectangles with internal padding (typically 24px) sitting on the body surface. Panel surface is one step lighter or darker than body — the rules differ for screen vs print bodies (see §2):

**Screen bodies:**
- D+B (G90 body): panel = white (`#FFFFFF`) for clean elevation, or G80 for panel-on-body
- PRIME (G10 body): panel = G12-G15 (`#1F1F1F`-`#262626`)
- Tech (S10 body): panel = S12-S15

**Print body (white, default per §2):** the elevation hierarchy inverts. White can't lift off white, so panels go *down-tier*:
- White body: panel = G90 for subtle lift, or G80 for stronger weight. Used sparingly — print deliverables typically lean on hairlines (§6.8) instead of panels for structure, since the engineering-drawing register prefers ruled separation over filled boxes. Reach for a panel only when a section genuinely needs to feel boxed off (a sidebar, an aside-card §7.8, a callout); otherwise skip panels entirely on print.

Avoid borders on panels; rely on surface contrast. If a border is needed (e.g. for an outlined card variant), use `--rule-chrome` opacity, not the accent.

### 7.2 Dividers

Use `<hr>` or border-bottom. Color from the hairline tier system (§6.8). Never use the accent for dividers — accent is for focal elements only.

### 7.3 Status indicators

Default: filled circle (status dot) + mono uppercase text (status label), color-matched. Both color tokens reference the same semantic state.

Dot size: 8px diameter for default density, 6px for tight rows, 10px for prominent rows.

### 7.4 Callouts (overview)

Reserve callouts for genuine focal moments — one or two per page, not per row. Three concrete recipes, picked by editorial purpose:

- **Panel-on-panel** (subtle elevation): standard callout, lifts a paragraph or stat. No accent stripe; relies on surface-tier contrast (§7.1).
- **Aside-card** (named editorial sidebar with leading-edge stripe): see §7.8.
- **Pull-quote** (display-weight callout for attributed quotations): see §7.9.

Pick by content type: a *quote* uses pull-quote; a *named sidebar* (Series D card, Business Model card, Will Hurd card) uses aside-card; a paragraph that just needs elevation uses panel-on-panel.

### 7.5 Section-head and chrome (letter-format)

**Chrome economy: only pertinent information.** Every chrome element (header items, footer items, page numbers, watermarks, breadcrumbs) must earn its presence by carrying information not available in the body. **Default to minimal chrome and add elements only when they're needed** — do not default to a maximalist trio. The trio described below is the *maximum* for a long-form letter, not the baseline for every deliverable.

**The economy principle extends beyond chrome to hero and caption elements.** Lede paragraphs, hero meta blocks, sub-titles in section captions, and the contextual-right of section captions are all opt-ins per piece, not defaults. A 1-pager whose context is already established through the eyebrow + stat row + table can drop the lede entirely — the hero becomes eyebrow + title alone. A section caption with adequate column headers may not need an h2 sub-title at all. A hero with a clear concept doesn't need a meta block beside the title. Default to less; add elements only when they carry information not available elsewhere on the page. When a section caption *does* have a flex-laid-out left + right (e.g., eyebrow on the left, stat counts on the right), baseline-align them so the type sits on the same baseline regardless of line count.

What to cut, by category:

- **Duplicates of body content.** Drop the project name in the breadcrumb when the hero already shows it. Drop the title in the footer when the cover carries it. Drop the date in the running header when it appears on the cover page.
- **Meaningless given the format.** Drop `Page 01 / 01` on a 1-pager. Drop sequential indices (HI / 01 / END) on a single-page brief. Drop the Orbital watermark in the footer when the wordmark already appears in the header of the same page.
- **Obvious from the format itself.** Drop `PROJECT BRIEF` from a project brief; drop `REPORT` from a quarterly report; drop `LETTER` from an investor letter. The format speaks for itself.
- **Already signaled by the palette.** Drop sub-brand labels like `DESIGN + BUILD` or `PRIME` from the breadcrumb when the body palette (orange, dark surface, etc.) already signals the sub-brand to a reader who knows the brand system.

What typically survives the cut:

- Issuer (wordmark) — required on the first page, optional on running pages of a single-issue document.
- Date or period of issue — useful on every chrome row.
- Sequential index — required on multi-page letters (§7.11), pointless on 1-pagers.
- Source attribution — required in the footer of any data-bearing page (§10.6).
- Contextual right — only when it carries a stat or state not in the body (`61 TITANS RESERVED`, `LAUNCHED · MARCH 11, 2026`).

For a 1-pager the chrome can collapse to: wordmark + date in the header, source attribution in the footer. For a slide, often nothing beyond the wordmark and the page index. For a long-form letter, the full trio earns its keep.

**Long-form letter trio (maximum chrome).** For multi-page letters the section-head row repeats at the top of every body page — three pieces sharing a single row, with a chrome-tier rule beneath:

1. **Index** — large display numeral or short token in accent, tight tracking. Sequential indices for long letters: `HI` (opener) → `01`–`NN` (body) → `END` (closer). See §7.11.
2. **Breadcrumb label** — single mono-caps line, dot-separated. Section context first, current section last: `OBJECTIVE TWO · RESERVATIONS · BUSINESS MODEL`. **Do not** stack lines or append `· cont.` — sequential indices remove the need for a continuation marker.
3. **Contextual right** — single mono-caps line opposite the index. The page's headline state or stat: `61 TITANS RESERVED`, `LAUNCHED · MARCH 11, 2026`, `DOW · 80% OF FY26 REVENUE`, `$201M POLK FOLLOW-ON`, `FY26 GUIDANCE · $103–109M`. Acts as the page's tl;dr — a reader scanning running heads can reconstruct the document.

The whole row sits above a `--rule-chrome` strength horizontal rule; nothing else competes with the section-head visually. The page-footer mirrors the chrome treatment (rule above instead of below) with the page number on the right and a small Orbital watermark on the left — and even these are only earned when the document is multi-page and the wordmark doesn't already appear above.

### 7.6 Stat-row

A horizontal row of N hairline-bracketed stat cells summarizing a page's quantitative content. Common variants: 3-up (objective summary, reservations) and 4-up (financials, metrics).

Cell anatomy:

1. **Label** — mono caps, sub-brand grey. `Q1 2026 REVENUE`, `RESERVATIONS · BUILDERS`, `CASH ON HAND`.
2. **Figure** — single text element, display family, **Bold (700)**, full-strength text. Numerals and any unit suffix (`SF`, `WK`, `%`, `/10`, `M`, `K`) sit in the same text run at the same size and weight — **do not split the unit into a separate span at smaller size or lighter weight.** A stat is one read; the unit reads with it. Default ~24pt; reduce one step at a time if a long figure overflows its cell (e.g., to 22pt or 20pt) before reducing tracking. Stat-row figures **override the §6.3 mixed-case-defaults-to-SemiBold rule** because they read as KPI-tier focal data; consistent Bold across every figure in the row anchors the row visually. **The focal stat** (at most one per row) sits in accent — already Bold, so no further weight bump from §6.3's accent rule. Examples (one text element each): `$22.2M`, `259`, `61 / 100`, `18,139 SF`.
3. **Suffix** — mono caps, subtle grey. The context, comparison, or definition: `41% BETTER THAN $15.7M PLAN`, `1.9 TITANS PER CUSTOMER · AVG.`, `RUNWAY · INTO Q1 2027`.

Top and bottom rules at heading-tier strength (between chrome and interior — see §6.8). Vertical interior dividers between cells at interior strength. First cell flush-left with no left padding; last cell flush-right with no right border. **At most one figure per row in accent** — picking the focal stat is editorial.

### 7.7 Megafig (large two-tone numeral)

Single hero figure where part of the value is in accent. Reserved for the page's *one* focal number — never stacked with other hero numerals on the same page.

Recipes:

- **Range with raised endpoint:** `$103`–**`109M`** — lower bound full text, upper bound accent. The accent calls out the upside.
- **Single dominant numeral in accent:** `213%` — entire figure in accent when the figure itself is the news.
- **Figure with muted unit:** `$22.2M` — figure full strength, unit suffix muted at ~0.55em. Used when the figure is a stat, not a megafig.

Pair with a mono-caps eyebrow above and a mono-caps suffix line below. The pattern's purpose: scanning the page yields *one number* before reading any prose.

### 7.8 Aside-card / sidebar

Named editorial sidebar with three layered text tiers. Used when a paragraph deserves elevation but isn't a quote (see §7.9 for that).

Anatomy:

1. **Solid panel surface** one tier off body (see §7.1).
2. **2pt accent border on the leading edge** (left in LTR layouts). The only place a 2pt stripe of pure accent appears in the system — reads as "focal here".
3. **Eyebrow** — mono caps, accent-colored. Names the card's role: `BUSINESS MODEL`, `SERIES D · IN FLIGHT`, `NEW · Q1 APPOINTMENT`, `FORT POLK · FOLLOW-ON CONTRACT`.
4. **Body** — display weight (Medium 500), 12-14pt, full-strength text. Short — 1-3 sentences. Reads as a "headline statement", not body prose.
5. **Footer label** *(optional)* — mono caps, subtle grey. The card's source attribution or product context: `TITAN PRINT SYSTEM`.

Use **full-width** (spans the body grid) when the aside is the page's editorial moment, or **column-width** (right rail of a 2-col layout) when it sits alongside running prose. Don't nest aside-cards inside aside-cards. Don't combine the leading-edge stripe with pull-quote curly-quote accents on the same callout.

### 7.9 Pull-quote

Attributed quotation, display-weight, set apart from running prose.

Anatomy:

1. **Display body** — Lightspeed, ~24-32pt, line-height ~1.18, slight negative tracking (per §6.4).
2. **Accent-color curly quotes.** The opening `"` and closing `"` glyphs are pure accent (`#FF4F00`); the body text remains full-strength. Implementation: CSS `::before { content: "\201C" }` and `::after { content: "\201D" }` with `color: var(--accent)`. The text-indent of the body is negatively shifted (~−0.4em) so the opening quote hangs into the margin (optical alignment).
3. **Attribution** — mono caps, sub-brand grey. Name + role + provenance, dot-separated. Name in full-strength, role and provenance muted: `DALE MARKS · ASST. SECRETARY OF DEFENSE FOR ENERGY, INSTALLATIONS & ENVIRONMENT · TESTIMONY BEFORE CONGRESS, MARCH 4, 2026`.

Pull-quotes do not get the leading-edge stripe of an aside-card — the accent quotes are the focal device.

### 7.10 Image caption (figure)

Two-column row sitting directly below a figure, separated from running body prose. Left column carries provenance; right column carries description.

1. **Provenance** (left column, narrower) — mono caps, subtle grey, dot-separated. Always begins with `FIG. NN`: `FIG. 02 · FORT BLISS, TX · 10 TRAINING BARRACKS · US ARMY`.
2. **Description** (right column, wider) — body type, sub-brand grey. One sentence describing the substantive content, not the image: `Delivered in 6 months at half the cost of the next best alternative — on time, on budget.`

Use the same caption pattern for stand-alone figures, image pairs, and image grids. For grids with distinct sub-captions per cell (e.g. configuration grids: `Multiple Printers / On Grade / Hillside / Hillside 3 Stories`), promote the per-cell labels to a 4-column caption strip with orange titles + body descriptions; the row's `FIG. NN` provenance still applies as a left-aligned footer label.

### 7.11 Sequential page indices (long-form letters)

For letter-format documents that span more than ~6 body pages, use **sequential indices** in the section-head left position rather than thematic numbering.

Sequence: `HI` (opener / table-of-contents-equivalent page) → `01`, `02`, `03`, … (body pages, monotonically increasing) → `END` (closing / signature / colophon page). Each body page gets its own index regardless of subject — even when two consecutive pages cover the same objective.

Why: thematic numbering ("Objective 02 / Objective 02 cont. / Objective 03") forces a `· cont.` suffix on continuation pages, repeats labels, and makes "page X of Y" navigation harder. Sequential indices remove ambiguity — every page is a unique anchor — and the breadcrumb label (§7.5 piece 2) carries the topical "where am I" content.

Short letters (≤4 body pages) can use thematic indices without ambiguity; the sequential discipline is for longer formats.

### 7.12 Income statement / quarterly table

Multi-period financial table showing N prior periods plus the current period in a highlighted column.

1. **Caption above the table:** mono caps eyebrow (`INCOME STATEMENT · $000s`) + display title (`Quarterly performance · Q1 2025 → Q1 2026`).
2. **Header row:** prior-period columns in muted grey (`2025 / Q1` stacked); current-period column with a **solid accent-color background block** the full height of the data area (`2026 / Q1` over an orange field).
3. **Section-header rows:** mono caps, subtle grey, full-row span: `REVENUE`, `GROSS PROFIT`, `OPERATING EXPENSES`. Hairline gap rows separate sections.
4. **Data rows:** body type, right-aligned numerics, no `$` prefix on individual rows.
5. **Subtotal rows:** Medium weight, `$ ` prefix on figures, descriptive labels (`Total Revenue`, `Gross Profit`, `Total Operating Expenses`, `Adjusted EBITDA`).
6. **Percent rows** (`Gross Margin %`, `Adjusted EBITDA Margin %`): muted treatment to differentiate from currency rows.
7. **Negative values:** render with leading minus or parens; *do not* color negative currency values — the parens carry the signal. Margin-percent rows can use subtle red on dark / vivid red on light when negative.
8. **Footnote(s)** below the table: mono small, subtle grey, leading `*` matching in-table asterisks.

The accent column block is the only place a flood-fill of accent appears in editorial type. It signals "this is the period the document is reporting on."

### 7.13 Cover / hero composition (architectural grid)

The cover or opener page treats the body surface as a blueprint field. Composition rules:

1. **Hairline grid mesh** — chrome-tier hairlines (0.18–0.22, see §6.8) covering most of the cover-stage area. The grid is a hybrid: orthogonal horizontal lines stack vertically (denser toward the horizon), combined with vanishing-point lines radiating from a low-center vanishing point. Not pure 1-point perspective, not pure isometric — the hybrid reads as "construction drawing", not rendered space. **Pre-built grid SVGs are available in the asset library** — see §11.1; pick `WHITE LINES` for dark surfaces, `BLACK LINES` for light, same on-surface logic as the wordmark.
2. **Single accent plumb-line** — a vertical line in pure accent (`#FF4F00`), ~1.5–2pt, dropping straight from the top of the cover-stage through the grid to the horizon. The plumb-line is the singular focal axis of the page.
3. **Accent ring + dot terminus** — at the bottom of the plumb-line, a hollow ring (~24–30pt diameter, ~1.5pt stroke) with a small filled accent dot at its center. This is the literal focal point — where the eye lands.
4. **Hero copy below the grid** — display title in **ALL CAPS** (Lightspeed, ~96–120pt, Bold per §6.3 — uppercase wants the heavier step, tight negative tracking per §6.4). Examples: `INFLECTION POINT`, `Q1 2026 IN REVIEW`. The mono-caps discipline that governs labels and breadcrumbs extends to display hero copy on covers and openers — this is the one place display type goes uppercase. Set against a clean unbroken section of body surface below the grid. The grid + plumb-line + ring carries the visual moment; the hero text carries the verbal moment. They sit on separate vertical bands of the cover-stage.
5. **Issue tag and meta block** — to the left of the hero, a single mono-caps issue pill (`● ISSUE NO. 01·Q1 2026`) outlined in chrome-tier hairline with an accent dot prefix; to the right, a small meta block (`FROM` / `PERIOD` / `ISSUED` keys with body values) separated from the hero by thin chrome rules.

The composition is reusable across openers — replace the hero copy and the meta block contents; keep the grid + plumb-line + ring as the fixed visual signature.

### 7.14 Centered editorial opener

Body-page composition variant for objective opener pages where the page's *concept* is the visual moment. Distinct from §7.13 (cover) — this is a body page that retains the section-head chrome.

Anatomy:

1. **Section-head** at the top, per §7.5 — unchanged from standard body pages.
2. **Centered display title** below the section-head, ~36–48pt, often two lines. Title carries the focal phrase in pure accent on the second line (see §3.2): `Installations are` / **`weapon systems.`**. Single-clause titles can stay full text without accent (`A new platform.` / `Not just a new printer.`) — accent is for the focal *clause*, applied when the second line is the headline.
3. **Centered lede paragraph** below the title, ~14–16pt body, sub-brand grey, max ~3–4 lines. Optional accent phrase highlight for the headline stat or claim (e.g. `representing just over 80% of total 2026 revenue`). One highlight per lede; pick the headline.
4. **Centered hero visual** below the lede — a technical illustration (§10.7), single image, or diagram. Center-aligned with breathing room left and right.
5. **Supporting imagery** at the bottom returns to the standard left-aligned image-pair (§7.10) treatment with the standard caption pattern. The centered composition is for the editorial moment; supporting evidence sits on the standard grid.

Use this when the opener's concept is itself the visual moment. Don't use it for pages that lead with a stat-row or a chart — those want the standard left-aligned section-head + body composition.

### 7.15 Self-review (default process)

After composing, stand back and check:

- One focal element per page? If two compete, demote one.
- Consistent hairline tier within each viewing context?
- Mono is always uppercase?
- Status colors paired (dot + text reference same token)?
- Sub-brand discipline maintained (no orange in Tech, no cyan in PRIME)?
- **Chrome, hero, and caption elements carry only pertinent information?** (§7.5) Cut anything that duplicates the body, is meaningless given the format (`Page 01 / 01` on a 1-pager, sequential indices on a single page), or is obvious from the format itself (`PROJECT BRIEF` on a brief). The lede, hero meta block, and section-caption sub-title are opt-ins, not defaults. When in doubt, cut.
- *(Letter format)* Section-head trio consistent across body pages? (sequential index, single-line breadcrumb, contextual right)
- *(Letter format)* `FIG. NN` numbering monotonic across the document?
- *(Charts)* Single focal stat per chart? Source attribution present? All labels mono caps?

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
- Don't use Lightspeed (display) inside tables — tables use Helvetica Neue (body) and Roboto Mono (mono) only. Lightspeed is reserved for display-tier focal moments (hero, stat-row, megafig) outside table contexts.
- Don't print deliverables on the screen body surfaces (G90, G10, S10) by default — print body is white per §2, unless explicitly requested otherwise. The screen surfaces are tuned for backlit displays and read poorly on paper.
- Don't refer to FormCrete as CarbonX or Lavacrete; replace those names wherever encountered.

---

## 10. Charts, diagrams & technical illustration

ICON ships chart-bearing deliverables continuously (investor letters, board decks, live dashboards). The visual approach is consistent across surfaces: minimal chrome, mono-caps labeling, single-accent focal stat, source attribution always present.

**When to chart.** Whenever a page or panel carries data — a stat, a trend, a comparison — and there's room on the page, consider visualizing it. **Complexity scales with available space:** tight space → a sparkline, a single line, or a one-bar comparison; full space → a combo chart, an annotated time-series, or a richer diagram. Don't shoehorn complex visualizations into corners; don't leave full-page real estate carrying a single number that could carry an arc. The page's real estate is the budget — match the chart to it.

### 10.1 General charting principles

- **Minimal chrome.** No boxed plot frames; no visible axis lines unless absolutely needed for ambiguous baselines (e.g. the zero-line in a chart with negative values). Default to implicit axes — the labels carry the structure.
- **Horizontal-only gridlines** at interior tier (0.08–0.12, see §6.8). No vertical gridlines unless the x-axis is categorical and a vertical reference is essential.
- **Single focal accent.** One point of accent per chart — typically the focal datapoint or focal period. Never two competing accents in the same chart.
- **Mono caps for all labels.** Axis labels, tick labels, legend swatches, source attribution, callout annotations — all mono caps, sub-brand grey at varying opacities.
- **Source attribution is required.** Mono caps subtle grey at chart footer (right-aligned), prefixed `SOURCE:` and including the period covered: `SOURCE: ICON INCOME STATEMENT, Q1 2025 – Q1 2026`. No source = chart is not shippable.

### 10.2 Line charts (Plan vs Actual)

Anatomy:

1. **Plan line** — dashed (4–3 dash pattern), `--text-subtle` strength, 1–1.25pt. **Hollow-ring milestone dots** at each anchor point (~2.5pt radius, body-surface fill + thin grey stroke).
2. **Actual line** — solid accent, ~2pt, round line caps. Single **filled accent dot** at the current/focal datapoint (~3.75pt radius, accent fill + dark stroke for separation from the line itself).
3. **Optional area fill under the actual line** — subtle accent gradient (~0.10–0.15 opacity), bounded by the actual line above and the x-axis below, extending from the line's start point to the focal datapoint x-coordinate. Use when the *area-under-curve* narrative matters — cumulative metrics like reservations, units shipped, revenue YTD. Only the actual/focal series gets the fill; the plan line stays unfilled. Skip when the chart is about *trajectory* (rate, slope) rather than *accumulation*.
4. **Inline callout at focal datapoint** — large display numeral (~14–18pt) in accent, just above the focal dot. Below it, a 2-line mono-caps context label: `61 / Q1 LETTER · MAY 8`. Two-line composition keeps the callout vertical and avoids horizontal collision with line geometry.
5. **Vertical event marker** — dashed chrome-tier hairline at the event x-coordinate, spanning from a few points above the plot top down to the x-axis. Mono-caps label at the top: `LAUNCH · MAR 11`. Use sparingly — at most one event marker per chart.
6. **Plan endpoint annotation** — small mono-caps text near the plan line's terminus (`EOY PLAN · 100`) with a hollow-ring dot at the terminus.

### 10.3 Bar / column charts

- **Prior-period bars** in muted grey (`--g30` to `--g40` on dark, equivalent on light), thin border at chrome strength.
- **Focal-period bar in solid accent** — the only flood-fill of pure accent in the chart.
- **Value labels on top of each bar** in mono caps. Sub-brand grey for prior periods, full strength or accent for the focal period.
- **Optional float callout above the focal bar** — large display figure in accent for the headline number (e.g. `$22.2M`). Use when the focal figure is the point of the chart.
- X-axis labels in mono caps below each bar.

### 10.4 Combo / dual-axis charts

Bars + line on the same chart. Common use: revenue (bars) + margin % (line) over time.

- Bars per §10.3.
- **Line in pure accent throughout** — not just the focal segment. The line is a continuous narrative; coloring the whole line in accent reads as the through-line of the chart.
- **Inline data labels on every line point** (not just the focal one): mono caps, accent or full text strength.
- **Dual y-axes:** primary scale on the left (revenue $, currency), secondary scale on the right (percent, margin). Both in mono caps subtle grey.
- **Legend below the chart** — left-aligned, mono caps. Hollow-square swatch for bar series, filled-circle swatch for line series.

### 10.5 Inline callouts and event markers

Two distinct devices, often co-occurring:

- **Float callout** — a large display figure (display weight, accent) plus a 1–2 line mono-caps context label below it, free-floating near the focal datapoint of a chart. The float callout is *the* takeaway — a reader who reads only the callout should still get the headline. Reserve for one per chart.
- **Event marker** — a vertical dashed line at a specific x-coordinate marking a date or event, with a mono-caps label at the top of the line. Event markers explain *why* the chart shape is what it is (launch event, fundraise close, regulatory date, contract award).

Don't combine an event marker and a float callout at the same x-coordinate — they fight for the same focal slot. Pick one.

### 10.6 Legends and source attribution

Legend placement: top-right of the chart for charts with ≤2 series, bottom-left for ≥3 series. Mono caps. Swatches:

- **Hollow square** — bar/column/area series.
- **Filled circle** — line series in accent.
- **Dash** (`— —`) — dashed line, secondary or "plan" series.

Source attribution: mono caps subtle grey at chart footer, right-aligned, prefixed with `SOURCE:`. Always include the period covered: `SOURCE: ICON INCOME STATEMENT, Q1 2025 – Q1 2026`.

### 10.7 Technical illustrations (variants)

Used for site plans, equipment layouts, system diagrams, process maps, construction details. **Three variants — pick by content type:**

- **§10.7.a Isometric / axonometric** — spatial layouts (site plans, system architecture, process flows). Default for *"where things are arranged in space"*.
- **§10.7.b Orthographic equipment elevation** — single-equipment views (Vulcan, Magma, Titan, containers, modules). Default for *"what the machine looks like"*.
- **§10.7.c Construction detail / cross-section** — cutaway views of structural assemblies (FormCrete walls, slabs, joints). Default for *"how it's built"*.

**Before drawing, search for a reference.** ICON has accumulated illustration references across the asset library (§11) — press kit (§11.4), Hall of Fame photography (§11.2), brand grids (§11.1), tertiary elements (§11.5). Start there; redraw from scratch only if no usable reference exists. Production work is faster and more consistent when it builds on existing references.

**Simple is better than detailed.** A technical illustration's job is to communicate the *concept* — site layout, system relationships, process flow, structural assembly — not to render the subject photographically. Aim for legibility at glance: 12–15 building volumes is enough for "site plan", not 50; 4–6 process nodes is enough for "flow", not 20. If the illustration takes more than a few seconds to read, it's too detailed — strip elements until the focal callouts carry the page.

**Shared anatomy (all three variants):**

1. **Subject artifact in monochrome grey** — `--g30` to `--g50` strokes/fills, chrome-tier line weight. Bulk monochrome, but **focal elements may be tinted accent** — 1–3 per illustration max, treated like §10.5 callouts (never a wash).
2. **Accent connector lines from artifact to label** — thin (~0.75pt), pure accent, **straight or single-bend only** (no curves, no multi-bend dog-legs). Each connector terminates at a tiny accent dot on the target.
3. **Mono-caps callout labels** positioned *outside* the artifact's boundary. Two-line composition typical: `BLDG XX / 1,234 SF`. The connector enters the label block from the artifact side.
4. **No frame, no panel, no background** — sits on bare body surface. The accent connector lines (and focal-tinted artifact elements, if any) are the only color.
5. **Surface-aware strokes** — light strokes on dark surfaces, dark strokes on light, same on-surface logic as the wordmark (§1).

#### 10.7.a Isometric / axonometric

- **Parallel projection at standard 30° angles** — not perspective. The parallel projection reads as "construction drawing", not rendered space.
- Apply the shared anatomy above.

Use for: building/site plans (e.g. Fort Bliss layout), system architecture diagrams, process flow maps, equipment cluster layouts.

#### 10.7.b Orthographic equipment elevation

- **2D orthographic projection** — front, side, or top view. Not isometric, not perspective.
- **Mono-caps labels stenciled *into* the artifact** as integral graphic elements (`MAGMA 2513` on the container, `VULCAN 2513` on the gantry rail, small `ICON` wordmark on a chassis leg). These are part of the drawing, not floating callouts; the standard connector + outside-boundary callout pattern (shared anatomy 2–3) still applies for explanatory annotations laid on top.
- **Hatched detail patterns** — parallel diagonal lines (~30°) for vents, grilles, fabric panels, material indication.
- **Technical accuracy** — proportions, openings, fasteners, and vents drawn correctly. Spec-sheet feel; an engineer should be able to read the elevation.

Use for: equipment overview pages, spec sheets, product brochures, customer technical decks, comparison plates (Vulcan ↔ Magma ↔ Titan).

#### 10.7.c Construction detail / cross-section

- **Cross-sectional view** looking down or through a structural element; internal print layers visible.
- **Continuous serpentine lines** show rebar / continuous internal reinforcement (CIR) routing through the wall cavity. The "snake" pattern is the canonical visual signature for ICON wall sections.
- **Break lines** (zigzag markers) where the section continues offscreen — standard architectural drafting convention.
- **Drafting conventions** for T-junctions, corner conditions, and doorway interfaces; corner radii and joint geometry should match as-built reality.

Use for: "how it's built" pages on FormCrete wall systems, engineering documentation, permit/code-compliance materials, investor education on structural performance.

---

**Production note (all variants):** build illustrations in vector (Illustrator, Figma, Blender for 3D-derived axonometrics) and export as SVG for letter/web use, PDF for print. Stroke weights should be specified in absolute units (pt or px) so they survive scaling across surfaces.

### 10.8 Tertiary design elements (micrographics & labels)

Small decorative graphic ornaments in technical / HUD / terminal aesthetic. Used to add textural detail and "instrument panel" register to layouts without competing with primary content. Source assets live in §11.5.

**Categories** (from the Micrographics Vol.1 + Labels libraries):

- **Bracketed state labels** — `(CALIBRATED)`, `[FUSION]`, `[ANALOG]`, `[CALIBRATING]`. Mono caps in parens or brackets.
- **Numeric IDs / serial markers** — `100%`, `007`, `0079`, `0574`, `005`, `064`, `2026`. Short alphanumeric codes.
- **Process state indicators** — `INSTALLED`, `ONLINE`, `OFFLINE`, `SYSTEM RESET +`, `OVERRIDE +`, `PRE-PATCH`, `COMPLETE`.
- **Module / section IDs** — `ARCHIVE_LOG`, `CTRL`, `CORE_FUNCTION`, `MODULE-09`, `EPOCH`, `DATA CLUSTER`, `NODE`.
- **Asterisk / star / cross glyphs** — small radial bursts (4-, 6-, 8-point, dotted variants) for focal-point markers.
- **Mini diagrams** — tiny concentric/radial/grid patterns simulating sensor readouts or telemetry overlays.
- **Mini telemetry readouts** — 2–3 column blocks of tiny mono-caps text with labels and values.
- **Asian-script accents** — `アクセス` (access), `方式` (method), `デジタル` (digital). Used sparingly as decorative tokens.
- **Geometric markers** — hexagons, diamonds, squares, dot grids, dash patterns.
- **Bracket / frame ornaments** — corner brackets, `< >`, dotted frames.

**Use cases:** page-corner ornaments, section-break decorations, status overlays on dashboards, spec-sheet annotations near figures, watermarks. **Sub-brand neutral** — works across D+B / PRIME / Tech because the technical register doesn't reference a specific palette.

**Constraints:**

- **1–2 micrographics per page max.** They're seasoning, not the meal. Three or more on a page = visual noise.
- **Don't compete with focal content.** Place at margins, corners, or beside body text — never in the visual zone where the page's headline number, hero image, or section title sits.
- **Recolor to match surface.** Black-on-light, white-on-dark — same on-surface logic as the wordmark (§1).
- **Don't translate or modify the Asian-script tokens.** They're decorative; using them as functional copy mistakes their role.
- **Pull existing assets from §11.5.** Don't redraw what already exists — the libraries are licensed for commercial use and cover the common cases.
