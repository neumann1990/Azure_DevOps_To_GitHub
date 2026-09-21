---
title: Open questions
status: verified
tags: [session, decisions, blockers]
updated: 2026-09-04
---

**In one line:** Everything still undecided or blocked, in rough order of how much else depends on it.

## Blocking other work

**2. Budget the 75 minutes.**
Roughly 15 minutes per section leaves room for opener, takeaways and slack. This is the checkpoint that reveals whether the PoC produced enough material for each section.

**3. Write the two remaining section opener cards.**
Four of six section slots now have a card (see [`04-section-outline.md`](04-section-outline.md)). Two drafts proposed — "A Field Guide to the Local Species" (section 2) and "The Tracking Collar Still Points to the Old Watering Hole" (section 6) — need Kevin's sign-off on tone. → [`02-narrative-and-theme.md`](02-narrative-and-theme.md)

## Blocked externally

**4a. The AI migration prompts are drafted but untested.**
Three prompts (analyze, convert, validate) now live in a `prompts/` folder in this repo — [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub). None have been run against a real pipeline yet. That's the same blocker as picking repos for the screenshot walkthrough below — solving one likely solves both. → [`../mechanics/07-migration-approaches.md`](../mechanics/07-migration-approaches.md)

**4. ELM cannot be trialled.**
Enterprise Live Migrations requires a GitHub Enterprise Cloud with data residency tenant. Hunter doesn't have one. Covered as research, not demo. Worth asking whether a vendor walkthrough or recorded demo is available — four weeks out is already tight. → [`mechanics/03-enterprise-live-migrations.md`](../mechanics/03-enterprise-live-migrations.md)

## Smaller, still open

- **Which repos to use for the recorded walkthroughs.** Needs one clean repo and one deliberately ugly one.
- **Whether to show the Azure Artifacts → GitHub Packages path at all,** or just name it and move on.
- **Re-check every price on [`case/04-pricing.md`](../case/04-pricing.md).** The figures came from a third-party comparison site and are already dated.

## Answered

- ~~Session length~~ → 90 minutes, ~75 content + Q&A.
- ~~Live demo?~~ → No. Recorded walkthroughs.
- ~~Full narration or section openers only?~~ → **Section openers and transitions only.** Technical content played straight. Decided 4 Sep 2026. → [`02-narrative-and-theme.md`](02-narrative-and-theme.md)
- ~~Write the slide outline?~~ → **Six sections mapped, following the scorecard's difficulty gradient.** → [`04-section-outline.md`](04-section-outline.md)
- ~~Where does the public repo for QR codes/prompts/the .pptx live?~~ → **This same notes repo** — [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub), confirmed public. Decided/confirmed 21 Sep 2026.
- ~~Q&A placement?~~ → **Between sections, not banked for the end.** A Q&A break lands before an opener card, not after. Decided 20 Sep 2026.
- ~~Deck format?~~ → **PowerPoint (.pptx), designed from scratch** (no existing Hunter-Enterprise template to conform to) — not an interactive HTML doc. Chosen for offline reliability on unknown venue AV, native video embedding for the recorded walkthroughs, and presenter-view speaker notes for the documentary narration lines. Decided 20 Sep 2026.
