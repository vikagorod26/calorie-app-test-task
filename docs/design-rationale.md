# Design rationale — The Measured Kitchen

A short account of the decisions that shaped this calorie app, in the order they were made. Each section links to the file where the full reasoning lives. It summarises existing work and adds no new justifications.

**Reading time:** about 8 minutes · **Deeper context:** [`CLAUDE.md`](../CLAUDE.md) (stage notes) and [`PRODUCT.md`](../PRODUCT.md) (product context)

---

## 1. The problem

The brief asks for two things: *calculate the calories in a dish or product*, and *find a recipe that suits me*. Research showed the first is a crowded, well-served category. The second, and especially **the step from finding a recipe to logging it**, is a real gap that no major competitor fills.

---

## 2. What research told us

Evidence came from review mining of ~1,557 App Store and Google Play reviews (MyFitnessPal, Lose It!, Cal AI), the MyFitnessPal and Cronometer community forums, and store data for a competitor feature comparison. Full synthesis: [`01-research/04-conclusions.md`](../01-research/04-conclusions.md).

| | Finding | Evidence |
|---|---|---|
| **H1** | **Speed beats feature depth for logging.** People log several times a day, often one-handed, mid-meal-prep. | Ease of use was the most repeated praise across all three apps; repetitive multi-step entry was a recurring Cronometer forum complaint. [`01-secondary-research.md`](../01-research/01-secondary-research.md) |
| **H2** | **Trust depends on the accuracy of each logging method, and paywalling that method feels like betrayal.** | Moving barcode scanning behind a paywall was the loudest complaint in the whole sample. Cal AI's most repeated complaint was wrong foods and wrong portions. |
| **H3** | **Recipe discovery is a real, unserved need.** | No competitor has a positive review pattern around recipes; home cooks leave for external sites; a whole niche app category exists just for "recipes that fit my macros". [`03-competitor-analysis.md`](../01-research/03-competitor-analysis.md) |
| **H4** | **The handoff from finding a recipe to logging it is the biggest differentiation point.** | A multi-year, still-open feature request on both the MyFitnessPal and Cronometer forums; MyFitnessPal's own version is imperfect. |

From these, the scope set itself: a fast, ungated logging core (search, barcode, photo, macros, targets), plus recipe discovery filtered by **both** diet tags and macro targets, joined to logging in one action. Research also gave us a third audience between the two stories, the **macro-conscious meal planner** ([`02-audience-5w.md`](../01-research/02-audience-5w.md)). This person wants a recipe that hits their numbers, then wants to log it just as precisely.

---

## 3. The branding decision: The Measured Kitchen

Three directions were explored against real reference screens ([`03-branding/01-direction-options.md`](../03-branding/01-direction-options.md)):

- **A · Clinical Ledger** (MyFitnessPal): the strongest for numeric trust (H2), but it reads as the incumbent users are frustrated with.
- **B · Oat & Serif** (Lifesum, Noom): the strongest for recipes (H3), but weak for fast logging and for trust in the numbers.
- **C · Bold Coach** (Yazio, Cal AI, MacroFactor): the most glanceable (H1), but its gamified tone puts trust at risk.

**The finding: no single reference served both stories.** The chosen direction is a hybrid. It takes A's figure discipline and B's cookbook warmth, and drops C's gamification ([`02-hybrid-direction.md`](../03-branding/02-hybrid-direction.md), final presentation in [`04-stylescape.html`](../03-branding/04-stylescape.html)).

The rule that makes the hybrid hold together is **"Words are warm, figures are exact."**

- **L1:** every nutrition figure gets one identical treatment (Inter, tabular numerals, Ink, never the serif) on logging and recipe screens alike.
- **L2:** warmth lives only in words, the ground colour and imagery: Oat and Paper surfaces, the Newsreader serif for names and headlines, warm-graded food photography.
- **L3:** logging and recipe screens share every token and differ only in emphasis. For example, section spacing is 24 px on logging screens and 40 px on recipe screens: two steps on one scale.

Pine green is the **only** action colour, so "Log it" on Food Confirmation and "Log this" on Recipe Detail are visibly the same button. That makes H4's continuity something you can see.

---

## 4. The structural insight: one convergence screen

The information architecture ([`information-architecture.md`](../02-information-architecture/information-architecture.md)) keeps exactly five screens: Today, Add Food, Food Confirmation, Recipes & Filter, and Recipe Detail. Its key move is where the two stories meet:

- **Flow 1 (story 1):** Today → Add Food → Search / Barcode / Photo → **Food Confirmation** → Log it → Today
- **Flow 2 (story 2):** Today → Recipes & Filter → Recipe Detail
- **Flow 3 (the handoff):** Recipe Detail → Log this → **Food Confirmation**, pre-filled with the recipe's nutrition → Log it → Today
- **Flow 4 (added at Screens):** Today → tap an entry → **Food Confirmation** (Save changes / Remove entry) → Today

Food Confirmation is the **single convergence screen**. Every way of logging (search, barcode, photo, recipe, correcting an entry) ends there, so the recipe handoff is not a parallel logging path. It reuses Flow 1's final step. Three structural rules follow from it:

1. Logging is reachable in one tap from anywhere (H1).
2. A recipe never dead-ends: it always resolves into Food Confirmation (H4).
3. A logged entry is never final (H2). This rule was added after the Today critique.

On screen, "one convergence screen" became **one skeleton with named slots**: Back · source note · name · macro breakdown · portion · primary button. Each path only fills slots and never adds layout.

---

## 5. Key screen decisions

**1 · Every logged entry names where its number came from**
→ **Why:** H2 says trust depends on the accuracy of each method, and the research notes that "being transparent about confidence has outsized upside". The source (Photo estimate / Barcode / Food database / From recipe) leads each Today row, ahead of the amount and the time. We accepted the cost (more rows wrap onto a second line) because legibility of the source outranks compactness.
→ **Proves:** [`05-screens/01-today.html`](../05-screens/01-today.html)

**2 · An AI photo estimate looks exactly like any other figure (judgment call J2)**
→ **Why:** H2 plus Cal AI's portion complaints. Figures stay exact in form, because an estimate becomes a real entry that sums into the day, and a "~" or a range can't be summed. The uncertainty is carried in words instead: a source note, and one helper line placed directly above the portion control ("Estimated from your photo. Check the portion before you log it."). We rejected confidence percentages as a precision claim the product can't back. ([`tokens-v1.md`](../04-design-system/tokens-v1.md) §5)
→ **Proves:** [`05-screens/03-food-confirmation.html`](../05-screens/03-food-confirmation.html), frame C

**3 · Going over target is information, not an alarm (judgment call J1)**
→ **Why:** the audience includes people *gaining* weight and training, so "over" is not bad for everyone (`PRODUCT.md`, Segment 1). The stylescape's tone is "no confetti, no guilt trips", and L1 forbids a red figure. The word "over" and a hatched meter overflow carry the meaning with no colour, which also works for colour-blind users. The Today critique found "over" too easy to miss, so it was strengthened with weight, not hue.
→ **Proves:** [`05-screens/01-today.html`](../05-screens/01-today.html), frame B

**4 · Recipe filtering has two modes, and switching modes never drops a criterion**
→ **Why:** `PRODUCT.md` defines "suitable for me" as **both** diet tags (the home cook) and macro targets (the meal planner), with neither a subset of the other. The critique caught macro mode silently dropping diet criteria, which showed chicken to a vegetarian. The resulting rule: *a mode switches which criteria you tune, never which ones apply.*
→ **Proves:** [`05-screens/04-recipes-filter.html`](../05-screens/04-recipes-filter.html)

**5 · The proof of fit lives on the result card, not inside the recipe**
→ **Why:** the MyFitnessPal reference ([`mfp_nutr.png`](../03-branding/refs/mfp_nutr.png)) computes goal fit only *inside* an opened recipe. That is the research's "flags problem recipes retrospectively rather than recommending ones that already fit", seen directly. So each card names *your* criterion or margin ("170 kcal under your limit"), and results are ordered best fit first. The critique then moved the image beside the card body. This roughly doubled the number of results visible per screen, so options can be compared.
→ **Proves:** [`05-screens/04-recipes-filter.html`](../05-screens/04-recipes-filter.html)

**6 · A serving count means "the servings you are eating", and it carries into logging**
→ **Why:** Flow 3 requires that what gets logged is what the screen showed. The Cronometer forum finding says label servings aren't what people eat, and MyFitnessPal's "save and log a serving" pattern points the same way. The other reading ("servings the recipe makes") would have to rescale every ingredient, which the IA never asks for. The critique made the commit button say what it will log: **"Log this · 1.5 servings"**. The same dish also reads 412 kcal / 26 / 48 / 12 g on the recipe card, the detail page, Confirmation and Today; this was checked at build.
→ **Proves:** [`05-screens/05-recipe-detail.html`](../05-screens/05-recipe-detail.html) → [`06-prototype/index.html`](../06-prototype/index.html) (clickable)

---

## 6. Honest tensions

These are left open on purpose and recorded where they arise, not hidden.

- **"Authored, but undifferentiated."** The cross-screen taste pass found the product unmistakably its own against the twelve competitor references, but visually monotonous across its own set. Every element is a full-width band, two of the five screens open the same way, and the serif sets nouns only: not one sentence in 21 frames. The cookbook half of the brand is closer to a typeface than to a voice. Recorded for a copy and layout pass that was never scheduled. ([`CLAUDE.md`](../CLAUDE.md), Stage 5b)
- **The handoff carries the value, but not the name.** The portion control is called "Servings you're eating" / "Increase servings" on Recipe Detail and "Portion" / "Increase amount" on Food Confirmation. Similarly, "Log this" (go to Confirmation) and "Log it" (commit) are one word apart and do opposite things. Both labels come from the IA, so fixing them is an IA change, not a screen tweak. Related: neither screen yet tells you when a bigger portion breaks the fit that brought you to the recipe (a shared v2 item).
- **J1's bold "over": a reviewer disagreed, and the decision was kept.** The second critique read a bold "over" on a 2.3% overage as an alarm set in type. Both alternatives were weighed. Bold stays because the first revision showed the plain word was missed. The objection is recorded in [`tokens-v1.md`](../04-design-system/tokens-v1.md) §5 J1, to revisit with real users.

---

## 7. What ties it together

Every layer answers to the one before it. **Research** produced four hypotheses. The **IA** turned H4 into a structural rule (a recipe never dead-ends) and into one convergence screen. **Branding** turned the tension between trust and warmth into one law ("words are warm, figures are exact"). The **design system** made that law checkable: semantic tokens only, one figure treatment, two judgment calls written down with their reasons and their rejected alternatives. The **screens** were built only from that system, each element traced to research, the IA or a flagged judgment call, and each screen critiqued once with its P1/P2 findings fixed. **Verification** checks the whole chain, not just the pixels: one byte-identical system stylesheet across the reference and all ten screen and prototype files, 0 contrast failures, every figure tabular and in Inter, and the same dish's numbers identical on every screen it passes through. Where a decision rests on judgment rather than evidence, it says so.

---

**Where to go deeper**

| Topic | File |
|---|---|
| Research synthesis | [`01-research/04-conclusions.md`](../01-research/04-conclusions.md) |
| Screens, flows, structural rules | [`02-information-architecture/information-architecture.md`](../02-information-architecture/information-architecture.md) |
| Branding rationale and traceability | [`03-branding/02-hybrid-direction.md`](../03-branding/02-hybrid-direction.md) · [`04-stylescape.html`](../03-branding/04-stylescape.html) |
| Tokens, J1/J2, backlog | [`04-design-system/tokens-v1.md`](../04-design-system/tokens-v1.md) · [`components-v1.html`](../04-design-system/components-v1.html) |
| Screens with per-element "why" notes | [`05-screens/`](../05-screens/) |
| Clickable prototype (start here) | [`06-prototype/index.html`](../06-prototype/index.html) |
| Full stage log, critiques, audits | [`CLAUDE.md`](../CLAUDE.md) |
