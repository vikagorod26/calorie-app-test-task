# Design System v1 — Tokens

**Last updated: Stage 7** (current and complete) — extracted and verified against all five final screens in [`05-screens/`](../05-screens/) (revision 2+, Stage 5b cross-screen audit passed) and the audit trail recorded in `CLAUDE.md`. This document and its companion HTML are the single canonical design-system reference; the "v1" name is kept for continuity with the token/component IDs (B1, C2, N2, …), not because a separate "final" version exists.

**Stage:** Design System — a living document, not a Stage-4 snapshot. Built at Stage 4 as the *v1 foundation* (color, typography roles, spacing & sizing, radius, plus two decisions Stage 3 left open), then extended in place through Screens (Stage 5), Stage 6 (interaction states, §10), Stage 6b (propagation to the screens) and Stage 7 (real imagery in M1) — same file throughout, no separate "final" version. The five screens and the clickable prototype in `06-prototype/` carry this system's CSS byte for byte.
**Companion:** [`components-v1.html`](components-v1.html) renders every token and the default-state components built on them. Its CSS `:root` block uses exactly the token names in this document. Audited line by line in [`audit-v1.md`](audit-v1.md).
**Builds on:** [`03-branding/02-hybrid-direction.md`](../03-branding/02-hybrid-direction.md) and [`03-branding/04-stylescape.html`](../03-branding/04-stylescape.html). Both are binding. Anything this document adds or refines is listed in §8 and recorded back in the hybrid direction doc.

**Not in v1 (on purpose), originally:** interaction states (hover, pressed, focus rendering, disabled, error, loading, empty), an error/status color, elevation, motion, a full icon set, and dark mode. See §7. Screens showed which of these were actually needed.

**Added at Stage 6, after all five screens and the cross-screen audit:** hover, pressed, disabled, error and loading for buttons, chips (and the mode switch), inputs and the stepper — see new §10. Elevation, broader motion, empty states beyond E1, the camera-permission flow and dark mode are still open (§7).

**Propagated at Stage 6b; imagery at Stage 7.** The states are wired into the screens that need them, and the M1 image slots carry real dish photographs. `.claude/scripts/propagate-system-css.js` keeps the system block identical across `components-v1.html`, `05-screens/` and `06-prototype/`.

**How to read the citations** (same convention as Stage 3, per the traceability rule in `CLAUDE.md`):
- **Structural/functional choices** cite the brief, [`PRODUCT.md`](../PRODUCT.md), [`01-research/`](../01-research/) or [`information-architecture.md`](../02-information-architecture/information-architecture.md).
- **Aesthetic choices** follow the Stage 3 tone and are marked *(aesthetic judgment)* where a specific value is a designer's pick.
- Anything neither evidenced nor purely aesthetic is flagged **Judgment call**.

---

## 0. Token architecture

**Two tiers.**

| Tier | What it names | Example | Who uses it |
|---|---|---|---|
| **Primitive** | A raw value, named by what it *is*. Uses the friendly names from the stylescape. | `color-pine` = `#2F5245` | Only the semantic tier. |
| **Semantic** | A value named by what it *does*. | `action-primary` → `color-pine` | Every component. |

**Rule: components reference semantic tokens only.** A component never says "pine". It says "primary action". This keeps L3 ("context changes emphasis, not tokens") checkable: logging and recipe components resolve to the same semantic set, so they can't drift apart.

**The same rule covers every token group.** Type (`--type-*`), spacing, sizing, stroke and radius are all tokens. No component rule contains a raw px value, font size or font weight; it applies a token whole. This is verified in `audit-v1.md`.

**Name mapping from Stage 3.** `02-hybrid-direction.md` used working names. v1 splits each into a primitive name (from the stylescape) and a semantic role:

| Stage 3 working name | v1 primitive | v1 semantic role(s) |
|---|---|---|
| `ground` | `color-oat` | `surface-ground`, `meter-track` |
| `paper` | `color-paper` | `surface-paper`, `text-on-action` |
| `ink` | `color-ink` | `text-primary`, `figure-value`, `meter-fill` |
| `ink-2` | `color-ink-soft` | `text-secondary`, `figure-unit` |
| `rule` | `color-rule` | `line-hairline` |
| `pine` | `color-pine` | `action-primary`, `text-action`, `line-selected`, `focus-ring` |
| `pine-tint` | `color-pine-light` | `action-selected` |
| `protein` / `carbs` / `fat` | `color-terracotta` / `color-ochre` / `color-slate` | `macro-protein` / `macro-carbs` / `macro-fat` |
| *(stylescape only)* `--oat-deep` | `color-oat-deep` | `surface-sunken` |
| *(new in v1)* | `color-stone` | `line-control` |

---

## 1. Color

### 1.1 Primitives

| Token | Hex | Friendly name | Origin |
|---|---|---|---|
| `color-oat` | `#F2EDE6` | Oat | Stage 3 palette |
| `color-oat-deep` | `#E7DFD4` | Oat Deep | Stage 3 stylescape CSS; formalized in v1 |
| `color-paper` | `#FFFDF9` | Paper | Stage 3 palette |
| `color-ink` | `#1F2421` | Ink | Stage 3 palette |
| `color-ink-soft` | `#5E605A` | Ink Soft | Stage 3 (`ink-2`) |
| `color-rule` | `#E3DCD2` | Rule | Stage 3 (`rule`) |
| `color-stone` | `#857F76` | Stone | **Added in v1**, see below |
| `color-pine` | `#2F5245` | Pine | Stage 3 palette |
| `color-pine-light` | `#DCE6DF` | Pine Light | Stage 3 palette |
| `color-terracotta` | `#B0513A` | Terracotta | Stage 3 palette |
| `color-ochre` | `#A87A1F` | Ochre | Stage 3 palette |
| `color-slate` | `#4D6A85` | Slate | Stage 3 palette |
| `color-error` | `#B3261E` | — *(no friendly name; a true error, not a brand color)* | **Added at Stage 6**, see §10.4 |

**Why `stone` was added** *(functional; exact shade is an aesthetic judgment)*. v1 introduces the first controls whose edges identify them: a search field, number fields, the portion control and unselected filter chips. WCAG 2.2 SC 1.4.11 asks for 3:1 against the adjacent color for boundaries needed to identify a control. `rule` measures only 1.34:1 on Paper, which is fine for decorative ledger hairlines but can't outline an input. `stone` is a warm grey from the same family as Ink Soft, at 3.90:1 on Paper and 3.41:1 on Oat. **It is a functional neutral, not a brand color:** the stylescape's brand palette (Oat, Paper, Ink, Pine, Pine Light, Terracotta, Ochre, Slate) is unchanged, so the stylescape doesn't need a new swatch. The addition is recorded in `02-hybrid-direction.md` §4.

**Why `color-error` was added** *(functional; the hex is Material 3's error role, checked directly, not a designer's pick)*. §5's J1 write-up reserved this move from the start ("a true error color... must never be reused for over-target"). Stage 6 needed exactly that color, for an out-of-range typed amount (I2/I3) — a value the system can't act on, distinct from over-target (a value it can and does act on). It's a true red, distinct from Terracotta's rust-orange by hue, not just by context, and never appears on a figure (L1 extended). Full reasoning, including the measured contrast this table's own §1.4 row draws from, is in §10.4.

### 1.2 Semantic roles

| Token | → Primitive | Used for | Never for |
|---|---|---|---|
| **Surfaces** | | | |
| `surface-ground` | `color-oat` | Screen background, both contexts | Behind figures inside a data block |
| `surface-paper` | `color-paper` | Every data block: log lists, macro breakdown, daily summary, recipe cards, input fills, unselected chips | Full-screen backgrounds |
| `surface-sunken` | `color-oat-deep` | Mode-switch track; the M1 image box before its image loads (it striped the placeholder before Stage 7) | Meter tracks (Ochre fails on it, see 1.4) |
| `surface-viewfinder` | `color-ink` | The camera feed area in V1 (Barcode and Photo modes). *Added at Screens, IA 2.* In prototypes it stands in for live video | Any other surface: it is not a dark theme and not a card color |
| **Text** | | | |
| `text-primary` | `color-ink` | Titles, body, item names, chip and segment labels (selected or not); the source of a figure (N4 source note, first segment of a C2 meta line) | — |
| `text-secondary` | `color-ink-soft` | Time in a meta line, helper lines, section labels, placeholders, macro labels inside a nutrition strip (macro *row* labels in N2/N3 are `text-primary`, like any row name) | Anything the user must read to act |
| `text-action` | `color-pine` | Text buttons, stepper glyphs, the check in a selected chip | Non-interactive text |
| `text-on-action` | `color-paper` | Label on a primary button | — |
| **Figures** | | | |
| `figure-value` | `color-ink` | Every nutrition value, target, portion amount (including the amount in a C2 meta line), percentage | — (a figure is never tinted, L1) |
| `figure-unit` | `color-ink-soft` | Units and unit-like words attached to a figure: "kcal", "g", "left", "eaten", "/" | The figure itself |
| **Lines** | | | |
| `line-hairline` | `color-rule` | Ledger dividers, separators inside a block | Identifying a control's edge (1.34:1) |
| `line-control` | `color-stone` | Edges of inputs, the portion control and unselected chips | Decoration |
| `line-selected` | `color-pine` | Outline of a selected chip or mode segment | Unselected things |
| `line-guide` | `color-paper` | Corner marks of the V1 framing guide (15.51:1 on `surface-viewfinder`). *Added at Screens, IA 2* | Anything outside the viewfinder |
| **Action** | | | |
| `action-primary` | `color-pine` | Primary button fill, secondary button outline | Anything not tappable |
| `action-selected` | `color-pine-light` | Fill of a selected chip or mode segment | On its own: always paired with `line-selected` (1.26:1 vs Paper) |
| `focus-ring` | `color-pine` | Keyboard/switch focus outline. Rendering finalized at Stage 6 (§10.6): a 2 px outline at a 2 px offset, checked against WCAG 2.2 SC 2.4.7/2.4.13 | — |
| **State** *(added Stage 6, §10.4)* | | | |
| `state-error` | `color-error` | Invalid-field border/icon/text on I2 and I3 only | A figure — the typed value stays `figure-value` (L1); J1's over-target (reserved by design) |
| **Data** | | | |
| `macro-protein` | `color-terracotta` | Protein marks, meter fill, energy-split segment | Text |
| `macro-carbs` | `color-ochre` | Carbs marks, meter fill, energy-split segment | Text; sitting on `surface-sunken` |
| `macro-fat` | `color-slate` | Fat marks, meter fill, energy-split segment | Text |
| `meter-track` | `color-oat` | Unfilled part of every meter (calories and macros) | — |
| `meter-fill` | `color-ink` | Calorie meter fill, including its over-target overflow (see J1), and the target tick on every meter | — |

### 1.3 Usage rules

Rules 1–3 of `02-hybrid-direction.md` §4 still apply. v1 adds the component-level detail:

1. **Pine means "act" or "chosen".** A pine fill, outline or glyph appears only on something tappable (primary/secondary/text buttons, stepper glyphs) or on the current selection (the line and check of a selected chip or segment). *Refinement:* neutral tappables (unselected chips, input fields) are identified by the `line-control` edge, never by a decorative hue. So "no other color is tappable" means no *other hue* marks tappability. *Screens:* a tappable ledger row (C2 `.row-link`) is identified by a trailing chevron in `text-secondary`.
2. **Selection = Pine Light fill + Pine line (+ check on chips). The label stays in Ink.** Pine Light is only 1.26:1 against Paper, so fill alone can't signal selection. The `stroke-emphasis` (1.5 px) Pine outline (8.56:1 on Paper, 6.59:1 on Oat Deep) and the check glyph carry it. *Refinement:* Stage 3's contrast table allowed a Pine label on Pine Light. v1 keeps chip labels in Ink (12.33:1) instead, because macro-match chips contain figures ("Protein ≥ 30 g") and L1 says a figure is never tinted. One rule for every chip is simpler than an exception for chips with numbers.
3. **Macro colors are marks.** Squares, meter fills and energy-split segments only, never text. Adjacent segments are separated by a `size-separator` (2 px) knockout in the surface color, so Terracotta next to Ochre doesn't rely on their low mutual contrast. Meter tracks are `meter-track` (Oat), where all three fills clear 3:1.
4. **No reward, premium or alarm hues.** Over-target is not an error and gets no hue (J1). The one status color, `color-error` (Stage 6, §10.4), marks an invalid typed amount on I2 and I3 only, and is never reused for over-target.
5. **Figures are never tinted, faded or italic.** This includes estimates (J2), targets and percentages.

### 1.4 Measured contrast (WCAG 2.x relative luminance)

| Pair | Ratio | Verdict / use |
|---|---|---|
| Ink on Paper / Oat / Oat Deep | 15.51 / 13.53 / 11.93 | All text and figures ✓ |
| Ink on Pine Light | 12.33 | Selected chip/segment labels ✓ |
| Ink Soft on Paper / Oat / Oat Deep | 6.27 / 5.47 / 4.82 | Secondary text, placeholders ✓ AA |
| Pine on Paper / Oat / Oat Deep | 8.56 / 7.47 / 6.59 | Text buttons, stepper glyphs, selected outlines ✓ |
| Paper on Pine | 8.56 | Primary button label ✓ |
| Stone on Paper / Oat | 3.90 / 3.41 | Control edges ✓ (≥ 3:1, SC 1.4.11) |
| Terracotta / Ochre / Slate on Paper | 5.06 / 3.78 / 5.56 | Marks ✓ (non-text ≥ 3:1) |
| Terracotta / Ochre / Slate on Oat (meter track) | 4.42 / 3.30 / 4.85 | Meter fills ✓ |
| Terracotta / Ochre / Slate on Oat Deep | 3.89 / **2.91** / 4.28 | ✗ Ochre fails, so tracks are never Oat Deep |
| Error on Paper / Oat / Oat Deep | 6.43 / 5.61 / 4.95 | ✓ AA text/icon (I2/I3 only, §10.4) — 4.95 on Oat Deep is the weakest of the three, still clears 4.5 |
| Ink on Oat (calorie meter) | 13.53 | ✓ |
| Rule on Paper | 1.34 | Decorative hairlines only |
| Pine Light on Paper | 1.26 | Never a selection signal on its own |
| Paper on Oat | 1.15 | Card edges are not a legibility device (Stage 3 note stands) |

Meters are also supplementary: every meter sits next to the same information as text ("70 of 120 g", "50 g left"), so no value is conveyed by a bar alone.

---

## 2. Typography

### 2.1 Families

| Token | Stack | Settings |
|---|---|---|
| `font-voice` | `"Newsreader", "Iowan Old Style", Georgia, "Times New Roman", serif` | Variable, `font-optical-sizing: auto` (opsz 6–72) |
| `font-ui` | `"Inter", ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, Arial, sans-serif` | Weights 400 / 500 / 600 |
| `figure-numerals` | *(feature, not a family)* | `font-variant-numeric: tabular-nums lining-nums` on every figure role |

### 2.2 Role scale

Size/line-height in px. Tracking relative to font size.

| Token | Family · weight | Size / line | Tracking | Used for | IA screens |
|---|---|---|---|---|---|
| **Voice** | | | | | |
| `voice-display` | Newsreader 400 | 32 / 36 | −1.5% | Recipe title on Recipe Detail | 5 |
| `voice-title` | Newsreader 400 | 26 / 32 | −1% | Screen title (the day, "Add food", "Recipes"); food/dish name on Confirmation, which is that screen's one serif element | 1, 2, 3, 4 |
| `voice-heading` | Newsreader 400 | 22 / 28 | 0 | Recipe section heads (Ingredients, Method) | 5 |
| `voice-card` | Newsreader 400 | 20 / 26 | 0 | Recipe card titles | 4 |
| **Interface** | | | | | |
| `ui-body` | Inter 400 | 16 / 24 | 0 | Body copy, ingredient lines, method steps, input text | 2–5 |
| `ui-body-strong` | Inter 500 | 16 / 24 | 0 | Item names in ledger rows | 1, 2 |
| `ui-label` | Inter 600 | 16 / 20 | 0 | Button labels | all |
| `ui-chip` · `ui-chip-selected` | Inter 500 · 600 (selected mode segment or current tab) | 14 / 20 | 0 | Chip, mode-switch and tab labels (S2) | 1, 2, 4 |
| `ui-secondary` · `ui-secondary-strong` | Inter 400 · 500 | 14 / 20 | 0 | Meta, helper lines, match criteria · *strong:* source notes, field labels | all |
| `ui-overline` | Inter 500 | 12 / 16 | +8%, uppercase | Section labels inside blocks ("PER SERVING") | all |
| **Figure** | | | | | |
| `figure-hero` | Inter 600, tnum | 48 / 52 | −2% | Remaining kcal on Today; total kcal on Confirmation / nutrition panel | 1, 3, 5 |
| `figure-lg` | Inter 600, tnum | 24 / 28 | −1% | Portion value in the portion control | 3, 5 |
| `figure-md` · `figure-md-key` | Inter 500 · 600 (leading kcal in a strip), tnum | 16 / 24 | 0 | Ledger row kcal, default nutrition strip, macro breakdown rows, values typed into number fields | 1–5 |
| `figure-sm` · `figure-sm-key` | Inter 500 · 600 (leading kcal in a compact strip), tnum | 14 / 20 | 0 | Compact strip on recipe cards, meter captions, figures inside chips and match criteria; the answer in a macro line ("50 g left", `figure-sm-key`) | 1, 4 |

The anchors in `02-hybrid-direction.md` §5 (hero 44–48, recipe title 30–32, card 18–20, body 16, secondary 13–14, label 12) are each resolved to one value above *(aesthetic judgment within the given ranges)*.

**Implementation.** Each role is one token, `--type-<role>` (a `font` shorthand), plus `--track-<role>` where tracking isn't 0. Unit styles are `--type-unit-hero / lg / md / sm`, and numerals are `--figure-numerals`. Components apply a role token whole and never restate a size or weight. *Audit v1 change:* `ui-chip` went from 15 to 14 px, so figures inside chips use `figure-sm` and stay on the same size as their label. Before, they were set at an off-role 15 px.

### 2.3 Rules

1. **Numbers are never serif** (Stage 3, unchanged). A figure role is always `font-ui` with `figure-numerals`, including inside chips, inputs and match criteria.
2. **Figure + unit pairing.** The value uses `figure-value`, and the unit uses `figure-unit` one step smaller at a lighter weight. The two are joined by a non-breaking space ("412 kcal" never wraps).

   | Figure role | Unit style |
   |---|---|
   | `figure-hero` | `type-unit-hero`: Inter 500, 17 / 24 |
   | `figure-lg` | `type-unit-lg`: Inter 400, 15 / 28 |
   | `figure-md` | `type-unit-md`: Inter 400, 14 / 24 |
   | `figure-sm` | `type-unit-sm`: Inter 400, 13 / 20 |
| Status word "over" (J1, revised at Screens) | `type-unit-hero-strong`: Inter 600, 17 / 24 · `type-unit-sm-strong`: Inter 600, 13 / 20 · color `figure-value` |

   Words that behave like units ("left", "eaten", "target", "over", and portion words such as "g", "ml", "serving", "slice") and the "of" in "70 of 120 g" take the unit style (v1's "/" was retired at Screens, J1). **Every number, including the target, stays in `figure-value`.** *Screens:* `figure-hero` is the one figure whose unit may wrap below it when the line is too narrow (a wrapping flex row with a `space-1` gap); every other figure keeps its unit on the same line.
3. **Serif budget** (Stage 3, unchanged): at most one `voice-*` element per logging screen (IA 1–3), no cap on recipe screens (IA 4–5).
4. **Floors.** 12 px is the smallest size, used only by `ui-overline`. Input text is never below 16 px *(functional: iOS zooms the viewport on focus for inputs under 16 px)*.
5. **Weight before size** (Stage 3, unchanged). Size jumps are reserved for `figure-hero` and `voice-display`/`voice-title`.

### 2.4 Verification

Stage 3 asked for two checks when the system was built (`02-hybrid-direction.md` §5).

- **Tabular figures: ✓ confirmed.** `components-v1.html` was rendered in Chromium with Inter loaded (confirmed via `document.fonts.check`) — at Stage 4 from Google Fonts; since Stage 7b the identical woff2 files are vendored in `assets/fonts/`. At `figure-md` with `tabular-nums lining-nums`, "1111" and "8888" both measure **41.47 px**. With proportional figures they measure 26.56 px vs 40.28 px. So this Inter build keeps the `tnum` feature, and right-aligned figure columns line up digit for digit. The page includes a side-by-side "Tabular check" specimen.
- **Newsreader optical sizes:** the vendored variable font carries the `opsz 6..72` axis, and `font-optical-sizing: auto` is set on every voice role. The smallest voice role (20 px card title) and the largest (32 px display) both sit inside the axis range, so each gets its own optical cut.

---

## 3. Spacing & sizing

### 3.1 Scale (4 px base)

| Token | Value |
|---|---|
| `space-1` | 4 |
| `space-2` | 8 |
| `space-3` | 12 |
| `space-4` | 16 |
| `space-5` | 20 |
| `space-6` | 24 |
| `space-8` | 32 |
| `space-10` | 40 |
| `space-12` | 48 |
| `space-16` | 64 |

A 4 px base keeps every value on the 4 pt / 4 dp grid both iOS and Android lay out on *(functional: Platform decision in `CLAUDE.md`, one cross-platform system)*.

### 3.2 Semantic spacing

| Token | → | Used for |
|---|---|---|
| `inset-screen` | `space-5` (20) | Left/right screen gutter, both contexts |
| `inset-block` | `space-4` (16) | Padding inside a paper block or card body |
| `row-pad-y` | `space-3` (12) | Vertical padding of a ledger row, macro row or meter row |
| `gap-inline` | `space-2` (8) | Between chips; icon ↔ label |
| `gap-stack` | `space-3` (12) | Between elements inside one block |
| `gap-section-log` | `space-6` (24) | Between blocks on logging screens (IA 1–3) |
| `gap-section-recipe` | `space-10` (40) | Between sections on recipe screens (IA 4–5) |

**The emphasis dial, made concrete.** Logging and recipe screens use the *same scale* but pick different steps for section rhythm: 24 for ledger density (H1), 40 for cookbook pacing (Stage 3 kept B's "generous spacing on recipe screens"). Two picks from one scale are a difference in emphasis, not in tokens (L3). *(Exact steps: aesthetic judgment.)*

### 3.3 Sizing

| Token | Value | Used for | Grounding |
|---|---|---|---|
| `size-hit-min` | 48 | Minimum touch target for anything tappable | `PRODUCT.md`: native conventions respected for touch targets. 48 satisfies both Material (48 dp) and Apple HIG (44 pt) with one number |
| `size-control` | 48 | Input field height | = hit minimum |
| `size-button` | 52 | Primary/secondary buttons, portion control | Slightly taller than the minimum for the one-handed primary action (H1) *(aesthetic judgment: +4)* |
| `size-chip` | 40 | Visual height of chips and mode segments. The hit area is extended to `size-hit-min` by an invisible `::after` reaching (`size-chip` − `size-hit-min`) / 2 above and below. *(Audit v1: segments previously relied on track padding, which isn't part of the button, so their real target was 40.)* | Keeps dense filter rows compact without shrinking targets |
| `size-icon` | 20 | Icons; round caps, `currentColor` | *(aesthetic judgment)* |
| `size-icon-sm` | 16 | Inline icons: chip check, source note, match check | *(aesthetic judgment)* |
| `size-mark` | 10 | Macro color square | Stage 3 stylescape |
| `size-meter` | 8 | Meter and energy-split bar height | *(aesthetic judgment)* |
| `size-stepper-value` | 64 | Value box in the portion stepper | Fits "1.5" / "250" at `figure-lg` |
| `size-separator` | 2 | Knockout between meter and energy-split segments | A line, not spacing (see 3.4) |
| `size-hatch-period` | 6 | Repeat length of the over-target hatch (J1) | *(aesthetic judgment)* |
| `inset-safe-top` · `inset-safe-bottom` | `env(safe-area-inset-*)` | Added to the S1 header's top padding and the S2 bottom bar's bottom padding | **Added at Screens.** Platform values from the OS, not design values (Stage 4 carry item "safe-area insets"). Prototypes simulate them in the device frame |
| `meter-target` | 87% | Position of the target on every meter track, marked by a tick (about 15% headroom past the target) | **Added at Screens** (critique run 2, N2). One scale for calories and macros, under and over target *(aesthetic judgment: headroom)* |
| `size-viewfinder-min` | 320 | Minimum height of the V1 camera area; above it, the area takes the rest of the screen | **Added at Screens (IA 2).** Keeps the photo guide large enough to fit a plate when the screen is short *(aesthetic judgment)* |
| `size-guide-corner` | → `space-6` (24) | Length of each corner mark on the V1 guide | **Added at Screens (IA 2)** *(aesthetic judgment)* |
| `size-thumb` | 120 | Width of the M1 thumbnail on Food Confirmation (Flow 3 only) and on every C3 card | **Added at Screens (IA 3)**, originally the smallest width at which the placeholder label stayed legible in three lines; hybrid §3 asks for a small thumbnail. **Confirmed at Stage 7:** all ten real dish images stay identifiable at this size *(was an aesthetic judgment, now tested)* |
| `ratio-recipe-image` | 4 / 3 | Crop of recipe images: the C3 card image, the M1 Confirmation thumbnail and the IA 5 hero | **Added at Screens (IA 3)**, replacing the literal in C3. One token, so the thumbnail matches the card the recipe was chosen from. **Audit A9 closed at the Stage 7 imagery pass:** the shared crop holds at both rendered sizes against real images |
| ~~`size-placeholder-stripe`~~ | → `space-2` (8) | Stripe width of the M1 image placeholder | **Added at Screens (IA 3); retired at Stage 7** — M1 carries real images, so the striped fill it sized no longer exists. Nothing else referenced it |
| `ratio-guide-barcode` · `ratio-guide-photo` | 2 / 1 · 1 / 1 | Shape of the V1 guide: a wide frame for a barcode, a square for a plate | **Added at Screens (IA 2).** Barcodes are wide; the square asks for the whole plate, since portion is the part photo estimates get wrong most (`01-secondary-research.md`, Cal AI) |
| `bp-screen-narrow` · `bp-screen-compact` | 320 · 280 | Container widths of S1 (`screen`) where S2 shortens "Add food" to "Add", then goes icon-only, and C2 drops the kcal figure below the meta line. *Add Food (A8):* under `bp-screen-narrow` the F3 mode switch goes icon-only | **Added at Screens** (critique R4). The only raw px in component CSS: container-query conditions can't read custom properties (the audit A8 limit). Derived from measured bar widths, see `05-screens/01-today.html` checks |

### 3.4 Stroke

Line weights aren't spacing, so they sit outside the 4 px scale. They're still tokens, and no component sets a raw width.

| Token | Value | Used for |
|---|---|---|
| `stroke-hairline` | 1 | Dividers (with `line-hairline`); control edges (with `line-control`) |
| `stroke-emphasis` | 1.5 | Selected outline on chips and segments; secondary button outline |
| `stroke-focus` | 2 | Focus ring width and offset (rendering finalized at Stage 6, §10.6) |
| `stroke-hatch` | 2 | Stripe width of the over-target hatch |
| `stroke-icon` | 1.75 | Icon stroke (unitless, SVG) |
| `stroke-guide` | 3 | Corner marks of the V1 framing guide. Heavier than every other line because it sits on a moving camera image. *Added at Screens, IA 2* |

**Judgment call, recorded by the audit:** the 2 px knockout between segments (`size-separator`) is classed as a *line*, not a spacing gap. Snapping it to the spacing scale (4 px) would visibly split the energy bar and meters into separate pills.

---

## 4. Radius

| Token | Value | Used for |
|---|---|---|
| `radius-xs` | 3 | Macro marks (as in the stylescape) |
| `radius-sm` | 8 | Small thumbnails (e.g. recipe thumbnail on Confirmation when arriving from Flow 3) |
| `radius-md` | 14 | Buttons, input fields, portion control |
| `radius-lg` | 20 | Paper blocks, recipe cards |
| `radius-full` | 999 | Chips, mode switch, meters |

**Shape follows role** *(aesthetic judgment, functional intent)*: things you *choose* are pills (chips, mode segments), and things that *do* something or take input are rounded rectangles (buttons, fields). A selected chip and a primary button can both carry pine, so shape keeps "chosen" and "act" apart at a glance. Radii step up with container size, so nested corners stay visually concentric.

---

## 5. Two judgment calls (decided at Stage 4, tested on the screens)

Stage 3 left two questions open for this stage (`PRODUCT.md` "Still undecided" / "Still open"; `02-hybrid-direction.md` §4 rule 4). Both are decided here as **judgment calls**. Research doesn't say how users want either framed. The decisions are derived from the Stage 3 brand rules. Both were then tested on the real screens: J1's revisit condition was met and it was revised (below); J2 held as specified.

### J1 · Over-target tone — **Judgment call**

**Decision: going over a target is information, not an alarm. No status hue at all.**

- The hero figure keeps its treatment and changes its word: "1,273 kcal **left**" becomes "180 kcal **over**". There's no minus sign, no red, no warning icon and no exclamation.
- The caption keeps both numbers checkable: "2,180 eaten · 2,000 target".
- The meter fills solid Ink up to the target, then a `size-separator` (2 px) gap marks the target point, and the overflow continues in **hatched** Ink (`stroke-hatch` stripes every `size-hatch-period`). Hatching carries "past the target" without color, so it also works for color-blind users and in grayscale.
- Macros use the same pattern with their own mark color and a hatched overflow (worded "12 g over" since the Screens revision below).
- The same wording is used for every goal. The system doesn't judge whether "over" is good or bad.

**Why** (grounded, not evidenced):
- **"Over" isn't bad for every user.** `PRODUCT.md` and Segment 1 (`02-audience-5w.md`) include people *gaining* weight and training, not only losing. Going over a protein or calorie target is the goal for some of them. An alarm color would misread half the audience.
- **Brand tone:** the stylescape's mood slide says "No confetti, no guilt trips". Red for "over" is a guilt trip, and green for "under" is the reward color Stage 3 excluded (§4 rule 3).
- **L1:** figures are never tinted, and a red number would be a tinted figure.
- **Color is never the only carrier:** the word "over" and the hatch carry the meaning.

**Rejected:** red/terracotta figure or meter (tinted figure, alarm tone, and Terracotta already means protein); an amber "warning" state (same problem, plus a new status hue); a negative number "−180" (ambiguous in a remaining-calories context); a celebratory state for staying under (reward mechanics, excluded in Stage 3).

**Revisit condition (set at Stage 4):** "over" is too easy to miss at a glance on Today (H1: glanceability). The first fallback is stronger typography (for example, the word "over" at hero weight), not color. **Met — see below.**

**Revised at Screens (IA 1), after the Today critique: the revisit condition was met.** In frame B of `05-screens/01-today.html`, "47 kcal over" and "808 kcal left" differed only in a small grey word, a 47 kcal overflow drew a hatch about 5 px wide, and a macro overflow had no word at all. The fixes are typographic and geometric, still with no hue:
- The word "over" is set in `type-unit-hero-strong` (Inter 600) in `figure-value` Ink. "left" keeps the unit style, so the weight changes only when the state does.
- **Shared meter scale (critique run 2, N2).** Every track places the target at `meter-target` (87%, about 15% headroom), marked by an Ink tick in the separator gap. Under target the fill is eaten ÷ target of that position. Over target the solid fill stops at the tick and the hatch continues past it, capped at the track end. Protein at 92% and calories at 102% now end at visibly different points. This replaced a short-lived 24 px minimum overflow width (`size-overflow-min`), which rescaled over-target meters so they looked shorter than under-target ones.
- **Bold "over" kept (user decision, critique run 2, N1). Judgment call.** The second review read a bold "over" on a 2.3% overage as an alarm set in type. Both alternatives were considered: a neutral "2,047 of 2,000 kcal" hero, and "over" back at unit weight. Bold stays because revision 1 showed the plain word was missed. The objection is recorded here, to revisit with real users.
- Macro lines state the answer in words: "50 g left", or "8 g **over**" (`figure-sm-key`, with `type-unit-sm-strong` for "over"), with "70 of 120 g" beside the name. This also retires "/", which screen readers announce as "slash".
- The framing itself ("left" for every goal) is unchanged. Reopening it was considered and declined.

### J2 · AI-photo estimate display — **Judgment call**

**Decision: say it's an estimate in words, keep the figures exact in form, and put the check within reach.**

1. **Figures unchanged.** An estimated 560 kcal looks exactly like a database 560 kcal: same role, tabular, Ink. No "~", no range, no fading, no italics.
2. **A source note says where the number came from.** The **Source note** component (N4: `size-icon-sm` icon + `ui-secondary-strong` in `text-primary`; `text-secondary` until the Screens typeset pass) names the method on Food Confirmation: *Photo estimate*, *Barcode*, *Food database* or *From recipe*. Every method gets one, so the photo one isn't singled out as a defect but is still honest. The note is not a chip and not tappable, so it's not pine and has no outline.
3. **One helper line, only for photo:** "Estimated from your photo. Check the portion before you log it." It sits directly above the portion control, which is where the check happens. It's styled as `ui-secondary` in `text-secondary`, with a `stroke-hairline` rule above it. *Screens, IA 3:* when a photo entry is reopened from Today (Flow 4), the line drops “before you log it”, which only fits a new entry, and reads “Estimated from your photo. Check the portion.”
4. **The provenance survives logging.** The Today row keeps it in its meta line. *Screens typeset pass:* the source leads that line with its icon, in `ui-secondary-strong` · `text-primary`, ahead of the amount (a figure) and the time: "[camera] Photo estimate  1 serving · 19:40". The line ranks source > amount > time, because the accuracy of the logging method is "the top scrutiny point" and being "transparent about confidence" has "outsized upside" (`01-secondary-research.md`). When space runs out, the amount and time wrap together; the source never does. **Accepted trade-off (user decision):** at 390 px, 5 of 8 rows in frame B take a second meta line (list 564 → 668 px, about 18% taller). A tighter-gap variant (icon gap `space-1`, source-to-amount gap `gap-inline`, 3 of 8 rows wrapping) was measured and rejected, because "Food database 150 ml" starts to read as one phrase and that undoes the legibility goal. Density is left to backlog item N3.

**Why** (grounded, not evidenced):
- **AI-photo accuracy is Cal AI's most-repeated complaint.** Misidentified foods and wrong portions (`01-secondary-research.md`), and the same research notes that "being transparent about confidence has outsized upside".
- **Copy guardrail from Stage 3:** figures are presented as consistent and checkable, not promised as accurate.
- **H2:** trust depends on each logging method's own accuracy, so naming the method for every entry is the consistent, method-neutral way to be transparent.
- **Figures stay exact in form (L1)** because the estimate becomes a real log entry that sums into Today's total. A range or "~" can't be summed and would make the daily total look vague too.
- **The portion is the most commonly wrong part** of a photo estimate (Cal AI complaints) and a known friction point in general (Cronometer serving-size thread), so the helper line points at it.

**Rejected:**
- **A confidence percentage** ("92% match"): it reads as a precision claim the product can't back, which breaks the guardrail.
- **Ranges** ("480–620 kcal"): can't be logged as one entry.
- **"~" prefix, faded or italic figures:** break L1, and Stage 3 found approximate-looking numbers erode trust.
- **An amber "unverified" badge:** a status hue plus alarm tone.
- **An itemized "what we identified" breakdown:** plausibly useful, but it adds data to IA screen 3 that the IA doesn't list. Not added at Screens either; it stays an idea for user testing, not a silent addition.

**Structural note:** the source note adds one piece of information to IA screens 1 and 3 (where the entry came from). It's traceable to H2 and the photo-accuracy finding. Applying it to *all* methods, not only photo, is part of this judgment call.

**Held at Screens.** J2 shipped as specified on Food Confirmation and Today; the only change was the reworded helper line for a reopened entry (point 3). **Still open, for real users rather than a design review:** whether the helper line becomes noise for repeat photo loggers (H1). A candidate change is showing it only until the user has adjusted a portion once.

---

## 6. Components in v1 (index)

Specified and rendered in `components-v1.html`. All were originally **default state only**; as of Stage 6 (§10), B1–B3, F1–F3, I1–I2 and I3 additionally cover hover, pressed, disabled, error and loading — everything else below is still default-state only. For chips and mode segments, *selected vs. unselected* is a value the component displays, not an interaction state, so both are shown. The same goes for a meter being under or over target.

| ID | Component | IA screens | Source |
|---|---|---|---|
| B1 | Button · primary ("Log it", "Log this", "Add food") · *Screens:* on Recipe Detail the label carries the live count, "Log this · 1.5 servings" (critique P1: a bare "Log this" never said what it would log); on a reopened entry (Flow 4) it reads "Save changes" | 1, 3, 5 | IA structural rules 1–2; H4 same button (hybrid §3) |
| B2 | Button · secondary — **confirmed, three uses** | 2, 3 | *IA 2:* "Type the barcode number" (Barcode fallback, grounded in the reproducible scanner failures in `01-secondary-research.md`) and "Estimate from a photo" (the E1 no-match action). *IA 3:* "Retake photo", stacked above "Log it" in S3 so B1 never moves |
| B3 | Button · text · `.btn-flush` for a text button at the start of a column (“Back”, “Cancel”) — **confirmed, six uses, every exit named to its destination with an `sr-only` suffix** (a Stage 5b audit fix: "Close" was the one exit that didn't name where it went) | 2, 3, 4, 5 | *IA 2:* "Close" (→ "and return to Today"). *IA 3:* "Back" (→ the search results / scanner / camera / recipe), "Cancel" (an edit's exit, → "and return to Today"), "Remove entry" (destructive, top end of the header row, opposite Cancel), "Search instead" (→ Add Food, Search — on **both** the barcode and photo frames, so a wrong barcode match has the same escape as a misidentified photo; a Stage 5b audit fix). *IA 4:* "**Reset to my usual**" (the anticipated "Reset to my targets" is confirmed real, under its shipped name), beside the results count, appearing only once the filter differs from what was saved. *IA 5:* "Back" (→ Recipes & Filter) |
| C1 | Paper block (+ label above a list block, added at Screens) · two label treatments: a plain `ui-overline` list-label (IA 1, 2) and, where the label also carries a live count or verdict, `.list-head` — the label in `ui-secondary-strong` beside the one control that acts on the whole list ("Reset to my usual", IA 4) | all | Hybrid §4 `paper`; L1 |
| C2 | Ledger row (log entry / search result) · *Screens:* tappable `.row-link` with chevron; meta line with three roles, source first · *Add Food critique:* when every row shares one source (search results), the list label names it once and the meta line carries only the serving | 1, 2 | IA 1 entry list; IA 2 results with kcal/serving; ledger alignment (A); IA Flow 4 (a logged entry opens Screen 3) |
| C3 | Recipe card · *Screens, IA 4:* the image slot is M1 (a real image since Stage 7); `.rcards` is the results list; the whole card is one `.rcard-link` to Recipe Detail, **without** a chevron (**judgment call**: a card already reads as an object, where C2's ledger row needs the chevron to read as tappable). **Match rule:** a match names *your* criterion, never the recipe's figure, which is already in the strip above it. *After the IA 4 critique:* **`.rcard.compact`** puts the M1 thumbnail beside the body instead of full-bleed above it (398→210 px), so results are comparable without scrolling; the hero crop (full-bleed) stays for Recipe Detail. The `.matches` list's `aria-label` differs by mode — "Also suits" in tag mode (the recipe's *other* diet tags, screen-reader only; left standing as a Stage 5b finding, since sighted users see none) and "Closest to your limits" in macro mode (the two tightest margins, e.g. "170 kcal under your limit") | 4 | IA 4 result content: name, image, kcal/serving, matched criteria |
| N1 | Nutrition strip (default, compact) | 3, 4, 5 | P0 #4 macro breakdown; L3 same strip in log and recipe context |
| N2 | Macro breakdown · *Screens, IA 3:* labelled “Your portion” on Confirmation (static `ui-overline`, since the portion is set below it, in I3, not by this label), “Per serving” on Recipe Detail; *after the IA 3 critique:* a “% of kcal” column label (`.mb-head`) over the shares · *after the IA 5 critique:* **a label that names the amount takes `.mb-amount`** (`ui-secondary-strong` · `text-primary`, the count as a `figure-sm`), because `text-secondary` is barred from anything the user must read to act (§1.2); a label that names the section keeps `ui-overline`. *On Recipe Detail the label is uniformly `.mb-amount`* — one string bound to the serving stepper, reading “Per serving” at the default 1 and “For 1.5 servings” once adjusted, not two labels switched by content | 3, 5 | IA 3 full macro breakdown; IA 5 nutrition per serving |
| N3 | Daily target summary · *Screens:* no overline, macro lines "50 g left" / "8 g over", J1 revised | 1 | IA 1 remaining/consumed vs target; P0 #5; Segment 1 "running daily budget" |
| N4 | Source note · *Screens typeset:* `text-primary`; also leads every C2 meta line | 1, 3 | J2; H2 |
| F1 | Filter chip · diet tag · *Screens, IA 4:* in use, in two labelled `.fgroup`s ("How you eat", "Avoid"), pre-selected from saved preferences | 4 | "Suitable for me" part 1 (`PRODUCT.md`); Segment 2; the two groups follow `refs/lifesum_and.png`, which splits food preferences from allergies |
| F2 | Filter chip · macro match | 4 | "Suitable for me" part 2; Segment 3. *Screens, IA 4:* the macro mode is built from I2 number fields instead, because IA 4 asks for an editable numeric range, not a fixed set of choices. F2 stays specified for a later preset row (**flagged:** an anticipated use that IA 4 did not need) |
| F3 | Mode switch · *Screens, IA 2:* a `tablist` (A7); text labels, icon-only under `bp-screen-narrow` (A8) · *Screens, IA 4:* second use, the two filter modes, with new `i-tag` and `i-target` glyphs for the icon-only state · **only the selected tab carries `aria-controls`**, pointing at its panel; unselected tabs carry none, so there's never a dangling reference (a Stage 5b audit fix — IA 4 revision 1 put `aria-controls` on both tabs, which is wrong since only one panel exists at a time) | 2, 4 | IA 2 method switcher; IA 4 two filter modes. **Judgment call:** not in the requested v1 list, added because two of five screens need the same control |
| I1 | Search field | 2 | IA 2 Search mode; P0 #1 |
| I2 | Number field with unit · *Screens, IA 4:* in use, four fields in a `.field-pair` grid (kcal, protein, carbs, fat), pre-filled from saved targets; the pair stacks under `bp-screen-compact` | 4 | IA 4 macro-target values, editable per search |
| I3 | Portion control (stepper + unit) · *Screens, IA 3:* `.portion-wrap` puts the J2 helper line directly above it; `.stepper-static` wraps its unit word below the stepper at 200% zoom · *after the IA 5 critique:* the step buttons are named for the **direction, not the increment** (the servings step is 0.5, so “One serving more” was false) · **one contract, set by the Stage 5b cross-screen audit and live on both screens:** the field is `role="spinbutton"` carrying `aria-valuenow` / `aria-valuemax` / `aria-valuetext` (kept in step as the unit changes; no `aria-valuemin` is set, since no screen enforces a floor — left standing, see below); the ceiling belongs to the *unit*, carried in each screen's own portion data — a count caps at 99, a weight or volume at 5,000 (before the fix, IA 3 used one ceiling for every unit alike, so 5,000 "servings" rendered as 650,000 kcal); arrow keys step the value on **both** screens; the authored state restores on load | 3, 5 | IA 3 editable portion (Cronometer serving-size friction); IA 5 serving count. The ARIA/keyboard pattern shipped on IA 5 first and was backfilled onto IA 3 by the audit — **both screens carry it now**, not "IA 5 now, IA 1–3 in v2" as v1 first planned |
| S1 | Screen scaffold (header, body, safe-area insets) · *added at Screens* | all | Stage 4 carry item "safe-area insets"; §3.2 section rhythm. The context line under the title is a **judgment call** |
| S2 | Bottom bar (Today tab · Add food · Recipes tab) · *added at Screens* | 1, 4 | IA structural rule 1; IA Flow 2 "tap Recipes in navigation"; Principle 1; Segment 1 one-handed use. **Judgment call:** placing the action inside the navigation bar. *Resolved:* IA 2, 3 and 5 are task/step screens and use the S1 task or step header with S3 instead, the same pattern IA 2 set — not an open question, as v1 first left it |
| S1 · media band | `.screen-media`: a full-width element between the header and the body, outside the `inset-screen` gutter · *added at Screens, IA 5* | 5 | IA 5 lists an image as recipe content. Full width is right for a detail screen and wrong for a results list (IA 4's critique), because there is one picture and nothing to compare it against |
| S1 · task header | Title row with one dismiss action (B3 "Close"); a body with no bar below it clears the bottom safe area; `.panel` for tab panels · *added at Screens, IA 2* · *IA 3:* step header (B3 "Back" with `i-chev-left` above the title) and head with media (`.screen-head-media`, the Flow 3 thumbnail beside the title); `.screen-head-row` wraps when its two items don’t fit | 2, 3 | IA 2 is a task opened from S2's action, so it closes back to where it came from. **Judgment call:** a closing task screen without the bottom bar |
| S3 | Action bar (one or two full-width buttons, sticky at the bottom, safe-area aware) · *added at Screens, IA 2* | 2, 3, 5 | Segment 1 one-handed use (thumb reach); IA 3 "Log it" and IA 5 "Log this" reuse it. Same surface and hairline as S2, no shadow. *IA 3:* two buttons stack with the primary last, so B1 never moves; a destructive action never goes in the bar (“Remove entry” sits at the top end of the S1 header, opposite “Cancel”) |
| V1 | Viewfinder (camera area + framing guide; instruction below, never over the feed) · *added at Screens, IA 2* · *after critique:* `.found` state (closed frame + "Found: …" status line), corners capped at 25% of the guide | 2 | IA 2 Barcode and Photo modes; hybrid §7 "only the camera viewfinder" on logging screens. Guide shape per mode (`ratio-guide-*`). Found state: barcode "pulls up the wrong food" (reviews), heuristic 1 |
| M1 | Recipe image (`.rimg`; `.thumb` at `size-thumb`, `.hero` full width, both at `ratio-recipe-image`) · *added at Screens, IA 3 as a striped “IMAGE · UNVALIDATED (§7)” placeholder* · *IA 5:* `.hero` in S1's `.screen-media` band · **filled with real images at the Stage 7 Krea pass**, which replaced the stripes and retired the label. One 4:3 source per dish, `object-fit:cover` at every size — the crop belongs to the component, not the file. `alt=""`: the dish is named in text beside every slot | 3, 4, 5 | Hybrid §3 (a thumbnail keeps a recipe’s identity on IA 3) and §7 (no text or figures over the image) |
| R1 | **Ingredient list** · *added at Screens, IA 5:* a quantity column in `figure-md` (tabular, so it lines up) beside the ingredient in `ui-body`, in a C1 paper block with C2's hairlines. `.ing-none` holds the column for an ingredient with nothing to measure | 5 | IA 5 "ingredients" as recipe content; L1 — a quantity is a figure, so it takes the figure treatment |
| R2 | **Method steps** · *added at Screens, IA 5:* an `<ol>` on `surface-ground`, numbered by a CSS counter in `ui-secondary-strong` (tabular, but **not** a figure role: a step number is a position, not a measurement) | 5 | IA 5 "steps"; `voice-heading` was reserved in v1 for "recipe section heads (Ingredients, Method)" — this is what those heads name. R1 on Paper and R2 on Oat are L3's emphasis dial at the scale of a section |
| E1 | Message (no-result state: title quoting the query, next-step text, action in S3; `role="status"`, no hue) · *added after the Add Food critique* · *Screens, IA 4:* reused for "no recipe matches". **Rule added:** where a screen has S2 rather than S3 (a navigation destination, not a task), the next-step action sits inside the message instead of the bar | 2, 4 | IA structural rule 2 ("never dead-ends") applied to logging and to filtering; critique P1. Full error/empty states stay v2 |

S1 and S2 were added when IA 1 (Today) was built, before the screen itself, per the rule that screens never style anything locally. They use existing tokens only; the one new glyph is `i-today`.

---

## 7. Remaining backlog

- ~~**Interaction states** for every component: hover, pressed, focus rendering (the `focus-ring` token exists), disabled, loading.~~ *Done at Stage 6, §10, for buttons, chips/mode switch, inputs and the stepper.* Still deferred for cards (C2, C3) and the nutrition components (N1–N4), and empty states beyond E1.
- ~~**Error states**, and whether an error color is needed at all (never reused for over-target, J1).~~ *Resolved at Stage 6, §10.4:* yes, for I2 and I3 — `color-error`, distinct from J1's over-target and from Terracotta.
Struck items are done, with the stage that closed them. The rest is genuinely open.

- **Elevation.** v1 separates blocks by spacing and hairlines (Stage 3 note on 1.15:1 card edges). A sticky bottom action bar on IA 3/5 may need one shadow token. *Screens, IA 1:* the S2 bottom bar is sticky and separated by a hairline only; add a shadow token only if screens show that edge gets lost.
- **Motion** beyond the loading spinner (for example, results updating in place on IA 4). *Stage 6 took one narrow, functional exception — a loading spinner, §10.5 — everything else here is still deferred.*
- ~~**Camera-mode UI** for Barcode/Photo~~ *Done at Screens (Stage 5), IA 2:* V1 viewfinder, and the capture button is B1 "Take photo" in S3. *Stage 6, §10.3:* a mode segment can now render disabled (e.g. no camera permission). **Still open:** the full camera-permission flow, "no barcode found" and live detection feedback.
- ~~**Imagery tokens** (grade, final crops).~~ **Resolved at the Stage 7 Krea pass.** `ratio-recipe-image` (4:3) is confirmed, not provisional: audit A9 is closed. No grade token was added — the warm, low-saturation grade of hybrid §7 lives in the images themselves, not in CSS, so there is nothing for a token to hold.
- **Dark mode:** open, and not planned for this deliverable. The brand commits to one light, warm look.
- ~~**A clickable prototype.**~~ *Done at Stage 8 / 8b:* `06-prototype/`, one canonical frame per screen, both flows wired, audited 18/20. It carries this system's CSS unchanged.

---

## 8. Additions and refinements vs. Stage 3 (reflected back)

| Change | Kind | Recorded in |
|---|---|---|
| **Stage 7 (Krea imagery pass): M1 becomes a real image component.** `.img-ph` (135° stripes + the “IMAGE · UNVALIDATED (§7)” label) becomes **`.rimg`**, an image box with `object-fit:cover` over a `surface-sunken` fill that shows only before load; `.img-ph-label` and `size-placeholder-stripe` are retired. Ten AI-generated dish images fill all 16 slots across IA 3, 4 and 5, one 4:3 source per dish shared across every size. **Audit A9 is closed:** the shared `ratio-recipe-image` crop holds at both rendered sizes. **No new tokens and no new colors** — and no grade token, because hybrid §7's warm, low-saturation grade lives in the images, not in CSS. `alt=""` throughout: every slot is beside the dish's name in text | Addition (the imagery pass the standing rule deferred; A9 resolved) | This doc §6 M1, §7, §8; `components-v1.html` M1, C3; `CLAUDE.md` Stage 7; `assets/images/` |
| Screens, IA 4 (Recipes & Filter): C3's image slot becomes an M1 placeholder (its spec already said so), plus `.rcards` and `.rcard-link`; the F filter group (`.filters`, `.filter-panel`, `.fgroup`); `.field-pair` stacks under `bp-screen-compact`; `i-tag` and `i-target` glyphs; E1's "action in S3" rule extended to screens that have S2 instead. **No new tokens and no new colors** — the screen is the first to use `gap-section-recipe` (40), the recipe half of the emphasis dial | Addition (needed by IA 4; B3's anticipated use confirmed) | This doc §6; `components-v1.html` C3, F, I2, E1 |
| Screens, IA 4 revision 2 (critique 23/40, 2 P1 fixed): **`.rcard.compact`** replaces the full-bleed C3 layout (card 398→210 px, so results are comparable without scrolling); **`.list-head`** (label + the one control that acts on the list) holds B3 renamed to **"Reset to my usual"**; a filter-mode switch now tunes criteria without dropping any (macro mode stays vegetarian and shellfish-free, closing a real cross-mode contradiction); results sort **best fit first**; a card reports its two tightest margins; `.matches` gets a mode-dependent `aria-label` ("Also suits" / "Closest to your limits"); F3's dangling `aria-controls` is fixed to name a panel from the selected tab only. **No new tokens and no new colors** | Refinement (critique P1–P2; Stage 5b audit) | This doc §6 C1, C3, F3; `components-v1.html` C1, C3, F3; `05-screens/04-recipes-filter.html` notes |
| Screens, IA 3 (Food Confirmation): M1 image placeholder with `size-thumb`, `ratio-recipe-image` (now also used by C3) and `size-placeholder-stripe`; S1 step header (B3 “Back”, `i-chev-left`) and head with media; B3 `.btn-flush`; I3 `.portion-wrap`; S3 stacking rule (primary last, nothing destructive in the bar); N2 label by context. **Stage 3 unchanged:** no new color, and the placeholder uses existing surfaces | Addition (needed by IA 3) | This doc §1.2, §3.3, §6, §7; `components-v1.html` B, C3, M1, N2, I3, S1, S3 |
| Screens, IA 2 after one critique (24/40): E1 message; V1 `.found` state and corners capped at 25%; C2 search results name the shared source once in an `aria-live` list label, with the serving alone in the meta line. No new tokens | Refinement (critique P1–P2) | This doc §6; `components-v1.html` C2, V1, E1; `05-screens/02-add-food.html` notes |
| Screens, IA 2 (Add Food): F3 becomes a `tablist` (A7) with text labels, icon-only under `bp-screen-narrow` (A8); S1 task header, `.panel`, `.fill`, body column `minmax(0,1fr)`; S3 action bar; V1 viewfinder with `surface-viewfinder`, `line-guide`, `stroke-guide`, `size-viewfinder-min`, `size-guide-corner`, `ratio-guide-barcode` / `ratio-guide-photo`; B2 and B3 in real use; `.btn` centres a wrapped label. **Stage 3 unchanged:** Ink as the camera surface uses an existing palette color for the one area hybrid §7 allows on logging screens, so the stylescape needs no change | Addition (needed by IA 2; A7/A8 resolved) | This doc §1.2, §3.3–3.4, §6, §7; `components-v1.html` F3, S1, S3, V1; `audit-v1.md` §6 |
| Screens, IA 2: `voice-title` also covers Add Food's screen title, so the role now lists IA 1, 2, 3, 4. **Reconciliation, not a new decision:** the title shipped at IA 2 and was allowed by §2.3 rule 3 (at most one serif element per logging screen), but `02-hybrid-direction.md` §3's dial table still read "None" for Screen 2. A cross-screen audit of the finished set caught the disagreement; it is resolved in favour of the shipped element, because a screen title is identity rather than decoration and Add Food is the one screen entered as a modal task | Reconciliation (binding documents disagreed) | `02-hybrid-direction.md` §3, with the reasoning recorded there; this doc §2.2 |
| `color-stone` added as a control-edge neutral | Addition (functional, WCAG 1.4.11) | `02-hybrid-direction.md` §4; stylescape unchanged (not a brand color) |
| `color-oat-deep` formalized from stylescape CSS | Formalization | `02-hybrid-direction.md` §4 |
| Selected chip labels in Ink, not Pine (selection shown by fill + line + check) | Refinement to keep L1 inside chips | `02-hybrid-direction.md` §4 |
| Status colors: none in v1; over-target handled by J1 | Resolves hybrid §4 rule 4 | `02-hybrid-direction.md` §4, `PRODUCT.md` |
| AI-photo estimate display: J2 | Resolves a `PRODUCT.md` open item | `PRODUCT.md` |
| Type anchors resolved to single values | Formalization within the Stage 3 ranges | This doc §2.2 |
| Screens typeset pass (C2 meta line): three roles instead of one. Source first (N4 icon + `ui-secondary-strong` · `text-primary`); amount as a figure (`figure-sm` + unit style); time last (`ui-secondary` · `text-secondary`); "amount · time" wraps as one unit. N4 text moves to `text-primary`. **No new token:** a `text-source` alias was considered and rejected, because it would only rename Ink | Refinement (J2 legibility; L1 amount as a figure; `text-secondary` "never for anything the user must read to act") | This doc §1.2, §2.3, §5 J2, §6; `components-v1.html` C2, N4, color table |
| Screens, IA 1 revision after critique: `type-unit-hero-strong`, `type-unit-sm-strong`, `meter-target` (replacing the short-lived `size-overflow-min`), `bp-screen-narrow` / `bp-screen-compact`; C2 `.row-link` and meta segments; N3 without overline and with "left / over" macro lines; the hero unit may wrap; `i-chev-right` glyph | Refinement (J1 revisit condition met; critique R1–R5) | This doc §1.3, §2.2–2.3, §3.3, §5 J1, §6; `components-v1.html` C2, N3, S1, S2, J1 |
| Screens, IA 1: S1 screen scaffold, S2 bottom bar, C1 list label, `inset-safe-top/bottom`, `i-today` glyph; `ui-chip` roles also label tabs | Addition (needed by the first screen; existing tokens only) | This doc §2.2, §3.3, §6; `components-v1.html` §10 |
| Audit v1: `--type-*` role tokens, `stroke-*` group, `size-icon-sm`, `size-stepper-value`, `size-separator`, `size-hatch-period` added; `ui-chip` 15 → 14 px; hatch period 5 → 6 px | Formalization of previously hardcoded values | This doc §2.2, §3.3–3.4; [`audit-v1.md`](audit-v1.md) |
| **Stage 5b, cross-screen audit (all 5 screens complete):** B1, B2, B3 confirmed and reconciled to shipped copy (B1 gains "Log this · ‹n› servings" and "Save changes"; B2's "Retake photo" placed on IA 3, not the IA 2 "anticipated" stage v1 first drafted; B3's "Reset to my targets" corrected to "Reset to my usual", and its Close/Back/Cancel/Remove entry/Search instead uses are enumerated). I3 gets **one contract**: the ceiling belongs to the unit (count 99, weight/volume 5,000, previously one ceiling for every unit), `role="spinbutton"` + `aria-valuenow`/`aria-valuemax`/`aria-valuetext` and arrow-key stepping are live on **both** IA 3 and IA 5 (not "IA 5 now, IA 1–3 in v2"), and authored state restores on load. F3 gains the rule that only the selected tab carries `aria-controls`. Nine clock values were resynced so Flow 3 no longer runs backwards in time (presentation-layer only, no token change). **No new tokens, sizes or colors** — this row is reconciliation, not addition | Reconciliation (verification pass found the docs describing an earlier revision than what shipped) | This doc §6 B1–B3, F3, I3; `components-v1.html` same; `CLAUDE.md` Stage 5b |
| **Stage 6 (interaction states), after Stage 5b:** `color-error` (Material 3's error role, checked directly; 4.95–6.43:1 on Paper/Oat/Oat Deep) and `state-error`, used only on I2 and I3, distinct from J1's over-target and never applied to a figure (L1 extended); `state-hover-opacity` (8%) / `state-pressed-opacity` (12%) state layers (Material 3 convention, checked directly) for B1–B3, F1–F3 and I3, gated to `@media (hover:hover)` for hover only; disabled reuses the existing `surface-sunken` + `text-secondary` pair (§1.4, 4.82:1) rather than a new opacity token, applied to buttons, chips, the mode switch and the stepper's ± at its own floor/ceiling; a loading state for B1 and I1 only (nothing else in this system has anything asynchronous to wait on); `scroll-clear-bottom` closing a WCAG 2.2 SC 2.4.11 gap (a sticky S2/S3 bar could obscure a focused row/card). New glyph `i-error`. **No change to any existing token's value or to J1.** Full reasoning in this doc's new §10 | Addition (screen notes + Stage 5b audit both flagged these gaps) | This doc §10; `components-v1.html` §11 |

---

## 9. Traceability summary

| Decision | Type | Source |
|---|---|---|
| Two-tier tokens; components use semantic only | Structural (system mechanism) | L3 (hybrid §2); `PRODUCT.md` Principle 5 "Systemic, not screen-by-screen" |
| `stone` control edge | Functional | WCAG 1.4.11; measured contrast · shade *(aesthetic judgment)* |
| Meter tracks on Oat, not Oat Deep | Functional | Measured contrast (Ochre 2.91:1 on Oat Deep) |
| Selection = fill + line + check, label in Ink | Functional | L1; color never the only carrier (hybrid §4 rule 2) |
| Type role values | Aesthetic within Stage 3 anchors | Hybrid §5 · *(aesthetic judgment)* |
| Input text ≥ 16 px | Functional | iOS focus-zoom behavior; cross-platform decision |
| 4 px spacing base | Functional | Cross-platform grid (`CLAUDE.md` Platform decision) |
| Logging 24 / recipe 40 section rhythm | Aesthetic, tone-grounded | Emphasis dial (hybrid §3); H1 vs Stage 3 "generous recipe spacing" |
| 48 px minimum hit target | Functional | `PRODUCT.md` touch-target convention; chips and segments reach it with an invisible `::after` (verified in `audit-v1.md`) |
| Shape follows role (pills choose, rectangles act) | Aesthetic, functional intent | *(aesthetic judgment)* |
| J1 over-target: no hue, word + hatch | Tone | **Judgment call:** `PRODUCT.md` users gain and lose; stylescape "no guilt trips"; hybrid §4 rule 3; L1 |
| J2 photo estimate: exact figures, source note, helper line | Tone + structure | **Judgment call:** Cal AI accuracy complaints and "transparency about confidence" (`01-secondary-research.md`); H2; Stage 3 copy guardrail; L1 |
| Mode switch added to v1 set | Structural | IA 2 + IA 4 · **Judgment call** (scope) |
| Secondary and text buttons | Structural | **Judgment call:** anticipated IA 2 / IA 4 uses |
| Hover/pressed as low-opacity state layers | Aesthetic, pattern-grounded | Material 3's state-layer convention, checked directly (Stage 4 carry-forward rule); exact opacities *(aesthetic judgment)* |
| Disabled = `surface-sunken` + `text-secondary`, not a fourth opacity token | Functional | Reuses the pair §1.4 already measured (4.82:1); WCAG 2.2 1.4.11's note exempts disabled controls from any minimum, so this exceeds what's required |
| `color-error` added, distinct from J1 and from Terracotta | Functional | Closes the "invalid amount" gaps IA 3/5 left standing (`05-screens` notes); §5 J1 itself reserved this ("a true error color... must never be reused for over-target"); Material 3's error role, checked directly; measured 4.95–6.43:1 |
| An out-of-range figure stays Ink, never tinted red | Functional | L1, extended the same way J2 kept a photo estimate exact in form |
| Loading limited to B1 and I1 | Functional | No other component in this system has anything asynchronous to wait on; not fabricated for symmetry |
| `scroll-clear-bottom` for sticky S2/S3 bars | Functional | WCAG 2.2 SC 2.4.11 (Focus Not Obscured, Minimum) — new in 2.2, found by checking the sticky-bar geometry directly against it |
| Stepper ± disables at the unit's own floor/ceiling | Functional | Closes a Stage 5b / Recipe Detail left-standing item ("no floor signal, no ceiling relative to the yield") |

---

## 10. Interaction states — added Stage 6

**Scope.** All five screens are built and the Stage 5b cross-screen audit passed. This pass adds hover, pressed, disabled, error and loading to the four component groups the screen notes and the audit actually flagged as missing them: **buttons (B1–B3), chips and the mode switch (F1–F3, which share the same chip mechanics), inputs (I1–I2) and the stepper (I3).** Everything else in §6 — cards, the nutrition components, the screen shell — stays default-state only; extending states there is unopened backlog, not a decision made here.

**Method.** Same as the rest of this doc: components use semantic tokens only, no raw values, and every new color is measured against the same three surfaces §1.4 already uses (Paper, Oat, Oat Deep). Rendered in `components-v1.html` §11, which doubles as the reference: hover and pressed are real `:hover` / `:active` CSS, checkable by pointing at any button, chip or mode segment already on that page; disabled, error and loading are shown as explicit markup, since a screenshot can't fake a pseudo-class-free state.

### 10.1 New tokens

| Token | Value | Tier | Used for |
|---|---|---|---|
| `state-hover-opacity` | 8% | Semantic | Hover overlay strength (pointer devices only) |
| `state-pressed-opacity` | 12% | Semantic | Pressed/active overlay strength |
| `color-error` | `#B3261E` | Primitive | The one new color this pass adds |
| `state-error` | → `color-error` | Semantic | Invalid-field border, error icon, error text |
| `scroll-clear-bottom` | `size-button × 2 + space-8 + inset-safe-bottom` | Semantic sizing | `scroll-margin-block` on rows/cards, so a sticky S2/S3 bar can't obscure a focused one |

No new radius, stroke, or type token was needed — states reuse the existing scale end to end.

### 10.2 Hover and pressed — state layers

**Decision: a low-opacity overlay in the control's own foreground color, over its resting fill or track.** This is Material 3's state-layer convention, checked directly against Material 3 per the Stage 4 carry-forward rule ("keep checking mobile standards directly against Apple HIG, Material 3 and WCAG 2.2"). The exact opacities (8% hover, 12% pressed) are a designer's pick within that convention *(aesthetic judgment)* — Material 3 documents the same pattern at similar values, and 8%/12% measured comfortably inside AA on every fill this system has (§10.6 has the numbers).

- **Filled controls** (B1 primary, a selected chip/segment): overlay tinted with the label's own color (`text-on-action` on Pine, `text-primary`/`text-action` on Pine Light), so pressing a dark fill lightens it very slightly rather than darkening toward black — there's no black in this palette, and there shouldn't be one for this.
- **Unfilled controls** (B2/B3, unselected chips/segments, stepper ± buttons, fields): overlay tinted with `text-primary` or `text-action`, over `surface-paper` or `transparent` (which lets whatever track color is underneath show through).
- **Hover is gated to `@media (hover:hover)`.** A touchscreen has no hover, and without this gate a tapped element can get "stuck" showing its hover state until the next unrelated tap — a well-known mobile-web defect this system's own target platform (`PRODUCT.md`: iOS + Android) would hit immediately. **Pressed is not gated:** `:active` fires from a touch as well as a pointer, so it still gives touch its own feedback.
- **Fields** get hover on the edge only (`line-control` tinted), not a fill change — a filled hover would visually compete with the existing `:focus-within` ring for the same "something is happening here" signal, and a field's most important state is focus, not hover.

**Rejected:** a fixed hover/pressed hex per component (would multiply into a second, untracked palette the moment a new component needed one); darkening toward black (off-palette, and this system has never mixed toward black); no hover at all on touch-first products (rejected because trackpads and styluses do send real hover events, and `@media (hover:hover)` already handles the touch case correctly without giving up the desktop/prototype-review affordance).

### 10.3 Disabled

**Decision: the same neutral pair on every component — `surface-sunken` fill (or an unchanged Paper fill with the outline dropped, for outline-only controls) and `text-secondary` label/value — not a new opacity token.**

This was the one place this pass deliberately checked a WCAG figure and found there isn't one: **SC 1.4.11's own note explicitly exempts inactive/disabled user interface components from any contrast requirement.** "Nothing in this Success Criterion requires content to be displayed when it is not in use, or requires the association of any specific styling or contrast requirement with a state such as disabled." So there is no WCAG 2.2 disabled-contrast minimum to cite — the honest finding is that one doesn't exist, not a number to meet.

Two disabled recipes were measured and compared:
- **A uniform opacity fade** (e.g. the whole control at 40%, composited over its background): measured at **2.05:1** label-vs-fill — legible, but so faint it reads as broken rather than intentionally inactive, and it would have needed a new token (`state-disabled-opacity`) purely to produce a worse result.
- **The neutral pair actually shipped** (Ink Soft on Oat Deep): this is the exact pair §1.4 already measured at **4.82:1** for secondary text — it clears AA text contrast, which the disabled state was never required to do. Reusing an already-audited pair rather than inventing a new one keeps the token count down and the result more legible, not less.

Applied to: B1/B2/B3, chips (provisioned; no current IA screen needs one, the same place B2/B3 started), the mode switch (one evidenced case: a Barcode/Photo tab with no camera permission — the *affordance* now exists even though the permission-request flow itself is still v2, per the Add Food carry notes), fields, and the stepper's ± buttons at their own floor/ceiling.

### 10.4 Error

**Decision: a new primitive, `color-error` (`#B3261E`), used only for I2 number fields and the I3 stepper — never reused for J1's over-target, and never applied to the figure itself.**

**Why a new color was warranted now, when v1 explicitly deferred it:** §5's J1 write-up already reserved this move — "a true error color (a failed scan, say) is a v2 question and must never be reused for over-target." An invalid typed amount is exactly that kind of true error (a value the system cannot act on), which is a different category from over-target (a value the system can act on and simply reports). J1's "no alarm hues" rule is about over-target specifically, not a blanket ban on ever having an error color.

**Why this hex, and why it's safe next to Terracotta.** `#B3261E` is Material 3's own error-role color — checked directly, the same way this doc checks Material 3 and HIG elsewhere. It reads as a true red, distinct from Terracotta's rust-orange protein mark (`#B0513A`) by hue, not just by context, so a user skimming quickly can't mistake one for the other. Measured (same method as §1.4):

| Pair | Ratio | Verdict |
|---|---|---|
| Error on Paper | 6.43 | Text/icon ✓ AA |
| Error on Oat | 5.61 | Text/icon ✓ AA |
| Error on Oat Deep | 4.95 | Text/icon ✓ AA (the weakest surface it can appear on, still clears 4.5) |

Non-text use (the field/stepper border) only needs 3:1 against the adjacent fill — comfortably clear at every ratio above.

**The figure itself is never tinted.** L1 ("figures are never tinted, faded or italic") already covered this for J2's photo estimates; this pass treats an out-of-range number the identical way. The border, an icon (`i-error`, added to the glyph set) and a short text message carry the error — the number stays Ink, tabular, unchanged in form, exactly like a photo estimate stays exact in form while a Source note carries its own uncertainty in words. This also satisfies **WCAG 2.2 SC 3.3.1 (Error Identification)**: the problem is named in text, not signaled by color alone.

**What this closes.** Both `05-screens/03-food-confirmation.html` and `05-screens/05-recipe-detail.html` left "an invalid amount reverts silently" standing as a v2 item, and the Stage 5b audit's own fix for the stepper's unit-based ceiling (a count capped at 99, a weight/volume at 5,000) had no way to explain *why* a typed 5,000 "servings" wouldn't be accepted — it just reverted. The error state now says so, using the audit's own example as the specimen in `components-v1.html` §11.

**Not applied to I1 (search) or chips.** A search field has nothing to validate — any text is a valid query, even one with no results (that's E1's job, not an error state). A chip is a value toggle with no invalid value.

### 10.5 Loading

**Decision: B1 (primary button) and I1 (search field) only.** Loading means "a request is in flight, wait" — every other component in this system resolves instantly against local state (a chip toggles, a stepper steps, a mode switch swaps a panel already in memory), so giving them a loading state would be inventing a wait that doesn't exist anywhere in the IA.

- **B1:** the label is hidden (`visibility`, not removed) and a spinner takes its place at the same size, so the button never changes width or height — the same "nothing reflows" principle N2/N3 already apply to figures. `aria-disabled` stops a second tap. **Corrected claim:** the accessible name *does* change mid-action — `visibility:hidden` excludes `.btn-label`'s text from accessible-name computation (per the AccName spec), while the `.spinner`'s `sr-only` text does not, so the button's computed name resolves from "Log it" to "Logging…" while loading. That's the intended behavior, not a defect: a screen reader user who lands on the button while it's loading hears what's actually true ("Logging…"), once, rather than a stale "Log it".
- **`.btn-label` layout, added at Propagation.** §11’s specimen wrapped a one-word label, so `.btn-label` needed no layout of its own. The first real screen to take the hook — Recipe Detail’s “Log this · 1.5 servings” (three elements, the serving count live) — showed the gap: `.is-loading` hides `.btn-label`, so a multi-part label has to be **one** element, and collapsing three flex children of `.btn` into a plain span would have dropped the `gap-inline` between them. `.btn-label` now carries `.btn`’s own row layout (same gap, same centring), so wrapping an existing label changes nothing at rest — verified by measuring every B1 before and after. No new token.
- **I1:** the spinner replaces the leading search icon in place while results are being fetched; the results list carries `aria-busy="true"` so a screen reader doesn't read a stale count while new results are still arriving.
- **Motion, revisited.** §7 defers "motion" broadly (e.g. IA 4's results updating in place). A loading spinner is the one narrow exception this pass takes: it isn't decorative, it's the only way to convey "in progress" to a sighted user without words repeating every frame, and it already respects `prefers-reduced-motion` (slowed, not removed, mirroring how this file's own reference-page chrome already gates `scroll-behavior:smooth` the same way). This is not a general license to add motion elsewhere — every other deferred motion item in §7 stays deferred.

### 10.6 Focus, finalized

The `focus-ring` token (Pine) and its rendering were already **substantially** in place before this pass — most interactive elements already had a visible `:focus-visible` outline. What this pass did was check that rendering against WCAG 2.2 directly, as asked, rather than assume it was sufficient:

- **SC 2.4.7 Focus Visible (AA, required):** pass. Every focusable control already had a rule.
- **SC 2.4.13 Focus Appearance (AAA, not required for this system's AA target, checked anyway):** the existing 2 px outline at a 2 px offset already meets its minimum thickness/area, and Pine's contrast against every surface it appears on (6.59–8.56:1, §1.4) clears its 3:1 minimum with room to spare. No change needed.
- **SC 2.4.11 Focus Not Obscured, Minimum (AA, new in 2.2) — the one real gap this check found.** S2 and S3 are `position: sticky`. A keyboard user tabbing through a long ledger (Today) or ingredient/recipe list, with a sticky bar at the bottom, can land on a focused row or card that the bar visually covers, even though the browser scrolled it "into view." **Fix:** `scroll-margin-block: scroll-clear-bottom` on `.row-link` and `.rcard-link`, sized to the tallest bar this system has (two stacked S3 buttons, Food Confirmation's edit state) so a single-button bar just gets a little extra headroom rather than needing its own measurement.
- **SC 1.4.11, disabled controls:** see §10.3 — there is no minimum to check, and that finding is itself the citation.

### 10.7 Not covered by this pass

Left open, as listed in §7: elevation, broader motion (results updating in place, camera-mode transitions), empty states beyond E1, camera **permission** flow (only the disabled-tab *affordance* shipped here), a full error/empty treatment for cards and the nutrition components, and dark mode. Hover/pressed were not extended to C2 ledger rows or C3 recipe cards in this pass, even though both are already tappable links with their own focus rings — that's additional surface area the user's scope for this pass (buttons, chips, inputs, the stepper) didn't ask for, flagged here rather than silently extended.

### 10.8 Self-check (in place of a full audit)

Run once, at the end of this pass, per instruction — not a second `/impeccable` pass:
- **Contrast:** `color-error` measured 4.95–6.43:1 across Paper/Oat/Oat Deep (§10.4), all ≥ AA text (4.5:1) and well past the 3:1 non-text minimum. Disabled reuses the existing 4.82:1 pair (§10.3). Hover/pressed overlays were spot-checked on the Pine fill (8%→6.85:1, 12%→6.14:1 label contrast, both still ≥ AA) and don't drop any existing pair below its measured ratio in §1.4.
- **No raw values:** every new rule reads a token (`state-hover-opacity`, `state-pressed-opacity`, `state-error`, `scroll-clear-bottom`) or composes existing ones via `color-mix()`/`calc()`; no bare hex, px, or opacity number was written into a component rule outside the `:root` block.
- **No off-palette colors besides the one flagged addition:** `color-error` is the only new primitive; hover/pressed introduce no new colors at all, only mixes of colors already in the palette.
- **L1 held:** no figure (a typed amount, a target, a percentage) changes color in any new state — disabled, error and loading all carry their signal in the container, an icon, or text, never in the number.
