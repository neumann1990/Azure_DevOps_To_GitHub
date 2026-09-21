---
title: Slide deck outline
status: draft
tags: [session, outline, slides, timing]
updated: 2026-09-21
---

**In one line:** Slide-by-slide allotment per section, six sections totaling 82.5 minutes (content + interim Q&A pockets), followed by a single 10-minute Q&A block at the end.

## Framing assumption (revised)

Changed from the previous draft: no recorded video walkthrough. Section 3 now uses screenshots plus a high-level narrated walkthrough of the steps, followed by a takeaways slide — cheaper to produce, easier to keep current, and it removes the single biggest fixed-length item in the deck (the old 4-minute video block).

Total shape: 6 sections averaging ~13.75 min each = 82.5 minutes (Section 1 runs 15 min and Section 3 runs 16.5 min, both after slides were added during their builds; the other four sections are unchanged at their planned lengths), each with a small interim Q&A pocket (~1 min) built in, then a single larger 10-minute Q&A block at the end of the 92.5-minute slot. This replaces the earlier "15 min flat per section, Q&A folded in" framing — interim breaks are now brief check-ins rather than full discussion windows, and the discussion happens at the end where there's real room for it.

The cold open is still folded into the front of section 1, and the documentary closer is still folded into the end of section 6, immediately before the final Q&A block.

## Section 1 — Why Leave the Herd (15 min, 11 slides — built, up from the original 13 min / 9 slide plan)

Cold open folded in here. **Built and QA'd; two slides were added during the build that weren't in the original plan** (a sponsor-thanks slide, and a new MCP-timeline slide — see "What changed" below), which is why this section now runs 2 minutes over its original budget.

| # | Slide | ~Min |
|---|---|---|
| 1 | Title + tagline ("Observe the DevOps Engineer in their natural habitat") | 1.0 |
| 1.5 | Sponsor thank-you (added during build) | 0.5 |
| 2 | Agenda + "Trails We're Not Hiking" (reframed from "the two debates I'm not having") | 1.5 |
| 3 | Opener card: "Migration Season Has Begun" | 1.0 |
| 4 | "The Honest Primary Driver" — why migrate, the AI angle | 1.5 |
| 5 | "Copilot's Head Start on GitHub" — comparison table, not a flat exclusivity list (see "What changed") | 1.5 |
| 6 | "The Terrain Changed Since I Proposed This Talk" — MCP timeline (added during build, see "What changed") | 1.5 |
| 7 | "A Split in Purpose, Not a Replacement" — GitHub (AI-native) vs. Azure DevOps (enterprise orchestration) | 1.5 |
| 8 | "The Hybrid Pattern — Microsoft's Own Recommendation" | 1.5 |
| 9 | "And the Non-AI Reasons, for Completeness" — now 5 items, not 3 (see "What changed") | 2.0 |
| 10 | Q&A pocket | 1.0 |

## Section 2 — A Field Guide to the Local Species (10 min, 8 slides — BUILT, matches this plan exactly)

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "A Field Guide to the Local Species" | 1.0 |
| 2 | The scorecard — full reveal, all seven subsystems, three verdicts | 1.5 |
| 3 | Repos: travels clean* — the asterisk (LFS, permissions, branch policy, size limits) | 1.5 |
| 4 | Wiki: travels clean — git repos on both sides | 1.0 |
| 5 | Packages/Artifacts: needs a decision, not a rewrite | 1.5 |
| 6 | Dashboards: partial equivalent — where GitHub's analytics falls short of Power BI | 1.5 |
| 7 | The pattern: file-based survives, database-backed doesn't (sets up sections 3–4) | 1.0 |
| 8 | Q&A pocket | 1.0 |

## Section 3 — Crossing the River (16.5 min, 12 slides — BUILT, revised from the original plan)

Heaviest section — restructured around three migration approaches instead of a flat concept dump, with ELM restored as its own slide (decent content even without a PoC). See [`07-migration-approaches.md`](../mechanics/07-migration-approaches.md) for the source material behind this framing. **Tooling (originally one slide) is now three** — a dedicated `gh-ado2gh` slide, a `gh-ado2gh` caveats/sequencing slide, and a dedicated `gh-actions-importer` slide — and the old screenshot-walkthrough slide is now a screenshot-free timeline map, real content rather than a placeholder. **One slide (11, the takeaways) is still a clearly-labeled placeholder** — see "What changed" below.

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "Rare Footage of Successful Deployment" | 1.0 |
| 2 | Pipelines: needs a rewrite — the core problem (same YAML, different concepts) | 1.0 |
| 3 | Three ways to cross the river: Manual, Tooling, AI | 1.5 |
| 4 | Approach 1 — Manual: concept mapping table + key syntactic differences `[QR: migrate-from-azure-pipelines docs]` | 2.0 |
| 5 | Approach 2 — `gh-ado2gh` (for repos): what it does, doesn't do, and why choose it `[QR: gh-ado2gh]` | 1.5 |
| 6 | `gh-ado2gh` — caveats & the one sequencing rule: install the Pipelines GitHub App *before* migrating repos | 1.0 |
| 7 | Approach 2 — `gh-actions-importer` (for pipelines): what it does, doesn't do, and why choose it `[QR: gh-actions-importer]` | 1.5 |
| 8 | ELM — the preview service Hunter couldn't PoC, and what it actually adds over standard tooling | 1.5 |
| 9 | Approach 3 — AI: prompt-driven pipeline→workflow mapping rules `[QR: neumann1990/Azure_DevOps_To_GitHub, prompts/]` | 2.0 |
| 10 | The Crossing, Mapped — four-step timeline (repo migration → pipeline audit → YAML rewrite → first green build), no screenshots needed | 1.0 |
| 11 | Key takeaways from the crossing | 1.0 |
| 12 | Q&A pocket | 0.5 |

## Section 4 — Sprint Planning in Its Natural Habitat (13 min, 9 slides — BUILT, matches this plan exactly)

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "Watch as the Scrum Master Approaches Carefully" | 1.0 |
| 2 | Boards: clings to the doorframe — where the gap is widest | 1.5 |
| 3 | Azure Boards' strengths (hierarchy, capacity, Delivery Plans, Power BI) | 1.5 |
| 4 | GitHub Projects' strengths (lightweight, dev-proximity, custom fields) | 1.5 |
| 5 | What you lose migrating work items (sprint history, capacity, process fields) | 1.5 |
| 6 | Test Plans: stays behind — no GitHub equivalent, full stop | 1.5 |
| 7 | The hybrid pattern as the resolution, not the compromise | 1.5 |
| 8 | Recommendation: connect Boards, don't migrate work items | 1.5 |
| 9 | Q&A pocket | 1.0 |

## Section 5 — Preventing the Uprising (14 min, 9 slides — BUILT, matches this plan exactly)

**Built and QA'd; no deviations from the original plan** — all 9 slides match the outline below as written, no slides added or removed, no restructuring.

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "The Senior Engineer Defends an Ancient Pipeline" | 1.0 |
| 2 | Thesis: this is change management wearing an engineering costume | 1.5 |
| 3 | The disciplined selection process (must-haves → pilot → weighted rubric) | 2.0 |
| 4 | Run the pilot first — delay customization until after | 1.5 |
| 5 | Don't judge on sticker price alone | 1.5 |
| 6 | The migration sequence *is* the change-management plan (hybrid → waves → incremental → leave work items) | 2.0 |
| 7 | AI payoff needs structured work items first | 1.5 |
| 8 | Match the tool to context, not the trend — with a documentary aside on the ancient-pipeline defense | 2.0 |
| 9 | Q&A pocket | 1.0 |

## Section 6 — The Watering Hole Nobody Told to Move (14 min, 8 slides — BUILT, matches this plan exactly)

**Built and QA'd; no deviations from the original plan** — all 8 slides match the outline below, custom-built closer and thank-you slides (no `addQAPocket`/`addContentSlide` fit those two shapes). Documentary closer folded in here. No interim Q&A pocket — flows directly into the final Q&A block. Now carries the master links/QR slide — see [`07-qr-and-links-plan.md`](07-qr-and-links-plan.md).

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "The Watering Hole Nobody Told to Move" | 1.0 |
| 2 | The long tail: hardcoded Azure DevOps URLs, everywhere you didn't check | 2.0 |
| 3 | The mannequins nobody claimed — identity's long tail, played for a beat | 3.0 |
| 4 | The unglamorous truth: most migrations aren't a disaster movie | 1.5 |
| 5 | Takeaways recap across all six sections | 2.0 |
| 6 | Links & QR codes — every tool, doc, and the public repo (neumann1990/Azure_DevOps_To_GitHub) `[QR: master list]` | 2.0 |
| 7 | Closer: documentary line over somebody's inherited 2016 pipeline | 1.5 |
| 8 | Thank you — hand off to open floor | 1.0 |

## Final Q&A (10 min)

Standalone block, not folded into any section. This is where the banked discussion time lives — the interim pockets above are brief check-ins, not full Q&A windows.

## Totals

| | |
|---|---|
| Sections | 6 |
| Section slides | 57 (Section 1 built at 11, up from the planned 9; Section 3 built at 12, up from the planned 11 — see "What changed") |
| Section time | 82.5 min |
| Final Q&A | 10 min |
| **Total** | **92.5 min** (2.5 min over the original 90-minute slot — see "What changed") |
| Avg. time per slide | ~1.5 min |
| QR-coded slides | 6 (sec 3 now ×4 — manual docs, gh-ado2gh, gh-actions-importer, and the AI-prompts repo, up from ×3 now that tooling is two slides instead of one; sec 6 ×1 consolidated; plus source list in [`07-qr-and-links-plan.md`](07-qr-and-links-plan.md)) — Section 1's QR (Azure DevOps MCP Server repo) was dropped from the build in favor of a plain text URL on a text-dense slide, so it isn't counted here |

## What changed from the previous draft

- **Section 3 revised again: tooling split into two slides, the sequencing rule moved, and the walkthrough slide no longer needs screenshots.** Kevin's review of the first build found the combined "Tooling" slide had enough content in `gh-ado2gh` and `gh-actions-importer` separately to earn their own slides. It's now three: a `gh-ado2gh` slide (what it does / doesn't do / why choose it), a `gh-ado2gh` caveats slide that absorbed the old standalone "sequencing rule" slide (install the Pipelines GitHub App before migrating repos, plus the identity-mapping note), and a `gh-actions-importer` slide with the same what/doesn't/why structure. Separately, the old screenshot-walkthrough slide is now "The Crossing, Mapped" — a four-step timeline (repo migration → pipeline audit → YAML rewrite → first green build) that needs no screenshots and isn't blocked on picking a repo, since the sequence is the same regardless of which repo runs through it. **Only the takeaways slide (11) is still a placeholder** — it genuinely depends on running that sequence against a real repo (still an open item, see [`03-open-questions.md`](03-open-questions.md), "one clean repo and one deliberately ugly one"). Net effect: section 3 grew from 11 to 12 slides and from 16 to 16.5 minutes, and dropped from two placeholder slides to one.
- **Section 1 built at 11 slides / 15 min, up from the planned 9 slides / 13 min.** Two slides were added that weren't in this outline: a sponsor thank-you slide right after the title, and a new MCP-timeline slide ("The Terrain Changed Since I Proposed This Talk") covering how MCP servers have opened new avenues since this talk was proposed — added per Kevin's explicit request once Azure DevOps's own MCP server made a fact-check on the Copilot-capability slide necessary. The 2-minute overage is absorbed into the overall 90→92 min total rather than cut from elsewhere; revisit if the full deck needs to come back to 90.
- **The "GitHub-exclusive Copilot capabilities" slide became a comparison table.** Fact-checking it (Kevin's request, prompted by Azure DevOps's MCP server) found 3 of the original 5 "exclusive" capabilities weren't actually exclusive — Autofix, Agentic Code Review, and Copilot Chat (via MCP) all have Azure DevOps paths now. The slide is now "Copilot's Head Start on GitHub," an honest three-column table (Capability / On GitHub / On Azure DevOps), not a flat exclusivity list.
- **The non-AI-reasons slide grew from 3 items to 5.** Added GitHub Actions' flexibility (reusable workflows, matrix builds, marketplace, self-hosted runners) and running a workflow locally to troubleshoot (tools like `act`), per Kevin's request.
- **No recorded video walkthrough.** Section 3's old 4-minute video block is now a screenshot-based walkthrough (3.5 min) plus a dedicated takeaways slide (1.5 min) — similar total time, but far cheaper to produce and keep current, and it removes the deck's single point of AV risk (a video that could fail to play, run long, or need re-recording if the product UI changes before 30 Sep).
- **Q&A restructured.** Interim pockets shrank to ~1 minute each (a breath, not a discussion), and the 15 minutes freed up moved into a single 10-minute block at the end plus a bit of headroom redistributed into content (sections 1, 3, and 6 picked up extra minutes).
- **Section 6 no longer has its own interim pocket** — it flows straight from the closer into the final Q&A, since stopping for a 1-minute pocket right before the big discussion window would be an odd beat.

## Open items this outline surfaces

- **The public repo question is resolved.** The QR/links repo is this same notes repo — [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub), confirmed public. No separate repo needed.
- **The AI prompts are drafted, not yet tested.** All three (`analyze`, `convert`, `validate`) exist in the `prompts/` folder in this repo. None have been run against a real pipeline yet — same blocker as picking the repo(s) for the screenshot walkthrough below. See [`07-migration-approaches.md`](../mechanics/07-migration-approaches.md).
- **ELM stays research-only, not a demo.** Restored as its own slide because there's real content (continuous sync, scheduled cutover, what it adds over the standard GEI CLI), but Hunter still can't PoC it — say so on the slide rather than implying it was tested.
- **The two war-story/confession placeholders are gone.** The PoC hasn't gone past basic testing of the three approaches, so there's no real anecdote to tell yet — rather than fabricate one, section 5 slide 8 now covers "match the tool to context, not the trend" (a real, sourced point that hadn't made it onto a slide) with a short documentary-voice humor beat, and section 6 slide 3 now covers the mannequins/identity long tail (also real, sourced, previously unused) with its own beat. Revisit if a genuine anecdote turns up before 30 Sep.
- **The screenshot walkthrough in section 3 needs actual screenshots.** Decide which repo(s) to use for them — this was already an open item in [`03-open-questions.md`](03-open-questions.md) ("one clean repo and one deliberately ugly one"), and it matters more now since there's no video to fall back on if a screenshot doesn't tell the story on its own.
- **10 minutes of final Q&A is a real commitment.** If the room is quiet, that's 10 minutes of dead air with nothing planned — worth having a "here's what people usually ask" backup slide or two in reserve, not part of the main flow but ready if needed.

## Related

- [`04-section-outline.md`](04-section-outline.md) — the six-section structure and opener cards this builds on
- [`05-timing-draft-script.md`](05-timing-draft-script.md) — why the current notes underfill these minutes today
- [`03-open-questions.md`](03-open-questions.md) — Q&A-between-sections decision this outline builds on, and the still-open question of which repos to use for the walkthrough
