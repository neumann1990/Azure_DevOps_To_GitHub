---
title: Migration approaches — Manual, Tooling, AI
status: draft
tags: [pipelines, tooling, ai-prompts, section-3]
updated: 2026-09-21
---

**In one line:** Three ways to cross from Azure Pipelines to GitHub Actions — by hand, with the vendor's CLI tooling, or with an AI prompt library — and section 3 of the talk walks all three.

## Why frame it this way

The existing notes on pipelines ([`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md)) and tooling ([`01-tooling.md`](01-tooling.md)) already cover the concept mapping and the CLI tools, but they read as a single flat wall of mechanics. Splitting it into three named approaches gives the audience a mental model — "here are your three options, here's what each costs you" — instead of a concept dump, and it gives the AI angle (the actual headline reason from section 1) a concrete, demonstrable payoff in section 3 rather than staying abstract.

## Approach 1 — Manual

Rewrite the YAML by hand, using the concept mapping and syntax differences as a translation guide.

- Source: [`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — concept mapping table, key syntactic differences (stages, conditionals, script steps, fail-fast behavior, classic editor).
- Honest cost: 1–2 days per complex pipeline, per the same source.
- QR target: [Migrating from Azure Pipelines to GitHub Actions](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines)

## Approach 2 — Tooling

Let `gh-ado2gh` handle repository migration and `gh-actions-importer` audit and assist the pipeline rewrite.

- Source: [`01-tooling.md`](01-tooling.md) — full setup, commands, the `audit` automatable/partial/manual breakdown.
- The `inventory-report` and `audit` outputs are, per Kevin's own note in that file, "the best slide material in the whole PoC — they turn 'this will be hard' into a number."
- ELM belongs here as a contrast, not a fourth approach: it's still tooling, just a preview service with continuous sync and a scheduled cutover instead of a one-shot script. See [`03-enterprise-live-migrations.md`](03-enterprise-live-migrations.md) for what it adds over the standard GEI CLI.
- QR targets: [gh-ado2gh](https://github.com/github/gh-ado2gh) (verify exact repo URL before printing), [gh-actions-importer](https://github.com/github/gh-actions-importer)

## Approach 3 — AI

Use an AI prompt library to define the mapping rules from Azure Pipelines constructs to GitHub Actions workflow syntax, rather than either memorizing the mapping (manual) or trusting a fixed CLI's rule set (tooling).

**Drafted, not yet tested.** The prompts live in a top-level `prompts/` folder in [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub) (the same repo these notes live in), matching the existing `case/`, `mechanics/`, `reference/`, `session/`, `subsystems/` pattern:

1. [`prompts/01-analyze-azure-pipeline.md`](../prompts/01-analyze-azure-pipeline.md) — inventory pass: what's in the pipeline, flagged by construct, rated Automatable/Partial/Manual.
2. [`prompts/02-convert-pipeline-to-actions.md`](../prompts/02-convert-pipeline-to-actions.md) — the actual conversion, encoding every rule from the concept mapping table and syntax differences above, plus a required change log for every judgment call.
3. [`prompts/03-validate-converted-workflow.md`](../prompts/03-validate-converted-workflow.md) — checks the converted workflow against the original for behavior parity (execution order, conditional logic, credentials, shell/error-handling defaults), not just YAML validity.

**Still open:** none of the three have been run against a real pipeline yet. That needs to happen before this slide is real — ideally against the same repo(s) chosen for the section 3 screenshot walkthrough (see the still-open "which repos" question in [`03-open-questions.md`](../session/03-open-questions.md)), so the AI approach and the manual/tooling approaches are all demonstrated against the same source material.

This is the natural payoff of section 1's "AI is the honest primary driver" thesis: it's one thing to say Copilot is why people migrate, another to demonstrate an AI-assisted path to a concrete migration task the audience actually cares about (pipeline rewrites).

## Related

- [`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — the manual approach's source material
- [`01-tooling.md`](01-tooling.md) — the tooling approach's source material
- [`03-enterprise-live-migrations.md`](03-enterprise-live-migrations.md) — where ELM fits as a tooling variant
- [`../session/06-slide-deck-outline.md`](../session/06-slide-deck-outline.md) — section 3's slide-by-slide placement of this framework, now with ELM restored as its own slide
- [`../session/07-qr-and-links-plan.md`](../session/07-qr-and-links-plan.md) — the repo (confirmed: this one) the prompts need a `prompts/` folder in
