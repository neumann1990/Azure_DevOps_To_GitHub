---
title: Slide deck outline
status: draft
tags: [session, outline, slides, timing]
updated: 2026-09-21
---

**In one line:** Slide-by-slide allotment per section, six sections totaling 80 minutes (content + interim Q&A pockets), followed by a single 10-minute Q&A block at the end.

## Framing assumption (revised)

Changed from the previous draft: no recorded video walkthrough. Section 3 now uses screenshots plus a high-level narrated walkthrough of the steps, followed by a takeaways slide — cheaper to produce, easier to keep current, and it removes the single biggest fixed-length item in the deck (the old 4-minute video block).

Total shape: 6 sections × ~13.3 min average = 80 minutes, each with a small interim Q&A pocket (~1 min) built in, then a single larger 10-minute Q&A block at the end of the 90-minute slot. This replaces the earlier "15 min flat per section, Q&A folded in" framing — interim breaks are now brief check-ins rather than full discussion windows, and the discussion happens at the end where there's real room for it.

The cold open is still folded into the front of section 1, and the documentary closer is still folded into the end of section 6, immediately before the final Q&A block.

## Section 1 — Why We Left the Herd (13 min, 9 slides)

Cold open folded in here.

| # | Slide | ~Min |
|---|---|---|
| 1 | Title + tagline ("Observe the DevOps Engineer in their natural habitat") | 1.0 |
| 2 | Agenda + the two debates I'm not having | 1.5 |
| 3 | Opener card: "Migration Season Has Begun" | 1.0 |
| 4 | Why migrate — the AI angle (the honest primary driver) | 1.5 |
| 5 | Copilot capability list — GitHub-exclusive features | 1.5 |
| 6 | Platform direction: GitHub (AI-native) vs. Azure DevOps (enterprise orchestration) | 1.5 |
| 7 | The hybrid pattern, per Microsoft's own recommendation | 1.5 |
| 8 | Non-AI reasons (ecosystem, marketplace, integrations) | 1.5 |
| 9 | Q&A pocket | 1.0 |

## Section 2 — A Field Guide to the Local Species (10 min, 8 slides)

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

## Section 3 — Crossing the River (16 min, 11 slides)

Heaviest section — restructured around three migration approaches instead of a flat concept dump, with ELM restored as its own slide (decent content even without a PoC). See [`07-migration-approaches.md`](../mechanics/07-migration-approaches.md) for the source material behind this framing.

| # | Slide | ~Min |
|---|---|---|
| 1 | Opener card: "Rare Footage of Successful Deployment" | 1.0 |
| 2 | Pipelines: needs a rewrite — the core problem (same YAML, different concepts) | 1.0 |
| 3 | Three ways to cross the river: Manual, Tooling, AI | 1.5 |
| 4 | Approach 1 — Manual: concept mapping table + key syntactic differences `[QR: migrate-from-azure-pipelines docs]` | 2.0 |
| 5 | Approach 2 — Tooling: `gh-ado2gh` for repos, `gh-actions-importer` audit breakdown `[QR: gh-ado2gh, gh-actions-importer]` | 2.0 |
| 6 | ELM — the preview service Hunter couldn't PoC, and what it actually adds over standard tooling | 1.5 |
| 7 | Approach 3 — AI: prompt-driven pipeline→workflow mapping rules `[QR: neumann1990/Azure_DevOps_To_GitHub, prompts/]` | 2.0 |
| 8 | Screenshot walkthrough — high-level steps, repo migration to pipeline rewrite | 2.0 |
| 9 | Key takeaways from the walkthrough | 1.0 |
| 10 | Sequencing rule: install the Pipelines GitHub App *before* migrating repos | 1.0 |
| 11 | Q&A pocket | 0.5 |

## Section 4 — Sprint Planning in Its Natural Habitat (13 min, 9 slides)

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

## Section 5 — Preventing the Uprising (14 min, 9 slides)

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

## Section 6 — The Watering Hole Nobody Told to Move (14 min, 8 slides)

Documentary closer folded in here. No interim Q&A pocket — flows directly into the final Q&A block. Now carries the master links/QR slide — see [`07-qr-and-links-plan.md`](07-qr-and-links-plan.md).

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
| Section slides | 54 |
| Section time | 80 min |
| Final Q&A | 10 min |
| **Total** | **90 min** |
| Avg. time per slide | ~1.5 min |
| QR-coded slides | 5 (sec 3 ×3, sec 6 ×1 consolidated, plus source list in [`07-qr-and-links-plan.md`](07-qr-and-links-plan.md)) |

## What changed from the previous draft

- **No recorded video walkthrough.** Section 3's old 4-minute video block is now a screenshot-based walkthrough (3.5 min) plus a dedicated takeaways slide (1.5 min) — similar total time, but far cheaper to produce and keep current, and it removes the deck's single point of AV risk (a video that could fail to play, run long, or need re-recording if the product UI changes before 30 Sep).
- **Q&A restructured.** Interim pockets shrank to ~1 minute each (a breath, not a discussion), and the 15 minutes freed up moved into a single 10-minute block at the end plus a bit of headroom redistributed into content (sections 1, 3, and 6 picked up extra minutes).
- **Section 6 no longer has its own interim pocket** — it flows straight from the closer into the final Q&A, since stopping for a 1-minute pocket right before the big discussion window would be an odd beat.

## Open items this outline surfaces

- **The public repo question is resolved.** The QR/links repo is this same notes repo — [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub), confirmed public. No separate repo needed.
- **The AI prompts still need to be written.** Section 3's AI approach slide links to a `prompts/` folder in that repo that doesn't exist yet. See [`07-migration-approaches.md`](../mechanics/07-migration-approaches.md).
- **ELM stays research-only, not a demo.** Restored as its own slide because there's real content (continuous sync, scheduled cutover, what it adds over the standard GEI CLI), but Hunter still can't PoC it — say so on the slide rather than implying it was tested.
- **The two war-story/confession placeholders are gone.** The PoC hasn't gone past basic testing of the three approaches, so there's no real anecdote to tell yet — rather than fabricate one, section 5 slide 8 now covers "match the tool to context, not the trend" (a real, sourced point that hadn't made it onto a slide) with a short documentary-voice humor beat, and section 6 slide 3 now covers the mannequins/identity long tail (also real, sourced, previously unused) with its own beat. Revisit if a genuine anecdote turns up before 30 Sep.
- **The screenshot walkthrough in section 3 needs actual screenshots.** Decide which repo(s) to use for them — this was already an open item in [`03-open-questions.md`](03-open-questions.md) ("one clean repo and one deliberately ugly one"), and it matters more now since there's no video to fall back on if a screenshot doesn't tell the story on its own.
- **10 minutes of final Q&A is a real commitment.** If the room is quiet, that's 10 minutes of dead air with nothing planned — worth having a "here's what people usually ask" backup slide or two in reserve, not part of the main flow but ready if needed.

## Related

- [`04-section-outline.md`](04-section-outline.md) — the six-section structure and opener cards this builds on
- [`05-timing-draft-script.md`](05-timing-draft-script.md) — why the current notes underfill these minutes today
- [`03-open-questions.md`](03-open-questions.md) — Q&A-between-sections decision this outline builds on, and the still-open question of which repos to use for the walkthrough
