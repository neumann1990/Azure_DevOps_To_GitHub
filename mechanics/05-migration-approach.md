---
title: Migration approach and change management
status: researched
tags: [approach, sequencing, change-management, waves]
updated: 2026-09-04
---

**In one line:** Start hybrid, migrate repos in waves, rewrite pipelines incrementally, and leave work items alone.

## Recommended approach

**1. Start with the hybrid.** Connect Azure Boards to GitHub repos before moving anything else.

**2. Migrate repos in waves.** Start with less critical repositories to build confidence.

**3. Rewrite pipelines incrementally.** Run old and new pipelines in parallel during transition.

**4. Keep Azure Boards.** Don't try to migrate work items to GitHub Issues unless your PM needs are simple.

Source: <https://codepulsehq.com/guides/azure-devops-vs-github-guide>

## Difficulty ordering

| Component | Difficulty | Note |
|---|---|---|
| Repository migration | Easiest | Git is Git |
| Pipeline migration | Rewrite required | 1–2 days per complex pipeline |
| Work item migration | Hardest | Usually shouldn't happen at all |

## Ordering constraints

Two orderings that are not negotiable:

1. **Install the Azure Pipelines GitHub app before migrating repositories** — otherwise the migration script can't automatically reconfigure pipelines to point at GitHub. → [`01-tooling.md`](01-tooling.md)
2. **Plan identity mapping before the first migration** — mannequins are created at migration time and remapping after the fact is worse. → [`02-identity-and-org-structure.md`](02-identity-and-org-structure.md)

## Change management

> **Kevin:** This is the "small, tool-related uprising" section of the abstract. The material below is the disciplined-selection framing from the comparison guides, which happens to double as change-management advice.

**Run a real selection process.** Define must-haves, assess current toolchain and data residency needs, model one increment in each tool, score with a weighted rubric, then run a four-to-six-week pilot with measurable outcomes.

**Delay heavy customization until after the pilot.** Customizing early locks in decisions made before anyone understood the tool.

**Don't judge on sticker price alone.** Compare licensing tiers, security add-ons like GHAS, runner and minutes costs, and administration or migration effort. At 100+ engineers, time saved in governance and reporting can outweigh modest per-user price differences.

**Match the tool to the context, not the trend.** Startups and one to three squads typically prefer GitHub Projects. Scaled agile, regulated industries and multi-team portfolios benefit from Azure Boards. Mixed estates and platform organizations often adopt a hybrid pattern.

**Structure your work items.** AI and Copilot multiply value only when work items are well structured. Invest in clear templates and acceptance criteria to realize real gains.

## The long tail

The thing that generates the most post-migration tickets: **hardcoded Azure DevOps URLs** in scripts, pipelines, IaC, service connections, README links and internal tooling. Budget a sweep, and expect to find more after you think you're done.
