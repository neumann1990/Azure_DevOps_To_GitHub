---
title: QR codes and links plan
status: draft
tags: [session, qr-codes, links, public-repo]
updated: 2026-09-21
---

**In one line:** QR codes throughout the deck pointing to specific tools/docs, plus a consolidated links slide near the end — all of it, including the AI prompts, published to a public git repo alongside these notes and the .pptx.

## The plan

Kevin's intent, as stated 21 Sep 2026: QR codes on individual slides where a specific tool, doc, or resource is named, not just a wall of links at the end. The end-of-deck links slide (section 6, slide 6 — see [`06-slide-deck-outline.md`](06-slide-deck-outline.md)) is the consolidated fallback for anyone who didn't scan one earlier, not the only place links live.

**Resolved 21 Sep 2026: the public repo is this same notes repo.** [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub) — confirmed public, and it's the repo these notes already live in (`git remote -v` matches). No separate cleanup repo. That simplifies the plan considerably: everything QR-coded — these notes, the AI prompts, and (still open) wherever the .pptx itself ends up — is already in one place.

## Still open

- ~~Where the AI prompts live within this repo.~~ → **Decided and created: top-level `prompts/` folder**, matching the existing `case/`, `mechanics/`, `reference/`, `session/`, `subsystems/` pattern. Three prompts drafted (analyze, convert, validate) — see [`../prompts/README.md`](../prompts/README.md). Added to the top-level README's folder map.
- **Whether the .pptx itself gets committed to this repo** (large binary in git) or hosted elsewhere with the repo just linking to it. Given the repo's current pattern is all-markdown notes, a separate release/host for the .pptx (or a GitHub Release attached to this repo) is probably cleaner than committing a binary alongside it — but this is Kevin's call, not decided yet.
- **Whether the repo needs a pass to make it presentation-ready before the QR codes point an audience at it.** It's already public and has a README, but it was written as a working notes repo (unverified-source callouts, personal asides like "Kevin:" notes) rather than as a polished companion site. Worth a look before 30 Sep, even if nothing structural changes.

## Draft QR placement, by section

| Section | Slide | QR target | Status |
|---|---|---|---|
| 3 | Approach 1 — Manual | [Migrating from Azure Pipelines to GitHub Actions](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines) | Ready — verified doc link |
| 3 | Approach 2 — Tooling | `gh-ado2gh` and `gh-actions-importer` GitHub repos | Ready — verify exact repo URLs before printing (see note in [`01-tooling.md`](../mechanics/01-tooling.md)) |
| 3 | ELM (dedicated slide) | [Introduction to Enterprise Live Migrations](https://learn.microsoft.com/en-us/azure/devops/repos/enterprise-live-migrations/overview?view=azure-devops) | Ready — verified doc link |
| 3 | Approach 3 — AI | [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub) `prompts/` folder | Folder created, 3 prompts drafted — **not yet tested against a real pipeline** |
| 6 | Links & QR codes (consolidated) | Master list — every link used above, plus [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub) itself | Ready to build once the prompts folder exists |

Candidates for additional QR codes elsewhere in the deck, not yet committed to a specific slide:

- Section 1 — the GitHub Copilot app doc, if the Copilot capability list slide wants one: <https://docs.github.com/en/copilot/concepts/agents/github-copilot-app>
- Section 2 — GitHub Packages vs. Azure Artifacts docs, on the Packages/Artifacts decision slide
- Section 4 — [azure-devops-migration-tools](https://github.com/nkdAgility/azure-devops-migration-tools), on the "what you lose migrating work items" or recommendation slide
- Section 5 — the source article behind the disciplined-selection framing, if it's citable on slide (see [`case/03-decision-framework.md`](../case/03-decision-framework.md) for the source link and Kevin's note about needing to properly source or paraphrase certain quotes)

## Open items

- **Test all three prompts against a real `azure-pipelines.yml`** — this is now the only blocker on the AI-approach QR target and the consolidated links slide. See [`../prompts/README.md`](../prompts/README.md) for which repo to use (same open question as the screenshot walkthrough).
- **Verify every QR-target URL right before the talk**, not just at outline time — a 404 on stage during a live QR scan is a worse look than not having the QR code at all.
- **Test-scan every QR code from a printed/projected slide**, not just on a laptop screen — size and contrast that work on a monitor don't always work projected across a conference room.
- **Decide whether the repo needs a presentation-readiness pass** (see above) before the audience is pointed at it live.

## Related

- [`06-slide-deck-outline.md`](06-slide-deck-outline.md) — where each QR-coded slide sits in the deck
- [`../mechanics/07-migration-approaches.md`](../mechanics/07-migration-approaches.md) — the AI approach that needs the prompts repo
- [`03-open-questions.md`](03-open-questions.md) — still-open decisions this plan depends on or adds to
