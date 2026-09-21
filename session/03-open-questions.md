---
title: Open questions
status: verified
tags: [session, decisions, blockers]
updated: 2026-09-04
---

**In one line:** Everything still undecided or blocked, in rough order of how much else depends on it.

## Blocking other work

**1. Write the slide outline.**
Unblocked — the theme decision is made. Map the abstract's four promises onto sections, and settle on six sections so the six opener cards have homes. → [`01-brief.md`](01-brief.md)

**2. Budget the 75 minutes.**
Roughly 15 minutes per section leaves room for opener, takeaways and slack. This is the checkpoint that reveals whether the PoC produced enough material for each section.

**3. Write two or three more section opener cards.**
Four exist; six sections need six. Same construction: documentary-caption cadence describing ordinary engineering behaviour as animal behaviour. → [`02-narrative-and-theme.md`](02-narrative-and-theme.md)

## Blocked externally

**4. ELM cannot be trialled.**
Enterprise Live Migrations requires a GitHub Enterprise Cloud with data residency tenant. Hunter doesn't have one. Covered as research, not demo. Worth asking whether a vendor walkthrough or recorded demo is available — four weeks out is already tight. → [`mechanics/03-enterprise-live-migrations.md`](../mechanics/03-enterprise-live-migrations.md)

## Smaller, still open

- **Q&A placement.** 90 minutes is long enough to take questions between sections rather than banking all 15 for the end. Decide before writing the outline — it changes section structure, and it interacts with the opener cards (a Q&A break lands naturally *before* an opener, not after).
- **Which repos to use for the recorded walkthroughs.** Needs one clean repo and one deliberately ugly one.
- **Whether to show the Azure Artifacts → GitHub Packages path at all,** or just name it and move on.
- **Re-check every price on [`case/04-pricing.md`](../case/04-pricing.md).** The figures came from a third-party comparison site and are already dated.

## Answered

- ~~Session length~~ → 90 minutes, ~75 content + Q&A.
- ~~Live demo?~~ → No. Recorded walkthroughs.
- ~~Full narration or section openers only?~~ → **Section openers and transitions only.** Technical content played straight. Decided 4 Sep 2026. → [`02-narrative-and-theme.md`](02-narrative-and-theme.md)
