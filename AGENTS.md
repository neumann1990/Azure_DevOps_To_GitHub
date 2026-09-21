# Instructions for AI agents

This repository is research and planning material for a conference talk and a migration proof of concept. It is notes, not code.

## Orientation

Read [`README.md`](README.md) first for the folder map, then the file closest to the question. Do not read every file — each one is self-contained and cross-links to its neighbours.

Fastest routes:

- "What happens to <subsystem>?" → [`subsystems/00-scorecard.md`](subsystems/00-scorecard.md), then the specific file
- "How do I run the migration?" → [`mechanics/06-gei-repo-migration-runbook.md`](mechanics/06-gei-repo-migration-runbook.md) is the authoritative step-by-step, taken from GitHub's official six-part guide. Prefer it over any command or limit stated elsewhere in these notes.
- "Why migrate at all?" → [`case/`](case/)
- "What's in the talk?" → [`session/`](session/)
- "What's still undecided?" → [`session/03-open-questions.md`](session/03-open-questions.md)

## Rules

1. **Respect `status` in the frontmatter.** A file marked `unverified` contains claims from marketing sites. Do not repeat its numbers as fact — say where they came from.
2. **Keep the two callout styles intact.** `> **Kevin:**` is his own voice and must never be edited to sound like sourced research. `> ⚠️ **Unverified.**` must never be silently promoted to fact.
3. **Preserve source lines.** Every `Source: <url>` line stays attached to the claim it supports.
4. **Distinguish the two audiences.** Some material is for the PoC (what Hunter will actually do); some is for the talk (what the audience needs to hear). Files say which.
5. **Commands come from the runbook, not from memory.** Several CLI details in these notes were corrected against the official docs on 4 Sep 2026. If a command isn't in [`mechanics/06-gei-repo-migration-runbook.md`](mechanics/06-gei-repo-migration-runbook.md) or explicitly marked verified, treat it as unconfirmed and say so.
6. **Don't fabricate.** If something isn't in these notes, say so rather than filling the gap from general knowledge. Several figures here are already stale or disputed; adding more unsourced claims makes the deck riskier, not richer.

## Known constraints

- Hunter does **not** have GitHub Enterprise Cloud with data residency, so Enterprise Live Migrations (ELM) cannot be trialled. See [`mechanics/03-enterprise-live-migrations.md`](mechanics/03-enterprise-live-migrations.md).
- The session is 90 minutes with no live demo. Recorded walkthroughs carry the proof.
- The documentary theme is **section openers and transitions only** — technical content is played straight. Do not draft narrated copy for body slides. See [`session/02-narrative-and-theme.md`](session/02-narrative-and-theme.md).
- Pricing figures throughout are from a third-party comparison site and predate the current date. Re-check before they go on a slide.
