# Target Audience — 5W Segments

Method: Mark Sherrington's 5W (Who, What, Why, Where, When), applied to build segments strictly around our two user stories — calculating calories in a dish/product, and finding a recipe that suits the user — not general app engagement (social, gamification, workouts, etc.). All evidence lines trace back to [01-secondary-research.md](01-secondary-research.md), per the product principle that UX/branding decisions should trace to research rather than be invented.

Two segments map directly to the two user stories (**Daily Calorie Tracker** → story 1, **Suitability-Seeking Home Cook** → story 2); a third (**Macro-Conscious Meal Planner**) sits at the seam between them, because the research surfaced that seam — recipe-to-log integration — as a distinct, underserved need rather than a natural extension of either story alone.

---

## Segment 1 — The Daily Calorie Tracker

*(Primary segment — user story 1: calculating calories in a dish/product)*

| 5W | Detail |
|---|---|
| **Who** | Adults actively managing weight (loss, gain, or recomposition) or training toward a fitness goal, who log food multiple times a day, most days, often for months at a stretch. Many are experienced switchers — long-time users of MyFitnessPal, Lose It!, or Cal AI who know exactly what "good" logging feels like because they've been burned by what doesn't. |
| **What** | They log every meal, snack, or product via barcode scan, manual search, or photo, expecting a fast, trustworthy calorie (and often macro) number with minimal typing — then check that number against a running daily budget. |
| **Why** | To stay accountable to a target without doing nutrition math themselves; the payoff they repeatedly cite is visible, measurable progress (specific lbs/kg lost) that makes the daily logging effort feel worth it. They abandon or openly complain about tools that make this harder — through slow multi-tap entry, unreliable barcode/database matches, or inaccurate AI-photo estimates — especially once a feature that used to make logging fast gets paywalled after the habit is built. |
| **Where** | On their phone, in real-world, often one-handed contexts: standing in the kitchen right before eating, at a restaurant table, in a grocery aisle scanning a product. Rarely a seated, focused session. |
| **When** | Multiple times per day, right at (or just before/after) the moment of eating — a repeated micro-task, not a planned one. The moments of highest frustration are the friction points: an unreadable barcode, an ambiguous photo, or a manual search returning duplicate/wrong entries. |

**Evidence:** Paywalling of barcode/macro-tracking features drew the single loudest, most repeated complaint across MyFitnessPal and Lose It! reviews; food-database and AI-photo accuracy were the top scrutiny points across all three apps; "effective for weight loss" and "easy/fast to log" were the most repeated praise in every app sampled; Cronometer's community forum shows sustained requests to collapse repetitive multi-tap entry into a single action, plus friction around portion/serving-size unit conversion.

**Job story:** *When I'm about to eat something and need to know if it fits my day, I want to log its calories in as few taps as possible with a number I can trust, so I can stay accountable to my goal without logging becoming its own chore.*

---

## Segment 2 — The Suitability-Seeking Home Cook

*(Secondary segment — user story 2: finding a recipe that's suitable for me)*

| 5W | Detail |
|---|---|
| **Who** | People who cook at home regularly and hold some personal constraint — a health goal, a diet type (keto, vegan, high-protein), or an allergy/intolerance — who want a recipe that already respects that constraint, rather than picking a recipe first and finding out afterward whether it fits. Less numerically obsessive than a macro tracker; motivated by "eating right for me," not hitting an exact number. |
| **What** | They search or browse for what to cook next, filtering (mentally or literally) by whether a recipe fits their calorie or dietary needs. When the app/site they're using doesn't filter well, they leave it — browsing external recipe blogs, asking in community forums for recommendations, or settling for generic "healthy recipes" lists that don't reflect their specific needs. |
| **Why** | They want confidence *before* cooking — deciding what to make without redoing nutrition math afterward or discovering midway that a dish doesn't fit their goals or restrictions. The value is trust in the choice, not just information about a dish already made. |
| **Where** | In the kitchen while deciding what to cook (before shopping or before starting), often on a phone or tablet propped nearby; also earlier — on the couch or during a commute — while planning meals for the week ahead. |
| **When** | At planning moments: deciding what's for dinner, building a weekly meal plan, or grocery shopping — a distinctly "before" moment, in contrast to Segment 1's "in the moment of eating." |

**Evidence:** None of the three reviewed apps had a recurring review pattern about recipe discovery — it isn't a headline feature for any of them, a gap rather than a solved pattern. MyFitnessPal's own community forum shows users can't even search/filter their own saved recipes (not listed alphabetically, no web search), and a long-running "Looking for good recipe sites" thread shows users routinely leaving the app for external recipe sources rather than trusting in-app suggestions.

**Job story:** *When I'm deciding what to cook next, I want to find a recipe that already fits my calorie and dietary needs, so I can cook with confidence instead of discovering afterward that it didn't fit.*

---

## Segment 3 — The Macro-Conscious Meal Planner

*(Bridge segment — spans both user stories at the point they currently break apart)*

| 5W | Detail |
|---|---|
| **Who** | People tracking macros for a specific body-composition or performance goal (cutting, bulking, general recomposition) — more numerically engaged than the average home cook, more meal-plan-oriented than the average daily tracker. Real enough as a distinct crowd that a whole niche app category (MacroMatch, Macrofy, "Stupid Simple Macro Recipes") exists solely to serve them, because general calorie trackers and general recipe sites each cover only half of what they need. |
| **What** | They want to find a recipe that fits precise macro targets (not just "healthy"), then log it as a single accurate entry — collapsing "what should I cook" and "how do I log what I ate" into one flow, instead of finding a recipe in one place and manually reconstructing its nutrition in a separate tracker. |
| **Why** | Reverse-engineering a recipe's macros ingredient-by-ingredient, or re-searching for it after the fact, is exactly the friction that drove years of user requests (on both MyFitnessPal's and Cronometer's forums) for URL-based recipe import with automatic nutrition calculation and one-tap logging. This segment cares specifically about that bridge working well — it's the one place the two user stories currently connect, and where both incumbent apps still treat it as an imperfect, secondary feature. |
| **Where** | Wherever meal-planning happens — batch-cooking on a weekend, planning the week's meals in advance — and later back in the kitchen at the actual moment of eating a pre-planned meal, just to confirm it was logged. |
| **When** | Two linked moments, not one: the **planning** moment (choosing or importing a recipe that fits their macros) and the **logging** moment (confirming they ate it as planned). What defines this segment is that they expect these two moments to stay connected rather than being two disconnected tasks. |

**Evidence:** MyFitnessPal's URL-based Recipe Importer (auto-parses ingredients, offers "save & log a serving") and Cronometer's multi-year-requested equivalent (shipped imperfectly, ingredient-matching still described as inexact) show recipe-to-log integration is a validated, still-unsolved need; the existence of standalone macro-recipe-finder apps is independent evidence that neither general trackers nor general recipe sites currently satisfy this segment on their own.

**Job story:** *When I plan a meal to fit my macro targets, I want to log it with the same accuracy I planned it with, so I can trust my numbers without redoing the math by hand.*
