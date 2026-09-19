# The Measured Kitchen

A calorie tracker that also finds recipes that suit you, then logs them just as precisely as you planned them.

This is a UX/UI design test task, made with an AI-native workflow: research, information architecture, branding, a design system, and five final screens with a clickable prototype.

## Video walkthrough

**▶ [Watch the walkthrough on Google Drive](https://drive.google.com/file/d/1tSHXqkwef8sRvdjh2sL3ZbbWhpBurUmL/view?usp=sharing)**

A short video tour of the project: the research behind it, the branding decision, the design system, and both user stories clicked through the prototype from start to finish. The written version of the same story is the [design rationale](docs/design-rationale.md).

## The two user stories

1. *As a user, I want to calculate the amount of calories in a dish or a specific product.*
2. *As a user, I want to find a recipe for a dish that is suitable for me.*

## Start here

**▶ Project home: [`https://vikagorod26.github.io/calorie-app-test-task/`](https://vikagorod26.github.io/calorie-app-test-task/)** (live once GitHub Pages is enabled). It links to the prototype, the branding, the design system, every screen and the rationale.

Working from a clone instead? Open [`index.html`](index.html), or go straight to the clickable prototype at [`06-prototype/index.html`](06-prototype/index.html). Both work offline, because the fonts and images are bundled with the repo.

**Why it looks and works this way:** [`docs/design-rationale.md`](docs/design-rationale.md), an 8-minute read covering the research findings, the branding decision, the key screen decisions, and the open questions.

## What's inside

| Folder | Contents |
|---|---|
| [`01-research/`](01-research/) | Review mining, audience segments, competitor analysis, conclusions |
| [`02-information-architecture/`](02-information-architecture/) | The five screens, their flows and the structural rules |
| [`03-branding/`](03-branding/) | Direction options, the chosen hybrid, and the [stylescape](03-branding/04-stylescape.html) |
| [`04-design-system/`](04-design-system/) | Tokens, [live component reference](04-design-system/components-v1.html), audit |
| [`05-screens/`](05-screens/) | Every screen in all its states, with notes explaining each element |
| [`06-prototype/`](06-prototype/) | The clickable prototype |

`CLAUDE.md` is the full stage-by-stage working log, and `PRODUCT.md` holds the product context.

## Tools

- **Claude Code** did the work, with these skills: [impeccable](https://github.com/pbakaus/impeccable) v4.3.1 (Apache 2.0) for critiques, audits and design checks; web-design-guidelines, heuristic-evaluation, design-taste-frontend and develop-design-rationale. The sources of the last four are pinned in [`skills-lock.json`](skills-lock.json). The skills folder itself isn't included in the repository.
- **MCP tools:** app-insight for the app-store research data, and [Krea](https://www.krea.ai) for the AI-generated dish photographs. Both are configured in [`.mcp.json`](.mcp.json).
- **Fonts:** Inter and Newsreader, bundled under the SIL Open Font License ([notice](assets/fonts/OFL-NOTICE.md)).

*Sample nutrition figures and recipe images are illustrative placeholders, not real or verified data.*
