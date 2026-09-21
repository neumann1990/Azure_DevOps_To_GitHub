---
title: Section outline
status: draft
tags: [session, outline, structure, sections]
updated: 2026-09-20
---

**In one line:** Six sections mapping the abstract's four promises, following the scorecard's difficulty gradient, bookended by the documentary opener and closer.

## The mapping

| # | Section | Promise it pays off | Opener card | Rough content source |
|---|---|---|---|---|
| 1 | **Why We Left the Herd** | *The real reasons teams migrate (yes, AI is one of them)* | "Migration Season Has Begun" | [`case/01-why-migrate.md`](../case/01-why-migrate.md), [`case/02-platform-direction.md`](../case/02-platform-direction.md) |
| 2 | **A Field Guide to the Local Species** *(new card — needs writing)* | *Which parts pack their bags gracefully…* (part A — the easy/partial movers) | "A Field Guide to the Local Species" | [`subsystems/00-scorecard.md`](../subsystems/00-scorecard.md) overview + repos, wiki, packages, dashboards ([01](../subsystems/01-repos.md), [04](../subsystems/04-wiki.md), [05](../subsystems/05-packages-and-artifacts.md), [07](../subsystems/07-dashboards-and-analytics.md)) |
| 3 | **Crossing the River** | *…rebuild your pipelines and workflows without a three-week meditation retreat* | "Rare Footage of Successful Deployment" | [`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md), [`mechanics/01-tooling.md`](../mechanics/01-tooling.md), [`mechanics/03-enterprise-live-migrations.md`](../mechanics/03-enterprise-live-migrations.md), [`mechanics/06-gei-repo-migration-runbook.md`](../mechanics/06-gei-repo-migration-runbook.md) |
| 4 | **Sprint Planning in Its Natural Habitat** | *…and which will cling to the doorframe* (part B — the hardest movers) | "Watch as the Scrum Master Approaches Carefully" | [`subsystems/03-boards-and-projects.md`](../subsystems/03-boards-and-projects.md), [`subsystems/06-test-plans.md`](../subsystems/06-test-plans.md), hybrid pattern from [`case/02-platform-direction.md`](../case/02-platform-direction.md) |
| 5 | **Preventing the Uprising** | *Change-management tips so your team transitions smoothly* | "The Senior Engineer Defends an Ancient Pipeline" | [`mechanics/05-migration-approach.md`](../mechanics/05-migration-approach.md) (change-management section), [`case/03-decision-framework.md`](../case/03-decision-framework.md) |
| 6 | **The Watering Hole Nobody Told to Move** | Wrap-up / long tail — sets up the closer | "The Watering Hole Nobody Told to Move" | Hardcoded-URL long tail from [`mechanics/05-migration-approach.md`](../mechanics/05-migration-approach.md), plus room for a war story / confession beat |
| — | **Closer** | Bookend, not a promise | "A world of our making" | Delivered over whatever's on screen at the end — Kevin's note: lands hardest over somebody's 2016 classic pipeline |

## Why this shape

- **Follows the scorecard's own reading order.** [`00-scorecard.md`](../subsystems/00-scorecard.md) already recommends "start with the easy win (repos), move into the grind (pipelines), end with the things that don't move (Boards, Test Plans) and the hybrid answer that makes that acceptable." Sections 2 → 3 → 4 *are* that gradient — it's also the emotional arc.
- **Promise 2 splits across two sections (2 and 4)** rather than one, because the scorecard's own verdicts split naturally into "travels clean / partial" (repos, wiki, packages, dashboards) versus "clings to the doorframe / stays behind" (Boards, Test Plans) — cramming all seven subsystems into one section would either rush the hard ones or bury the easy ones.
- **"The Senior Engineer Defends an Ancient Pipeline" moved to the change-management section (5), not the pipelines section (3).** The card reads as being about pipeline mechanics, but the joke is about a *person* resisting change — that's the "small, tool-related uprising" promise, not the YAML-rewrite promise. Putting it in section 5 makes the card do double duty: it's funny on its own, and it's the section's thesis.
- **Section 6 is deliberately light.** The material (hardcoded URLs, long-tail cleanup) is thin on its own — one paragraph in the source notes. It's sized to be a quick "six months later" beat that sets up the documentary closer, not a full 10-12 minute section.
- **Two new opener cards needed**, for sections 2 and 6. The four existing cards all had natural homes; the closer ("a world of our making") stays separate as the seventh and final documentary beat, per [`02-narrative-and-theme.md`](02-narrative-and-theme.md).

## Rough timing (draft — needs a timed read-through to confirm)

75 minutes of content, Q&A taken as a short break between sections rather than banked at the end (decided 20 Sep 2026 — see [`03-open-questions.md`](03-open-questions.md)).

| Segment | Minutes |
|---|---|
| Title + cold open | 3 |
| 1 — Why We Left the Herd | 10 |
| *Q&A* | 2 |
| 2 — A Field Guide to the Local Species | 8 |
| *Q&A* | 2 |
| 3 — Crossing the River | 15 |
| *Q&A* | 3 |
| 4 — Clings to the Doorframe | 14 |
| *Q&A* | 3 |
| 5 — Preventing the Uprising | 10 |
| *Q&A* | 2 |
| 6 — The Tracking Collar | 6 |
| Closer | 3 |

Total ≈ 81 min against a 90-minute slot — leaves ~9 minutes of slack, which is healthy rather than a problem. Section 3 (pipelines/tooling) carries the most weight; if anything needs trimming under time pressure, it's the ELM-vs-GEI contrast material, which is research-only anyway since ELM can't be trialled at Hunter.

## Still open

- ~~Write the two new opener cards (sections 2 and 6)~~ → **Locked in.** Section 2: "A Field Guide to the Local Species." Section 4's title also changed to "Sprint Planning in Its Natural Habitat" (opener card unchanged — still "Watch as the Scrum Master Approaches Carefully"). Section 6: "The Watering Hole Nobody Told to Move." Decided 21 Sep 2026.
- Confirm the timed read-through once section content is drafted — the table above is an estimate, not a rehearsed number.
- Section 6's "war story / confession" beat needs a concrete story — the abstract promises "confessions from teams who've already survived the trek," and nothing in the current notes is a first-person anecdote yet.

## Related

- [`01-brief.md`](01-brief.md) — the four promises, and the abstract they're drawn from
- [`02-narrative-and-theme.md`](02-narrative-and-theme.md) — the documentary conceit and existing opener cards
- [`03-open-questions.md`](03-open-questions.md) — outline was the top blocker; this resolves it
- [`../subsystems/00-scorecard.md`](../subsystems/00-scorecard.md) — the difficulty-gradient reading order this outline follows
