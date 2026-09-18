# Research Conclusions

This is the synthesis of everything in `/01-research/` — the reference point for information architecture, branding, design system, and screens. Later stages should trace back here rather than re-deriving decisions from raw research.

---

## 1. Key hypotheses about user needs

**H1 — Speed and low friction beat feature depth for logging.** Users log food multiple times a day, in real-world moments (kitchen, restaurant, grocery aisle), often one-handed. Ease-of-use was the most repeated praise across all three competitors, while multi-step, repetitive entry flows were a recurring complaint on Cronometer's own forum. Depth of tracking matters far less than not making the daily habit feel like a chore.
*Supports: [01-secondary-research.md](01-secondary-research.md) (cross-app patterns; community forum findings), [02-audience-5w.md](02-audience-5w.md) (Segment 1 job story).*

**H2 — Trust in a logging method depends entirely on that method's own accuracy, and gating it feels like a betrayal.** Manual/barcode apps are judged on food-database accuracy; the AI-photo app is judged on estimate accuracy — but in both cases, once users build a daily habit around a specific logging method, moving that method behind a paywall (e.g. barcode scanning) was the single loudest complaint in the whole review sample, worse than pricing complaints in general.
*Supports: [01-secondary-research.md](01-secondary-research.md) (MyFitnessPal & Lose It! pain points, cross-app patterns).*

**H3 — Recipe discovery is a real, unserved need, not a minor add-on.** None of the three competitors has a recurring positive pattern around recipe discovery, home cooks visibly abandon in-app recipes for external sites, and a whole niche app category exists solely to fill the "find a recipe that fits my macros" gap. This is evidence of unmet demand, not evidence the feature doesn't matter.
*Supports: [01-secondary-research.md](01-secondary-research.md) (recipe blind-spot, niche app category), [02-audience-5w.md](02-audience-5w.md) (Segments 2 & 3), [03-competitor-analysis.md](03-competitor-analysis.md) (recipe rows).*

**H4 — The handoff between "finding a recipe" and "logging what I ate" is itself an unmet need, and the biggest available differentiation point.** This isn't inferred — it's a multi-year, still-unresolved feature request on both MyFitnessPal's and Cronometer's own community forums, and the one competitor that ships a version of it (MFP) does so imperfectly. Users don't want two disconnected tasks; they want one continuous flow.
*Supports: [01-secondary-research.md](01-secondary-research.md) (recipe-to-log import findings), [02-audience-5w.md](02-audience-5w.md) (Segment 3), [03-competitor-analysis.md](03-competitor-analysis.md) (Delighter rows).*

---

## 2. Prioritized feature list

Derived directly from the competitor analysis's Must-have row set (table stakes — skip any and the app feels broken next to incumbents) plus its two Delighter opportunities (where the research shows real differentiation room). Nice-to-haves (voice logging, quick-add shortcuts, diet-mode toggles, generic un-filtered recipe browsing) are deliberately **excluded from this project's scope** — they're incremental parity features, not decisive for either user story, and out of proportion to a research-backed but tightly scoped design exercise.

**P0 — Core loop (table stakes, both stories depend on this existing):**
1. Manual food search & logging from a searchable food database
2. Barcode / packaged-product scanning
3. AI photo-based meal recognition & logging
4. Macro breakdown (protein/carbs/fat) alongside the calorie number
5. Personalized calorie/macro targets, set once from user goals — this is also the foundation "suitable for me" draws on for recipes

**P1 — Differentiators (where this app should actually win):**
6. Recipe discovery filtered by **both** diet/goal tags (vegan, low-carb, allergies, etc.) **and** macro-target matching — per PRODUCT.md's resolved definition of "suitable for me," covering Segment 2 and Segment 3 on their own terms rather than picking one
7. Recipe-to-log integration — selecting or importing a recipe carries its calculated nutrition straight into a logged entry in one action, instead of requiring the user to find a recipe in one place and reconstruct its numbers in another

---

## 3. Information architecture direction

High-level shape only — not screens yet.

- **One shared "profile of me" set once, used everywhere.** Goals, calorie/macro targets, and diet constraints are configured a single time and feed both the daily logging targets (P0 #5) and the recipe filters (P1 #6). Two separate setup flows for the same underlying data would contradict the whole "suitable for me" premise.
- **Logging needs to be the fastest thing to reach, not necessarily the first thing seen.** Given H1, the entry points for P0 #1–3 (search, barcode, photo) must be reachable in one action from wherever the user already is — not nested in menus — because the triggering moment (about to eat, mid-meal-prep) is short and impatient.
- **Recipes need to be a first-class section, not a sub-tab of logging.** Per Product Principle #1 ("both stories are first-class") and H3, recipe discovery is a distinct, planning-moment activity (deciding what to cook, often before the food even exists yet) rather than a variant of the logging screen — it deserves its own space with its own two filter modes (tags + macro-target matching).
- **A recipe can never be a dead end.** Per H4 and P1 #7, every recipe detail view must resolve into a direct "log this" action that already carries the recipe's calculated nutrition — the structural requirement that makes the recipe-to-log delighter real rather than aspirational. This is the one place the two stories' flows must structurally intersect, everywhere else they can stay independent.
