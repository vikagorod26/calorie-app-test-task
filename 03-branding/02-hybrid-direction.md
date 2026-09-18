# Hybrid Direction — The Measured Kitchen

**Stage:** 3 · Branding — *direction definition* (concept, unifying rule, palette, typography rule).
**Not in this doc:** the stylescape / visual presentation, components, full type scale, and screens. Those are the next steps.
**Builds on:** [`01-direction-options.md`](01-direction-options.md) (A · Clinical Ledger + B · Oat & Serif). Direction C is excluded, see §6.

**How to read the citations** (per the standing traceability rule in `CLAUDE.md`):
- **Structural/functional choices** cite the brief (`CLAUDE.md`), [`PRODUCT.md`](../PRODUCT.md), [`01-research/`](../01-research/) or [`02-information-architecture/information-architecture.md`](../02-information-architecture/information-architecture.md).
- **Aesthetic choices** are grounded in audience/tone and marked *(aesthetic judgment)* where the specific value is a designer's pick.
- Anything neither evidenced nor purely aesthetic is flagged **Judgment call**.

---

## 1. Concept

**The Measured Kitchen** is a warm, cookbook-like place where every number is kept like a ledger. The whole app shares one oat-and-paper ground, one pine action color and one type system. What changes between logging and recipes is **emphasis**: which of those shared elements leads on a given screen. Logging screens are led by figures, so they read like A. Recipe screens are led by words and images, so they read like B. A calorie figure looks identical in both.

**Why a hybrid at all.** The side-by-side in `01-direction-options.md` showed no single reference direction serves both user stories. A is strongest for trust in numbers (H2) and B is strongest for recipe discovery (H3). `PRODUCT.md` Principle #1 says "both stories are first-class", so dropping either strength would demote one story.

---

## 2. The unifying rule — *"Words are warm, figures are exact."*

One sentence that decides every styling question in the system:

> **Human language gets warmth. Nutrition figures get precision. Both always sit on the same ground, in the same palette.**

It breaks into three laws.

| # | Law | What it means in practice | Grounded in |
|---|---|---|---|
| **L1** | **A figure is always a figure.** | Every calorie/macro value (on Today, in search results, on the confirmation screen, on a recipe card, in a recipe's nutrition panel) uses the *same* treatment: sans, tabular lining figures, ink color, unit always attached ("412 kcal", "32 g"), right-aligned when in a list. Never serif, never tinted, never decorative. | **H2** (`04-conclusions.md`): trust depends on the accuracy of the logging method. Numbers must never read as approximate, and B's documented con was exactly that. A's ledger alignment is the pattern that made figures checkable (MFP food log reference). |
| **L2** | **Warmth lives in words, ground and images, never in the data.** | The serif, the oat ground and food photography carry the cookbook tone. They frame data but never restyle it. | **H3 / Segment 2** (`02-audience-5w.md`): home cooks want "confidence *before* cooking", in planning moments, which suits B's editorial tone. L2 keeps that tone from leaking into figures (H2). |
| **L3** | **Context changes emphasis, not tokens.** | Logging and recipe screens use the identical palette, type families and components. They differ only in *proportion*: how much serif, how much image, how large the figures (the dial in §3). A recipe's nutrition strip and a log entry's nutrition strip are the same component. | **H4** (`04-conclusions.md`) and **IA Flow 3**: a recipe "re-enters Story 1's logging flow through the one screen every other logging method already uses". The visual system mirrors that structure. If the recipe section had its own palette, the handoff would *look* like crossing into a different product. |

**Why this rule and not a split palette** *(Judgment call on the mechanism, evidenced goal)*: the requirement that the recipe→log handoff feel like one continuous flow is evidenced (H4, Segment 3's job story: "log it with the same accuracy I planned it with"). Choosing *typographic role + emphasis ratio* as the way to achieve it is a designer's call. Another valid mechanism exists (e.g., one palette with a section tint), but a section tint would visually separate exactly the two flows H4 says should feel joined.

---

## 3. The emphasis dial — per IA screen

The five screens from `information-architecture.md`, placed on one dial from **Ledger** (A-led) to **Cookbook** (B-led). Every row uses the same tokens (§4) and type roles (§5).

| IA screen | Dial position | Serif use | Figures | Imagery | Why here |
|---|---|---|---|---|---|
| **1 · Today / Daily Log** | Ledger ●○○○ | Screen title only (e.g. the day) | **Hero figure** for remaining kcal, then aligned figure column per entry | None | H1: glance in one-handed moments. Segment 1 checks "that number against a running daily budget" (`02-audience-5w.md`). |
| **2 · Add Food** | Ledger ●○○○ | Screen title only | Kcal/serving on every result row | Camera viewfinder only (functional) | H1 plus the Cronometer "too many steps" finding. This is the most task-focused screen, so nothing decorative *beyond the title* — and a title is identity, not decoration (see the note below). |
| **3 · Food Confirmation & Log** | Ledger ●●○○ | Food/dish name (keeps a recipe's identity when arriving from Flow 3) | **Hero figure** + full macro breakdown + editable portion | Recipe thumbnail only when arriving from Flow 3 | H2 (trustworthy, editable confirmation) and the serving-size friction finding. It's the literal meeting point (IA), so it sits between the two ends of the dial. |
| **4 · Recipes & Filter** | Cookbook ○○●○ | Section title + recipe titles on cards | Compact nutrition strip on every card (kcal + P/C/F), plus "matched criteria" | Card photo | H3, Segment 2 and Segment 3: "enough to judge fit at a glance" (IA). Warm browsing, but fit is judged by figures (L1). |
| **5 · Recipe Detail** | Cookbook ○○○● | Large recipe title, section heads (Ingredients, Method) | Nutrition panel per serving; **"Log this"** in the same pine primary button as Screen 3's "Log it" | Hero photo | H4 and the IA structural rule "a recipe detail view never dead-ends". Same button, same figures, so the handoff is visually continuous. |

**Reconciled at Screens (IA 2), recorded here per the binding rule.** This row originally read **"None"** for Screen 2's serif use, on the reasoning that the most task-focused screen should carry nothing decorative. What shipped carries a `voice-title` "Add food", and a cross-screen audit of the finished set found the two binding documents disagreeing: §5 rule 3 below allows *at most one* serif element on every logging screen, and §5's role table already assigns the voice face to "the one screen title on logging screens" — both of which permit it — while this row forbade it.

**Resolved in favour of what shipped, and the row above now says so.** The reasoning:

- **A screen title is identity, not decoration.** The original "nothing decorative" argument holds for badges, illustration and ornament, and Add Food still carries none of those. It over-reached in treating the screen's own name as ornament.
- **Add Food is a task screen that opens over another screen.** It is the only screen in the set entered as a modal task with a "Close" (S1 task header, IA 2), so it is the screen that most needs to announce what it is. Removing the title's voice treatment would make the one screen that interrupts you the one screen that doesn't introduce itself.
- **It is consistent, not exceptional.** With this row corrected, all five screens open with a serif title, and the dial's real work is done where §3 always intended it — in *how much* serif (Screen 2 has exactly one element; Screen 5 has four across three sizes), in figures, and in imagery. The dial still separates ledger from cookbook; it no longer does it by denying one screen its name.
- **It is the tested element.** It shipped, was measured and critiqued at 24/40, and removing a working element to satisfy a table would be changing the product to fit the documentation. The documentation is what was wrong.

Reflected into [`../04-design-system/tokens-v1.md`](../04-design-system/tokens-v1.md) §2.2 (`voice-title` now lists IA screens 1, 2, 3, 4) and §8. The stylescape needs no change: it specifies type roles, never a per-screen serif budget.

---

## 4. Palette — one set, shared by both contexts

Warm neutrals from B give the ground. A's single-action-color discipline governs how color is *used*.

| Token | Hex | Role | Origin | Grounding |
|---|---|---|---|---|
| `ground` | `#F2EDE6` | App background, both contexts | B (Lifesum oat `#F0EAE4`, nudged lighter) | Warm tone distances the brand from the white-and-blue list look of the incumbents Segment 1 switchers are "burned by" (`02-audience-5w.md`). *(aesthetic judgment: exact shade)* |
| `paper` | `#FFFDF9` | Surface for every data block: log rows, confirmation, nutrition panels, cards | A (MFP `#FCFCFC` list surface), warmed | Figures always sit on the highest-contrast surface available (L1 → H2). *(aesthetic judgment: warm tint)* |
| `ink` | `#1F2421` | All figures, titles, primary text | A (pure black ink), softened to warm near-black | H2: maximum legibility for numbers. |
| `ink-2` | `#5E605A` | Secondary text: serving sizes, units in lists, captions | A (MFP gray sub-lines) | Carries A's weight/gray hierarchy. |
| `rule` | `#E3DCD2` | Hairline dividers in ledger lists | A (grouped dividers) | Ledger alignment (L1). |
| `pine` | `#2F5245` | **The only action color**: primary buttons ("Log it", "Log this"), active filter chips, links, focus | B (Lifesum deep pine `#364E48`) | **One action color in both contexts** (L3 → H4). Not A's blue: `#0066EA` is MyFitnessPal's identity color, and its dashboard reference literally shows a PREMIUM badge, the paywall signal research calls the loudest betrayal (H2). Not B's bright leaf green: that's the generic "wellness" cliché flagged as a con for B. |
| `pine-tint` | `#DCE6DF` | Selected chip / selected filter background | Derived from pine | Supports the dual filter modes on Screen 4 (`PRODUCT.md` "suitable for me"). |
| `protein` | `#B0513A` | Macro marks only (bars, dots) | B (Noom coral `#E45A42`, deepened for contrast) | Macro breakdown is a P0 Must-have (`03-competitor-analysis.md`), and A showed small tinted bars work. Food-derived hues keep the data layer inside the warm palette (L3). *(aesthetic judgment: terracotta)* |
| `carbs` | `#A87A1F` | Macro marks only | New (grain / ochre) | Same as above. *(aesthetic judgment)* |
| `fat` | `#4D6A85` | Macro marks only | New (slate) | Same as above. Deliberately **not** green or olive, so it can't be mistaken for the pine action color and avoids a red–green pair with `protein`. *(aesthetic judgment: hue family; the colorblind reasoning is functional)* |

**Color usage rules**
1. **Pine means "act".** Nothing decorative is pine, and no other color is tappable. This is A's single-action-color discipline, applied to one warm hue.
2. **Macro colors are marks, never text.** Labels "P / C / F" and the gram values are always `ink` or `ink-2`. Color is never the only carrier of meaning, and the ochre can't carry text (3.78:1 on paper, below 4.5:1).
3. **No premium/reward colors.** No gold, no badge colors, no celebration palette. That excludes C's streak styling and avoids any visual shorthand for paywalled tiers (H2). *(Judgment call: extends the paywall finding from features to visual language.)*
4. **Status colors** (over target, error) are **deferred to the design-system stage.** Research doesn't say how users want "over budget" framed, so choosing a tone (neutral vs. alarm) now would be unevidenced.
   *Resolved in Stage 4 (v1) as a judgment call:* over-target gets **no hue**. The word changes ("left" → "over") and the meter shows a hatched overflow, because users gain as well as lose weight and red would be a tinted figure (L1). Error color stays deferred to v2 and must never be reused for over-target. See [`04-design-system/tokens-v1.md`](../04-design-system/tokens-v1.md) §5 J1.

**Measured contrast (WCAG 2.x)**

| Pair | Ratio | Use allowed |
|---|---|---|
| `ink` on `paper` / on `ground` | 15.51:1 / 13.53:1 | All text, figures |
| `ink-2` on `paper` / on `ground` | 6.27:1 / 5.47:1 | Secondary text |
| `pine` text on `paper` / on `ground` | 8.56:1 / 7.47:1 | Links, chip labels |
| `paper` text on `pine` button | 8.56:1 | Primary button label |
| `pine` on `pine-tint` | 6.81:1 | Selected chip label |
| `protein` / `carbs` / `fat` vs `paper` | 5.06 / 3.78 / 5.56:1 | Non-text marks (≥3:1 ✓). Not for text (see rule 2) |
| `paper` vs `ground` | **1.15:1** | ⚠ Card edges are **not** a legibility device |

> **Honest note on B's contrast con.** `paper` on `ground` (1.15:1) is about as faint as the Lifesum reference (1.12:1). The hybrid does **not** fix that by strengthening card edges. It avoids depending on them: every figure and label clears AA against the surface it sits on, and data blocks are separated by alignment, spacing and hairline rules (A's ledger structure), not by fill contrast. Glanceability (H1) comes from ink-on-paper figures, not card outlines. Legibility in outdoor, one-handed use still needs validating on-device at the Screens stage.

> **Stage 4 extensions (Design System v1)**, recorded here so this doc doesn't drift from what ships. Full detail in [`04-design-system/tokens-v1.md`](../04-design-system/tokens-v1.md) §8.
> - **`stone` `#857F76` added** as a functional neutral for control edges (fields, unselected chips): 3.90:1 on `paper`, 3.41:1 on `ground`, meeting WCAG 1.4.11. `rule` (1.34:1) stays decorative. It's not a brand color, so the stylescape palette slide is unchanged.
> - **`oat-deep` `#E7DFD4` formalized** from the stylescape CSS as the sunken surface (mode-switch track, image placeholder). Macro meter tracks use `ground`, not `oat-deep`, because ochre measures only 2.91:1 on it.
> - **Refinement to the table above:** a selected chip keeps its **label in `ink`** (12.33:1 on `pine-tint`), with selection carried by the `pine-tint` fill + a `pine` outline + a check. This replaces "`pine` on `pine-tint` = selected chip label", because macro-match chips contain figures and L1 forbids tinting a figure.
> - Working names above map to v1 primitive/semantic tokens (e.g. `ink-2` → `color-ink-soft` / `text-secondary`, `pine-tint` → `color-pine-light` / `action-selected`). See tokens-v1.md §0.

---

## 5. Typography rule

**Two families, three roles.** The role, not the screen, decides the face (L1–L3).

| Role | Family (proposed) | Used for | Never used for | Grounding |
|---|---|---|---|---|
| **Voice** | **Newsreader** (serif, variable, optical sizes) | Recipe titles, recipe section heads, the one screen title on logging screens, empty-state headlines | Figures, buttons, labels, ingredient quantities, cooking steps | B's editorial serif for Segment 2's cookbook tone (H3). Optical sizes keep it readable from card title to hero title. *(aesthetic judgment: specific family)* |
| **Interface** | **Inter** (sans) | Buttons, labels, lists, filter chips, ingredient lines, method steps, body copy | Recipe titles on cards | A's system-sans clarity for task UI (H1). Steps and ingredients are read mid-cooking at a glance, so sans rather than serif *(Judgment call: legibility reasoning, not directly evidenced)*. |
| **Figure** | **Inter, tabular lining figures** (`tnum`, `lnum`) | Every nutrition value, portion amount, target, remaining | Anything non-numeric | L1 → H2: aligned, fixed-width digits make values scan and compare like A's ledger column, identically in recipe and log context (H4). |

**Rules**
1. **Numbers are never serif.** This is the single typographic line that separates *warm* from *exact*, and it's what defuses B's "serif reads approximate" con (H2).
2. **Unit always attached, at lower emphasis**: figure in `ink`, unit in `ink-2` at a smaller size ("**412** kcal"). One pattern everywhere.
3. **Serif budget per context**: logging screens (IA 1–3) get **at most one serif element** (the screen title or the food name). Recipe screens (IA 4–5) have no cap. This makes the §3 dial a concrete, checkable rule instead of a mood.
4. **Small caps-style labels** (tracked uppercase, from B's "FOOD PREFERENCES" pattern) are allowed for section labels in Inter, in `ink-2`, never in the serif.
5. **Weight carries hierarchy before size** (A's pattern): medium/semibold for primary, regular for secondary. Size jumps are reserved for the hero figure (Today, Confirmation) and recipe titles.

**Starting size anchors** (to be formalized into a scale at the design-system stage, not final):
- Hero figure: Inter 44–48 semibold, tnum.
- Recipe detail title: Newsreader 30–32 regular.
- Card recipe title: Newsreader 18–20.
- Body/list: Inter 16.
- Secondary: Inter 13–14.
- Section label: Inter 12, tracked caps.

**Why these families** — cross-platform + brief:
- Both are open-license, so one identical brand-first type system ships on iOS and Android. That follows the Platform decision in `CLAUDE.md` (not per-OS native) and "minimize manual work": no licensing or per-platform substitution.
- Inter was picked for a verified functional need (true tabular figures and small-size legibility), not personality. The brand personality is carried by the serif on purpose.
- *Family choice to be double-checked for `tnum` rendering and Newsreader's optical-size range when the design system is built.*

---

## 6. What's taken, what's left behind

**From A · Clinical Ledger** — kept as *structure and figure discipline*:
- Right-aligned tabular figure columns
- Single action color used only for action
- Weight/gray hierarchy
- Hairline ledger dividers
- Always-reachable logging entry (already an IA rule)

**Left behind from A:**
- The MyFitnessPal blue, cold white/gray surfaces, and dense all-caps blue text links. These make up the incumbent look Segment 1 switchers associate with paywalls (H2).

**From B · Oat & Serif** — kept as *tone*:
- Oat ground and deep pine
- Editorial serif for voice
- Tracked uppercase section labels
- Generous spacing on recipe screens
- The diet-tag/allergy chip pattern for Screen 4's tag filter mode

**Left behind from B:**
- Serif anywhere near numbers
- Relying on low-contrast card fills for structure
- Bright leaf-green "wellness" gradients
- Single-question-per-screen airiness on *logging* screens, which conflicts with H1

**From C · Bold Coach** — **explicitly excluded:**
- **No gamification.** No streaks, badges, celebration modals, reward colors or motivational mascots. The 5W segments were deliberately scoped around the two user stories and away from gamification (`02-audience-5w.md` method note). Separately, Cal AI's streak tracker was itself a recurring bug-complaint source (16/246 Google Play reviews, "Out of scope" table in `01-secondary-research.md`): a feature that creates its own trust failures. Segment 1's need for "visible, measurable progress" is met by the figures themselves (remaining vs. target on Today), not by reward mechanics.
- **No custom illustration or character art.** It contradicts the brief's "minimize manual work", and every visual in this system is produced by type, color tokens and photography instead.
- **Not carried over either:** C's stark black/white base and black pill buttons (a different brand, not needed once `pine` is the sole action color).

---

## 7. Food & recipe imagery — intended approach

> **⚠ Judgment call — to be validated with targeted references during the Screens stage, not resolved now.** None of the 12 reference screens showed food photography or recipe browsing (see the known gap in `01-direction-options.md`), so the approach below is a designer's proposal without a direct reference.

Food imagery should be **natural, not styled for spectacle**:
- **Light and grade:** soft daylight, shot overhead or at a low three-quarter angle, color-graded warm so plates sit naturally against the `ground`/`paper` tones rather than popping off them like ad photography.
- **Crops:** one consistent crop per context. A fixed-ratio photo at the top of recipe cards (Screen 4) and a single hero image on Recipe Detail (Screen 5), always edge-aligned to the paper surface.
- **Portions:** plausible, single-serving-looking portions, since the serving-size friction finding (`01-secondary-research.md`) suggests a lavish photo shouldn't imply a portion the "per serving" figures don't describe. *(inference, not evidenced)*
- **Nothing on the image:** images **never carry text, badges or nutrition figures**. Figures always sit below on `paper` (L1/L2), so photos add appetite without compromising the legibility of the numbers.
- **Logging screens:** no decorative imagery, only the camera viewfinder and, when arriving from a recipe, a small thumbnail for continuity (§3).
- **Prototype sourcing:** licensed stock or AI-generated images, treated strictly as placeholders. Per `PRODUCT.md` ("must not fabricate… nutrition figures presented as real"), no image or its accompanying figures should be presented as a real, verified recipe.

~~What still needs validating with references later:~~ **Answered at the Stage 7 imagery pass** (Krea; see `CLAUDE.md` Stage 7). The judgment call above is no longer a proposal — it is what shipped, and it held:

- **Crop ratios and card density** — one 4:3 crop (`ratio-recipe-image`) serves both rendered sizes, 120×90 and the 390 px hero. Density was settled earlier, at screen 04's critique: a full-bleed image on a result card made the list unscannable, so the card went compact with the thumbnail beside the body. **Audit A9 is closed.**
- **Whether overhead or angled shots read better at card size** — **overhead by default**, and it is the stronger read for anything whose contents are distinct shapes seen from above. **45° only where a dish's identity is its thickness:** the courgette fritters (patties, not discs) and the cottage cheese & lentil bake (a cut edge showing its layers). Both were checked at 120 px.
- **How much warmth in the grade still keeps food looking appetizing on the oat ground** — a warm, low-saturation grade on pale oatmeal linen works: plates sit *on* the Oat ground rather than popping off it, which was the point. The limit found in practice is at the dark end, not the warm end — the black bean chilli reads as a dark mass at 120 px. That is the dish, not the grade, and it is recorded rather than corrected.

The one §7 rule that remains a prohibition, not a resolved question: **images never carry text, badges or nutrition figures.** It holds across all 16 slots.

---

## 8. Traceability summary

| Decision | Type | Source |
|---|---|---|
| Hybrid instead of a single direction | Structural | `01-direction-options.md` side-by-side; `PRODUCT.md` Principle #1 |
| L1 — figures always identical, tabular, never serif | Structural (what data looks like) | H2 (`04-conclusions.md`); B's "reads approximate" con |
| L2 — warmth in words/ground/images only | Aesthetic, tone-grounded | Segment 2 (`02-audience-5w.md`), H3 |
| L3 — context shifts emphasis, not tokens | Structural mechanism | H4; IA Flow 3 · **Judgment call** on mechanism (§2) |
| Emphasis dial per IA screen | Structural | `information-architecture.md` screens 1–5; H1, H3, H4 |
| Pine as sole action color (not blue, not leaf green) | Aesthetic, tone-grounded | Distance from incumbents (Segment 1 switchers, H2 paywall signal); B cliché con · exact shade *(aesthetic judgment)* |
| Macro colors as marks only, colorblind-aware hue split | Functional | P0 macro breakdown (`03-competitor-analysis.md`); measured contrast · hues *(aesthetic judgment)* |
| No premium/reward colors | Tone | H2 paywall finding extended to visuals · **Judgment call** |
| Status colors deferred | Scope | No research on "over budget" framing · **Judgment call** |
| Newsreader + Inter, open-license | Aesthetic + functional | Platform decision & "minimize manual work" (`CLAUDE.md`); `tnum` need (H2) · family pick *(aesthetic judgment)* |
| Serif budget ≤ 1 per logging screen | Structural rule | H1 (logging speed) |
| Sans for cooking steps/ingredients | Functional | **Judgment call** (legibility mid-cooking, not evidenced) |
| No gamification, no custom illustration | Scope | `02-audience-5w.md` scoping; brief "minimize manual work"; Cal AI streak bug complaints (`01-secondary-research.md`, out-of-scope table, supporting only) |
| Food imagery approach | Aesthetic | **Judgment call**, validate at Screens stage (§7) |

---

## 9. Handoff to the next step (stylescape)

The stylescape should *demonstrate* the unifying rule, not add new decisions. It should show:
1. The same nutrition strip rendered on a log row and on a recipe card side by side (L1/L3).
2. Screen 3 and Screen 5 next to each other with the shared pine "Log it" / "Log this" button (H4 continuity).
3. The dial's two ends: a Today ledger fragment and a recipe-card grid on the same ground.
4. Type-role specimens (Voice / Interface / Figure) and the palette with its usage rules and contrast table.
5. Placeholder food imagery treated per §7, clearly labeled as unvalidated.
