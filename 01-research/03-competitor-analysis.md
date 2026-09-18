# Competitor Feature Analysis — Calorie Logging & Recipe Discovery

**Method:** Built from data already gathered via the app-insight MCP — official App Store/Google Play app descriptions for MyFitnessPal, Lose It!, and Cal AI, cross-checked against the review-mining and forum findings in [01-secondary-research.md](01-secondary-research.md). No new competitor data was fetched for this doc. Scope is limited to features that serve our two user stories (calculating calories in a dish/product; finding a recipe suitable for the user) — GLP-1 tracking, social/community features, fitness/workout tracking, and other unrelated features are excluded, consistent with the "Out of scope" boundary set in the research doc.

**Categories (MoSCoW-style):**
- **Must-have** — present in all three apps; table stakes for either user story.
- **Nice-to-have** — present in some (one or two) apps; a differentiator if missing, but not universally expected.
- **Delighter** — either unique/standout where it exists, or an explicit opportunity flagged by research because no competitor executes it well today.

---

## Feature comparison

| Feature | MyFitnessPal | Lose It! | Cal AI | Category |
|---|---|---|---|---|
| Manual food search & logging from a text-searchable food database | ✅ 20.5M+ food database | ✅ 56M+ item global database | ✅ supported, but reviews describe it as a weaker secondary path behind the AI-photo flow | **Must-have** |
| Barcode / packaged-product scanning | ✅ (Premium) | ✅ (Premium) | ✅ via photo/packaging recognition, not a separate scanner | **Must-have** |
| AI photo-based meal recognition & logging | ✅ (Premium "Meal Scan") | ✅ (Premium "AI Photo" logging) | ✅ core/primary logging method | **Must-have** |
| Macro breakdown (protein/carbs/fat) alongside calories | ✅ | ✅ | ✅ | **Must-have** |
| Personalized calorie/macro targets from user profile & goals | ✅ (goal-based: loss/gain/maintenance/performance) | ✅ (personalized calorie budget from profile) | ✅ (onboarding "lifestyle questions" build a plan) | **Must-have** |
| Voice-based food logging | ✅ (Premium) | ✅ (Premium "AI Voice" — e.g. "I had 2 eggs, toast...") | ✗ not offered | **Nice-to-have** |
| Quick-add / saved-meal shortcut for fast re-logging | ✅ "Quick Add" (confirmed via review mining) | — not evidenced in gathered data | ✅ "Food Memory" (remembers frequent meals) | **Nice-to-have** |
| Diet-mode nutrition filtering while logging (e.g. keto/low-carb mode) | ✅ "Net Carbs Mode" (Premium) | — not evidenced | — not evidenced | **Nice-to-have** |
| In-app recipe search/browsing (generic recipe database, not goal-filtered) | ✅ Recipe Box + curated library | ✅ "search our database of items, menu items and recipes" | ✗ no recipe feature at all | **Nice-to-have** |
| **Recipe recommendations filtered to fit specific dietary/macro goals** (not just a generic list) | Partial — 1500+ recipes marketed as "tailored to your calorie, macro, nutrition & fitness goals," but gated behind the top Premium Plus tier; MFP's own community forum shows users still can't reliably search/filter even their *own saved* recipes | Minimal — recipe search exists with no evidenced goal/macro filtering; its "Weight Loss Diet Plans" feature flags problem recipes retrospectively rather than recommending ones that already fit | ✗ none — no recipe feature exists | **Delighter opportunity** |
| **Recipe-to-log integration** (import/paste a recipe → auto-calculated nutrition → log a serving in one action) | Partial — ships a URL-based Recipe Importer with a "save & log a serving" action, but it's web-first and its own ingredient-matching is explicitly described as imperfect | ✗ none evidenced | ✗ none (no recipe feature at all) | **Delighter opportunity** |

---

## Why the two Delighter rows matter

Both are called out explicitly (not just listed as gaps) because research already validated demand for them, not just their absence:

- **Goal-fit recipe recommendations:** [01-secondary-research.md](01-secondary-research.md) found that none of the three apps had a recurring *positive* review pattern about recipe discovery — it isn't a headline feature for any of them — while a whole niche app category (MacroMatch, Macrofy, "Stupid Simple Macro Recipes") exists solely to fill the "find a recipe that fits my macros" gap. [02-audience-5w.md](02-audience-5w.md)'s Segment 2 (home cooks) and Segment 3 (macro-conscious meal planners) both select recipes by fit criteria neither incumbent filters on well.
- **Recipe-to-log import:** Community-forum research found this is a multi-year, still-unresolved request on both MyFitnessPal's and Cronometer's own forums — the one incumbent that ships it (MFP) does so imperfectly (web-first, inexact ingredient matching), and Segment 3 specifically wants this bridge to "just work" rather than requiring users to plan a recipe in one place and reconstruct its nutrition by hand in another.

Together, these two rows are the strongest evidence-backed opportunity to differentiate on user story 2 — where the Must-have and Nice-to-have rows above are already commoditized across the category.
