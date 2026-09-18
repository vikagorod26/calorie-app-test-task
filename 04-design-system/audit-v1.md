# Design System v1 — Audit

**Date:** 2026-09-15 · **Audited:** [`components-v1.html`](components-v1.html) and [`tokens-v1.md`](tokens-v1.md), before they become the baseline for the Screens stage.
**Result:**
- **Fixed:** 28 internal-consistency findings (§3), 3 touch-target failures (§4.1) and the applicable web-guideline items (§4.4).
- **Also fixed:** 3 problems caught while verifying the fixes, one of them a regression the fixes introduced (§5).
- **Not fixed:** 3 advisories (§4) and 13 ambiguous items flagged for a decision (§6).

After the fixes, every internal check passes and all 33 controls meet 48×48 (§7).

**Line numbers** refer to `components-v1.html` *before* the fixes (the version this audit read). Where a line has moved, the finding names the rule or class so it can be found.

---

## 1. Scope and method

**In scope for the token rules:**
- the system CSS (tokens, type roles, components; pre-fix lines 12–212);
- every specimen inside a `.stage`, including inline `style` attributes;
- the spec tables that document each component.

**Out of scope for the token rules:** the reference-page chrome (header, contents, swatch grid, tables, `.stage` frames, judgment-call panels). It never ships to screens. It was checked against the web guidelines only, and its remaining raw values are listed in §6 (A10).

**Four passes:**
1. **Line-by-line read** of the component CSS (pre-fix lines 86–212) and a grep of every inline `style` attribute.
2. **Rendered computed-style scan** (Chromium, 375 px viewport) of every element inside the specimens, including `::after` pseudo-elements. It collected:
   - every padding, margin and gap value against the 4 px scale;
   - every corner radius against the radius scale;
   - every text, background, outline, border and icon-stroke color, resolved back to its primitive;
   - every rendered font/size/line-height/weight/tracking/numerals combination;
   - every use of Pine, and any macro color used as text.
3. **Hit-target geometry** for all 33 interactive controls (buttons, chips, segments, inputs, selects, stepper buttons), including the invisible `::after` extensions.
4. **Re-verification after the fixes:** the same scan, a source grep for raw values in the component CSS, and a narrow 320 px check.

**External standards used:**
- **Touch targets:** Apple HIG 44×44 pt; Material 3 48×48 dp. The system's own token `size-hit-min` = 48.
- **Accessibility:** WCAG 2.2 AA (1.4.3 text contrast, 1.4.11 non-text contrast, 1.4.4 resize text, 2.5.8 target size).
- **Type minimums:** HIG smallest text 11 pt; Material 3 label-small 11 sp; no inputs under 16 px (iOS focus-zoom).
- **Vercel Web Interface Guidelines**, fetched fresh for this audit via the `web-design-guidelines` skill.
- *There is no `mobile-app-design` skill installed, so HIG and Material 3 figures were applied directly.*

---

## 2. Summary

| Check | Before | After |
|---|---|---|
| **Pine:** one token for every primary action, no near-shades | ✅ Pass. 24 rendered Pine uses, all the single `--color-pine` via `action-primary` / `text-action` / `line-selected` | ✅ Pass |
| **Radius:** only scale values | ✅ Pass. 0 off-scale corners | ✅ Pass |
| **Spacing:** only 4 px scale values | ❌ Fail. 6 px gaps on 41 elements, 6 px margin ×6, 2 px gaps ×10, browser-default 1 px / 6 px button padding ×37 | ✅ Pass. One derived value (A5) |
| **Color roles:** macro colors never text; Pine only for act/chosen | ✅ Pass. 0 macro-colored text, 0 unknown colors, 0 decorative Pine in specimens | ✅ Pass |
| **Type roles:** no off-role size/weight | ❌ Fail. Chip figures at 15 px (no such role); role values re-typed literally in 16 rules | ✅ Pass. 24 rendered combinations, each maps to a role token |
| **Raw values in component CSS** (px, weights, hex) | ❌ Fail. Strokes, sizes, hatch geometry, a 52 px column, a 64 px width, a 16 px icon | ✅ Pass. Source grep finds none |
| **Touch targets ≥ 48** | ❌ Fail. 5 segments at 40, 3 text inputs at 20 px tall, 1 unit select 2 px wide | ✅ Pass. 33/33, minimum 48×48 |
| **Contrast** (AA text, 3:1 non-text) | ✅ Pass | ✅ Pass |
| **Type minimums** | ✅ Pass | ✅ Pass |
| **Docs match implementation** | ❌ Fail. 8 drifts | ✅ Fixed |

---

## 3. Layer 2: internal self-consistency findings

Severity: **High** = breaks a documented rule users would feel (targets, off-role type). **Med** = off-token value. **Low** = hygiene or doc drift.

### 3.1 Spacing (4 px scale)

| ID | Sev | Where (pre-fix) | Finding | Fix |
|---|---|---|---|---|
| S1 | Med | L148 `.matches li`, L154 `.mac`, L181 `.source`, L185 `.chip`, L193 `.seg button` | `gap:6px`, off-scale, rendered on **41** elements. The icon ↔ label gap already had a token (`gap-inline`, 8) that the components ignored | Mark ↔ label ↔ value in `.mac` → `space-1` (4, reads as a word space). Icon ↔ label everywhere else → `gap-inline` (8) |
| S2 | Med | L177 `.mm-top` | `margin-bottom:6px` | → `space-2` |
| S3 | Med | L162 `.split`, L172 `.meter` | `gap:2px`, off-scale and undefined (10 elements) | → new `size-separator` (2). Classed as a line, not spacing (A2) |
| S4 | Med | L174 `.meter .over` | Hatch geometry `2px` / `5px` hardcoded and undocumented | → `stroke-hatch` (2) / `size-hatch-period` (6); the period moved 5 → 6 (A4) |
| S5 | Low | L121 `.btn`, L185 `.chip`, L193 `.seg button`, L209 `.stepper button` | No `padding-block` reset, so the browser's default button padding (1 px block, 6 px inline on the stepper) rendered on **37** controls | `padding-block:0` / `padding:0` |
| S6 | Low | L186 `.chip::after` | `inset:-4px 0` literal | → `calc((var(--size-chip) - var(--size-hit-min)) / 2) 0` |

### 3.2 Sizing and stroke

| ID | Sev | Where (pre-fix) | Finding | Fix |
|---|---|---|---|---|
| Z1 | Med | L165 `.mb-rows li` | Share column hardcoded at `52px` so the columns line up across rows | Rows now share one grid via `subgrid`. Verified: the grams and share columns have identical right edges on all 3 rows |
| Z2 | Med | L210 `.stepper input` | `width:64px` | → new `size-stepper-value` |
| Z3 | Low | L114 `.ico.sm` | `16px`. The doc said "16 inline", but no token existed | → new `size-icon-sm` |
| K1 | Med | L113, 123, 127, 136, 147, 166, 176, 185, 187, 194, 198, 199, 210, 211 | Raw line widths (`1px`, `1.5px`, `2px`, focus offsets, `stroke-width:1.75`) in 14 rules; no stroke tokens existed | → new stroke group: `stroke-hairline` 1, `stroke-emphasis` 1.5, `stroke-focus` 2, `stroke-hatch` 2, `stroke-icon` 1.75 (tokens-v1.md §3.4) |

### 3.3 Typography roles

| ID | Sev | Where (pre-fix) | Finding | Fix |
|---|---|---|---|---|
| T1 | **High** | L189 `.chip .fig` + markup L909–911 | Figures inside macro-match chips set at **15 px / 500**, a size no figure role has (tokens-v1 said `figure-sm`, 14). Their units ("kcal", "g") were plain label text, which breaks the Stage 3 rule "unit attached at lower emphasis, one pattern everywhere" | `ui-chip` 15 → **14 px**, so chip figures use `figure-sm` with the unit style at the same size as their label. **Spec change, flagged (A3)** |
| T2 | Med | L121, 138, 139, 144, 147, 156, 157, 178, 181, 185, 193, 197, 200, 202, 203, 210 | 16 component rules re-typed role values literally (e.g. `font:600 16px/20px`) instead of referencing the role. The scan showed they matched, but a future drift couldn't be detected | Every role is now a token (`--type-*`, `--track-*`, `--type-unit-*`, `--figure-numerals`). Type classes and components apply tokens whole. Note: the `font` shorthand resets `font-variant-numeric`, so numerals are declared after it. The first version of this fix missed that for `.key` figures; see R1 |
| T3 | Low | L1036 (I3 Recipe Detail) | "servings" set as `ui-body` + `text-secondary`, not the unit style of its `figure-lg` value | → `figure-lg` unit style |
| T4 | Low | tokens-v1 §2.2 | The compact strip's 600-weight lead kcal was used but undocumented for `figure-sm` | → `figure-sm-key` (and `figure-md-key`) |

### 3.4 Color roles

| ID | Sev | Where | Finding | Fix |
|---|---|---|---|---|
| — | Pass | All specimens | **Pine:** 4 primary fills, 2 action labels (secondary, text button), 7 outlines (secondary button, selected chips and segments), 11 icon strokes (secondary button icon, chip checks, stepper glyphs). Every one is an action or the current selection, and all resolve to the single `--color-pine`. **Macro colors:** marks, meters and split segments only; 0 text uses. **Unknown colors:** 0 | — |
| C1 | Low | tokens-v1 §1.2 | `text-secondary` listed "macro labels", but macro *row* labels in N2/N3 are `text-primary` (correctly, like any row name) | Doc clarified: strip labels are secondary, row labels are primary |

### 3.5 Radius

Pass. 0 off-scale corners in rendered specimens. Every component uses `radius-xs / md / lg / full`.

### 3.6 Markup hygiene

| ID | Sev | Where (pre-fix) | Finding | Fix |
|---|---|---|---|---|
| H1 | Low | L1122 (J2) | Negative inline margin `calc(-1 * var(--space-1))` to tighten one gap | Removed; the block's `gap-stack` applies |
| H2 | Low | L1129 (J2) | Helper line built from inline styles, including a raw `1px` border | → `.helper` class under N4 |
| H3 | Low | L825 (N3) | Redundant class `p` on one meter | Removed |
| H4 | Low | L161 / L782 (N2) | Dead `.mb-head` wrapper | Removed |
| H5 | Low | L1025, L1136 | Inline `pointer-events` on chevrons | Moved into `.field.select > .ico` |

### 3.7 Documentation drift

| ID | Where | Drift | Fix |
|---|---|---|---|
| D1 | tokens-v1 §3.3 `size-chip` | Claimed segments reach 48 through the 4 px track padding. False: padding belongs to the track, not the button (see E1) | Corrected |
| D2 | HTML F3 spec | "size-chip + track padding = 48 hit" | Corrected |
| D3 | HTML spec tables B2, C2, N1, N2, N4, F1, F2, F3, I1, I2, I3 | Cited raw values (6 px, 16 px, 1 px, 1.5 px, 15 px, "16 px 500") instead of tokens | Now cite tokens |
| D4 | tokens-v1 §2.2 | `ui-chip` 15/20; the 500 variant of `ui-secondary` unnamed | `ui-chip` 14/20 + `ui-chip-selected`; `ui-secondary-strong` |
| D5 | tokens-v1 §3.3 | `size-icon` "20 (16 inline)" as one row | Split into `size-icon` / `size-icon-sm` |
| D6 | tokens-v1 §0, §2.2 | No statement that type, stroke and sizing are tokens too | Added |
| D7 | tokens-v1 §1.3 rule 3, J1 | "2 px gap" | → `size-separator` |
| D8 | tokens-v1 §8 | New tokens and the `ui-chip` change not recorded | Row added |

---

## 4. Layer 1: external standards findings

### 4.1 Touch targets

| ID | Sev | Where (pre-fix) | Finding | Fix |
|---|---|---|---|---|
| E1 | **High** | L193 `.seg button` | Mode-switch segments measured **40 px** tall. The 4 px track padding isn't part of the button, so taps there hit nothing. Below Material 48 dp and HIG 44 pt, and contradicts the system's own `size-hit-min` | Same invisible `::after` extension as chips → 48 |
| E2 | **High** | L198–200 `.field input` | Text inputs in I1/I2 measured **20 px** tall: `height:100%` does nothing inside a flex container with only `min-height`. Tapping the field's upper or lower padding didn't focus the input | `.field` now `align-items:stretch`, so inputs fill the full 48; icons and units are re-centered |
| E3 | **High** | L206 `.portion`, markup L1136 | In a narrower container the unit select collapsed to **2 px** wide (J2 specimen at 375; any Confirmation screen on a 320 px phone) | Portion control wraps: the unit field goes below the stepper whenever it would be narrower than 2 × `size-hit-min`. Unit selects now fill their whole field (`.field.select`), so the chevron and padding are tappable too |
| E4 | Pass | — | Buttons 52; text button 48; stepper buttons 48×52; chips 40 + extension = 48; rows ≥ 68. Chip extensions on wrapped rows meet but don't overlap (4 + 4 = the 8 px gap) | — |

### 4.2 Contrast

All pairs re-checked against tokens-v1 §1.4. Every text pair clears AA; the lowest is Ink Soft on Oat Deep at 4.82:1 (image placeholder). Every non-text pair that identifies a control or state clears 3:1; the lowest is Stone on Oat at 3.41:1. The focus ring (Pine) is 7.47:1 or higher on every surface. Ochre on the Oat meter track is 3.30:1, and meters are supplementary to text anyway.

| ID | Sev | Finding |
|---|---|---|
| E5 | Advisory | Unselected mode segments have no ≥ 3:1 boundary: the Oat Deep track on Oat is about 1.13:1. SC 1.4.11 allows this because the text labels identify the controls, and the selected segment has a 6.59:1 Pine outline. Flagged, not changed |

### 4.3 Type minimums

Pass. The smallest text is 12 px (`ui-overline`, uppercase, +8% tracking), and units go down to 13 px. Both sit above the HIG (11 pt) and Material 3 (11 sp) minimums. Every input is 16 px or larger.

| ID | Sev | Finding |
|---|---|---|
| E6 | Advisory | Type tokens are in px, so the HTML prototypes won't follow OS text-size settings (Dynamic Type, Android font scale). Browser zoom still works. At build, map to pt/sp, and test 200% text (WCAG 1.4.4) at the Screens stage |
| E7 | Advisory | Body is 16 px vs HIG's 17 pt default. Deliberate for one cross-platform system (Material 3 body-large = 16); no change |

### 4.4 Web Interface Guidelines (Vercel), `file:line`

```text
## 04-design-system/components-v1.html

components-v1.html:218  - scroll-behavior: smooth without prefers-reduced-motion → fixed (motion media query)
components-v1.html:969  - placeholder should end with "…" and show an example → fixed ("Search foods, e.g. oats…")
components-v1.html:969, 992, 993, 1020, 1024, 1033, 1133, 1136 - inputs/selects missing name + autocomplete → fixed
components-v1.html:121, 185, 193, 209 - buttons missing touch-action: manipulation → fixed
components-v1.html:(body copy) - straight quotes and apostrophes → fixed (34 quote pairs, 21 apostrophes → curly)
components-v1.html:(chrome h1/h2/h3) - headings without text-wrap: balance → fixed
components-v1.html:(body) - no skip link to main content → fixed
components-v1.html:6    - no <meta name="theme-color"> → fixed (#FFFDF9, page background)
components-v1.html:121, 185, 193, 209 - no hover state → deferred to v2 (default-state-only scope)
components-v1.html:121, 185, 193 - -webkit-tap-highlight-color not set intentionally → deferred with pressed states (v2)
components-v1.html:931, 937 - aria-pressed on a mutually exclusive set → flagged (A7); resolved at Add Food as a tablist
components-v1.html:(buttons, headings) - Title Case rule → not applied, brand voice is sentence case (A6)
✓ pass: icon-only buttons have aria-label · decorative icons aria-hidden · every control labelled · :focus-visible rings · outline:none on inputs replaced by :focus-within ring · tabular-nums on figures · &nbsp; between number and unit
n/a: Intl.NumberFormat (static prototype figures; applies at build) · safe-area insets (Screens-stage layout, not components) · value/onChange hydration (not React)
```

---

## 5. Also fixed during verification

| ID | Where | Finding | Fix |
|---|---|---|---|
| R1 | **Regression from fix T2:** `.fig-md.key`, `.fig-sm.key` | The new `font:var(--type-figure-*-key)` shorthand resets `font-variant-numeric`. Because `.fig-md.key` is more specific than the numerals rule, the bold leading kcal in every strip lost tabular numerals. The post-fix scan showed it (those combinations reported without `tnum`) and was misread at first; a targeted check caught it | The numerals rule now also targets `.fig-md.key, .fig-sm.key`. Re-checked: **56/56** figures render tabular |
| P1 | Page chrome, `.jc-stages` / `.jc-cols` | At a 320 px viewport the reference page scrolled sideways (338 px): judgment-call panel grids had fixed 280 / 260 px minimums | `minmax(min(280px,100%), …)` |
| P2 | Page chrome, `.stage` | The specimen frame's implicit `auto` grid column grew to fit the mode switch's intrinsic width. The frame widened past the viewport instead of showing how the component behaves when narrow, which also made the first 320 px measurement of the mode switch wrong (it reported 95 px segments) | `.stage{grid-template-columns:minmax(0,1fr)}`. The frame now keeps its real width, and the mode switch was re-measured (A8) |

---

## 6. Flagged for a decision (not fixed)

**Decisions (2026-09-15):** A1 → switched to Ink (fixed). A4 → accepted. A7 and A8 → resolved in context on the Add Food screen (`05-screens/02-add-food.html`). The other items stand as recorded.

| ID | Item | Why it's ambiguous | Current state |
|---|---|---|---|
| A1 | **Page header uses Pine as a decorative band** (chrome, pre-fix L223) | It contradicts "Pine means act" on the very page that documents the rule. It also mirrors the stylescape's Pine cover, which is binding presentation precedent. Chrome never ships to screens | **Resolved: switched to Ink.** The band is now `color-ink` with `color-paper` (15.51:1) and `color-rule` (11.58:1) text, so Pine appears on this page only on links and specimen actions. The stylescape keeps its Pine cover: it's a presentation, not a system reference |
| A2 | `size-separator` (2 px) treated as a line token, not spacing | Snapping to the scale (4 px) would split the energy bar and meters into separate pills | Token added, recorded as a judgment call in tokens-v1 §3.4 |
| A3 | `ui-chip` 15 → 14 px | The alternative is keeping 15 and adding a 15 px figure role. 14 reuses existing roles and matches Material's chip label size | Changed and recorded |
| A4 | Hatch period 5 → 6 px | Puts the gap on the 4 px grid. The visual change couldn't be confirmed by screenshot (the browser pane kept timing out); geometry was verified by computed style only | **Accepted** on computed styles; no visual check needed (minor value) |
| A5 | Unit select right padding = 44 px | Off-scale as a number, but derived entirely from tokens (`space-4` + `size-icon` + `gap-inline`), so it clears the chevron | Kept (derived) |
| A6 | Title Case (guidelines) vs sentence case ("Log it") | Brand voice is calm and sentence case; Title Case reads more formal | Sentence case kept |
| A7 | Mode switch semantics: `aria-pressed` buttons vs `radiogroup` / `tablist` | Depends on whether Add Food modes swap whole panels (tabs), which is a Screens-stage layout question | **Resolved at Add Food: `tablist` / `tab` / `tabpanel`.** Each mode swaps the whole panel (results vs. a camera), and IA 4’s two filter modes swap their filter controls, so both uses are tabs. `aria-pressed` would announce three independent toggles; a `radiogroup` implies a form value, not a panel. Manual activation (arrows move focus, Enter or Space selects), because Barcode and Photo start the camera |
| A8 | **Mode switch at small widths (real, minor)** | Measured after P2. With a **303 px** track (375 px phone) all segments fit: 96 px each, 0 overflow. With a **248 px** track (the 320 px frame, which adds page padding) the three icon segments are 77 px and "Barcode" overflows its segment by **2 px**. A real 320 px phone gives a 280 px track (about 88 px per segment), which should just fit, but with no margin. Fixing it is a design choice, not a token fix: drop icons below a container width, stack icon over label, or shorten labels. A container-query threshold would also be the one raw px value CSS can't tokenize | **Resolved at Add Food: text labels, icon-only under `bp-screen-narrow`.** Measured in the real screen with Inter loaded. Icon + label needs about 104 px per segment, so it doesn't fit a 360 px phone. Labels alone fit at 320 px, with 7.8 px to spare in the tightest case (“Barcode” selected, at 600). Under 320 the segments go icon-only (the label stays as the accessible name) and the track gap closes: 49 px wide at 195 px, hit height 48. It reuses the existing breakpoint, so no new raw value. The same measurement caught the S1 body column growing to fit the switch, which would have scrolled a 320 px screen sideways; fixed with `minmax(0,1fr)`, as in P2 |
| A9 | Recipe card `aspect-ratio: 4/3` hardcoded | Imagery tokens are explicitly deferred until imagery is validated at Screens (tokens-v1 §7) | Kept provisional. *Screens, IA 3:* now one token, `ratio-recipe-image`, shared by C3 and the M1 thumbnail, so it changes in one place once imagery is validated |
| A10 | Raw values in page chrome (e.g. `rgba()` overlays at pre-fix L279, L312, L315; `.stage` / `.jc` radii; table and swatch sizes) | Reference-page scaffolding, not system components; token rules don't apply | Kept |
| A11 | Token-based inline layout glue in specimens (pre-fix L642, L849, L1120, L1138; `style="margin:0"` on the J2 title) | Composition inside a specimen, all token-valued or zero | Kept |
| A12 | E5 (segment track boundary), E6 (px type vs OS text scaling) | See §4 | Advisory |
| A13 | Hover, pressed, tap-highlight | Out of v1 scope by decision | v2 |

---

## 7. Verification after fixes

- **Source grep** of the type-role and component CSS for raw `px`/`em`, `font:` with a number, `font-weight`, `font-size`, `line-height`, hex or `rgba`: **none found.** No inline `style` inside a specimen contains a raw px value.
- **Rendered scan, 375 px:**
  - **Spacing:** 0 off-scale values, apart from the derived 44 px select padding (A5) and the `size-separator` knockouts (A2).
  - **Radius:** 0 off-scale.
  - **Color:** 0 unknown colors, 0 macro-colored text.
  - **Pine:** 24 uses, all action or selection.
  - **Type:** 24 font combinations, each mapping to a role token. Chips now render 14/20/500 with `figure-sm` figures; 0 figures without a role.
- **Hit targets:** 33/33 controls at least **48×48** (minimum width 48, minimum height 48, including `::after` extensions).
- **Macro breakdown:** grams and share columns aligned on all rows (same right edges).
- **Tabular numerals:** after R1, **56/56** figure elements compute `tabular-nums` (earlier measurement: "1111" and "8888" both 41.47 px).
- **Narrow widths:** no page-level horizontal overflow at 375 px or 320 px (after P1 and P2). The portion control wraps as designed, so the unit field is full-width below the stepper instead of 2 px. Chips don't overflow. The mode switch fits at a 303 px track but overflows by 2 px at a 248 px track (A8, flagged).
