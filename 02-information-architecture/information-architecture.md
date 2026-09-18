# Information Architecture

**Scope check:** The brief in `CLAUDE.md` asks for "final screens" demonstrating exactly two user stories — calorie/product calculation and recipe discovery — not a full app. An earlier draft of this document included Onboarding and Profile/Settings screens; both are cut here because neither directly serves either user story (they're supporting infrastructure, not one of the two stories), and Profile/Settings specifically had no direct research justification when originally added — it existed only to keep a first-draft principle consistent, which isn't a strong enough reason to include it in a deliberately tight screen set.

**Judgment call, flagged explicitly:** Screens 1 and 4 below reference "the user's saved calorie/macro targets and diet preferences" as existing input. Where that data comes from (onboarding, defaults, manual entry) is out of scope for this screen set — this is a designer's scoping decision to keep the deliverable to the brief's two stories, not something directly evidenced by research. If a reviewer needs to see how that profile is set, it would be a 6th screen added deliberately later, not implied here.

**Traceability audit (self-review):** This document was checked line-by-line against `01-secondary-research.md`, `02-audience-5w.md`, `03-competitor-analysis.md`, `04-conclusions.md`, and `PRODUCT.md`. Two things were wrong and are now fixed: (1) Screen 2's justification previously attributed an "editable, not one-shot, AI workflows" industry trend to `01-secondary-research.md` — that phrase does not appear anywhere in the saved research; it was conflated with an earlier, unsaved web-search snippet that never made it into the document. The saved industry article (Consumer Tech Wire) actually emphasizes the opposite — that photo logging wins by becoming fast *and* accurate, not by adding review steps. The citation is corrected below; the underlying design choice is now marked as a judgment call. (2) Screen 4's content list was missing the profile-data reference the top note above claims it has — restored below. Several other choices (the mode-switcher pattern on Screen 2, the single shared confirmation screen on Screen 3, the chronological ordering on Screen 1) were stated with more confidence than the research gives them; they're now explicitly marked as judgment calls informed by, but not directly prescribed by, the cited findings.

---

## Screens & Content

Every screen below exists because a specific research finding demanded it, or a specific finding shaped a key choice on it. Sources: [01-research/01-secondary-research.md](../01-research/01-secondary-research.md), [02-audience-5w.md](../01-research/02-audience-5w.md), [03-competitor-analysis.md](../01-research/03-competitor-analysis.md), [04-conclusions.md](../01-research/04-conclusions.md), and [PRODUCT.md](../PRODUCT.md).

Five screens total. **Add Food** and **Food Confirmation & Log** are Story 1's core; **Recipes & Filter** and **Recipe Detail** are Story 2's core; **Today / Daily Log** is the shared entry point and intersection screen both stories return to.

---

### 1. Today / Daily Log (home)

**Content/elements:**
- Remaining/consumed calories and macros vs. today's target
- Chronological list of items logged today *(the chronological ordering itself is a judgment call — a reasonable default, but no research finding specifies list ordering; showing a running list at all is what's evidenced, via Segment 1's "check that number against a running daily budget" in `02-audience-5w.md`)*
- Persistent, one-tap entry point into **Add Food**
- Every logged entry opens **Food Confirmation & Log** to correct or remove it *(added at Stage 5, after the Today critique; see Flow 4)*

**Why it's shaped this way:** H1 in `04-conclusions.md` establishes that trackers log "multiple times a day, in real-world moments... often one-handed" — `02-audience-5w.md`'s Segment 1 job story is literally "I want to log its calories in as few taps as possible." Making Today the landing screen, with logging one tap away, is the direct structural answer to both, and to `04-conclusions.md`'s explicit rule that entry points "must be reachable in one action from wherever the user already is." This screen is also where both user stories converge — a recipe logged via Screen 5 (see below) lands here exactly like a manually-logged item does. That convergence is a **structural consequence** of the cited rules (H4 plus the two structural rules at the bottom of this doc), worked out here rather than a separately-evidenced requirement in its own right.

---

### 2. Add Food (Search / Barcode / Photo)

**Content/elements:**
- Method switcher between three logging modes, each a P0 Must-have from `03-competitor-analysis.md`:
  - **Search** — text field, live results from a food database, each result showing calories/serving
  - **Barcode Scan** — camera viewfinder framed for a barcode
  - **Photo Scan** — camera capture button, then an AI-identified result the user can review before accepting
- Reachable from the persistent entry point on Screen 1

**Why it's shaped this way:** All three modes are included because `03-competitor-analysis.md` found manual search, barcode scanning, and AI-photo logging present in *all three* competitors — Must-have, not optional; cutting any would fail the brief's first user story against the evidence for what "calculate the amount of calories in a dish or a specific product" requires in practice. Presenting them as switchable modes of one entry point, rather than three separate destinations, is a **designer's judgment call**: `04-conclusions.md`'s H1 (minimize steps to reach any logging method) supports the spirit of it, but no finding specifically prescribes a mode-switcher over any other pattern — a different designer could satisfy H1 another way. Photo Scan is shown as "review before accepting" rather than auto-committing because `01-secondary-research.md` found AI-photo accuracy (misidentified foods, wrong portions) was Cal AI's single most-repeated complaint — that risk is directly evidenced. The review-step *response* to that risk is this project's judgment call, not a cited industry consensus: an earlier draft of this document over-attributed it to an "editable workflows" industry trend that does not actually appear in `01-secondary-research.md`'s saved industry-article summary (that summary instead emphasizes photo logging winning on growing *accuracy and speed*, not on adding review steps).

---

### 3. Food Confirmation & Log

**Content/elements:**
- Identified food/dish name, calorie count, full macro breakdown (protein/carbs/fat)
- Portion/serving-size control, editable
- "Log it" action, committing the entry to Today's log
- Also opened from a logged entry on Today (Flow 4): pre-filled with that entry, with "Save changes" and "Remove entry" in place of "Log it" *(added at Stage 5)*

**Why it's shaped this way:** This is the single convergence point for every way calories enter the app — search, barcode, photo, and recipes — rather than each method having its own confirmation UI. `04-conclusions.md`'s H2 found trust in a logging method depends on that method's own accuracy; giving every method the same trustworthy, editable confirmation step is this project's chosen way of treating that accuracy-trust consistently — H2 supports that consistency, but **consolidating into one literal shared screen (rather than, say, per-method confirmation UIs that happen to look alike) is a designer's judgment call**, not something the research specifies as an implementation. The explicit, editable portion control itself is directly evidenced: Cronometer community-forum research (`01-secondary-research.md`) flagged serving-size entry as friction independent of the food database itself. This screen is also where the recipe→log handoff (Screen 5) actually lands — see below.

---

### 4. Recipes & Filter

**Content/elements:**
- Two filter modes on one screen: **diet/goal tags** (vegan, keto, allergies, etc.) and **macro-target match** (numeric calorie/macro range)
- Both modes pre-populated from the user's saved calorie/macro targets and diet preferences (per the judgment-call note at the top of this doc — where that profile data comes from is out of scope for this screen set), editable per search
- Results list that updates against whichever mode is active, each result showing enough to judge fit at a glance (name, image, calories/serving, matched criteria)

**Why it's shaped this way:** `PRODUCT.md`'s resolved definition of "suitable for me" requires **both** dietary/goal-tag fit and macro-precision fit, "since the two segments select recipes on different criteria and neither is a subset of the other" — directly reflecting `02-audience-5w.md`'s Segment 2 (home cook, thinks in tags) versus Segment 3 (macro-conscious planner, thinks in numeric targets). Filtering and results are combined into one screen (a filter-only screen and a separate results screen were considered and merged) because splitting them added a step without adding evidence-backed value — the brief calls for key screens demonstrating the story, and the dual-mode filtering insight is fully demonstrable on one screen. This screen is also `03-competitor-analysis.md`'s direct fix for its Delighter opportunity: no competitor filters recipes by real personal fit today.

---

### 5. Recipe Detail

**Content/elements:**
- Recipe content: ingredients, steps, image
- Calculated nutrition for the recipe (calories, macros — per serving, adjustable by serving count)
- A "Log this" action, always present, that carries the recipe's calculated nutrition into **Screen 3 (Food Confirmation & Log)**

**Why it's shaped this way:** This is where `04-conclusions.md`'s second structural rule is enforced: "a recipe can never be a dead end... every recipe detail view must resolve into a direct 'log this' action." It's the exact point where the two user stories in `CLAUDE.md`'s brief structurally meet — flagged in `04-conclusions.md` (H4) and `03-competitor-analysis.md` as the sharpest available differentiation opportunity, because the equivalent handoff is a multi-year, still-imperfect feature request on both MyFitnessPal's and Cronometer's own community forums (`01-secondary-research.md`). Routing "Log this" into the same Food Confirmation screen used by search/barcode/photo — rather than a separate recipe-specific logging UI — is what makes this seamless rather than a second, parallel logging path, directly serving Segment 3's job story in `02-audience-5w.md`: "I want to log it with the same accuracy I planned it with, so I can trust my numbers without redoing the math by hand."

---

## User Flows

Screen → Action → Screen, for both stories plus the point where they intersect.

### Flow 1 — Story 1: Calculate calories in a product/dish

```
Today / Daily Log  →  [tap the always-available Add Food entry point]  →  Add Food

Add Food (Search mode)   →  [type, select a result]              →  Food Confirmation & Log
Add Food (Barcode mode)  →  [scan a barcode, match found]         →  Food Confirmation & Log
Add Food (Photo mode)    →  [capture a photo, AI identifies]      →  Food Confirmation & Log (shown for review, not auto-logged)

Food Confirmation & Log  →  [adjust portion if needed, tap "Log it"]  →  Today / Daily Log (entry now visible in the list)
```

The one-tap-from-anywhere rule (`04-conclusions.md`) is satisfied at the first arrow: Add Food is reachable from Today in a single action, regardless of which of the three methods the user then picks.

### Flow 2 — Story 2: Find a recipe suitable for me

```
Today / Daily Log  →  [tap Recipes in navigation]  →  Recipes & Filter

Recipes & Filter  →  [choose "By diet & goals" or "By macro match", apply criteria]  →  Recipes & Filter (results update in place)

Recipes & Filter  →  [tap a result]  →  Recipe Detail
```

The dual-mode filter (`PRODUCT.md`'s resolved "suitable for me") is demonstrated at the second step — the same screen serves both fit criteria rather than forcing a choice between them upfront.

### Flow 3 — The intersection: recipe → log

```
Recipe Detail  →  [tap "Log this"]  →  Food Confirmation & Log (pre-filled with the recipe's calculated nutrition, not a blank form)

Food Confirmation & Log  →  [adjust serving if needed, tap "Log it"]  →  Today / Daily Log (recipe now appears as a logged entry, identical in form to a manually-logged item)
```

This is the deliberate structural overlap: Flow 3's second step is the *same* screen and the *same* action as Flow 1's last step. A recipe never dead-ends into a read-only page (`04-conclusions.md`'s second structural rule) — it re-enters Story 1's logging flow through the one screen every other logging method already uses, which is what makes the handoff a real, evidenced differentiator (`03-competitor-analysis.md`'s Delighter opportunity) rather than two features that merely sit next to each other.

### Flow 4 — Correct a logged entry *(added at Stage 5)*

```
Today / Daily Log  →  [tap a logged entry]  →  Food Confirmation & Log (pre-filled with that entry: name, source, portion)

Food Confirmation & Log  →  [adjust the portion, tap "Save changes"]  →  Today / Daily Log (entry updated, totals recalculated)
Food Confirmation & Log  →  [tap "Remove entry"]                     →  Today / Daily Log (entry removed, totals recalculated)
```

**Why it exists:** research shows wrong entries happen often. Barcode scans pull "up the wrong food"; AI-photo logging misjudges foods and portions; crowdsourced database values for the same food differ by −13% to +7% (`01-secondary-research.md`). Without a way back, one wrong entry skews "left" on Today for the rest of the day, which undercuts H2 (trust in the logging method). The Stage 5 critique of Today scored user control and error recovery 1 out of 4 because of this gap.

**Judgment call, flagged:** Flow 4 reuses Screen 3. Inline editing on Today, swipe-to-delete or a separate edit screen were the alternatives. Reusing Screen 3 keeps one place where a portion is set, which is where the evidenced serving-size friction is handled, and adds no sixth screen. An undo message straight after "Log it" is a related but separate state, deferred to Design System v2.

---

## Structural rules carried through every screen above

1. **Logging is reachable in one tap from anywhere.** Enforced on Screen 1 (persistent entry point) and Screen 5 (recipe → log in one action) alike — never buried behind navigation, per `04-conclusions.md`.
2. **A recipe detail view never dead-ends.** Screen 5 always resolves into Screen 3, carrying calculated nutrition with it — the structural realization of the recipe-to-log Delighter identified in `03-competitor-analysis.md`.
3. **A logged entry is never final.** Every entry on Screen 1 opens Screen 3 to correct or remove it (Flow 4, added at Stage 5). Evidence: barcode, photo and database accuracy findings in `01-secondary-research.md`, and H2.
