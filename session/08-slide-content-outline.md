---
title: Slide content outline (pre-build review)
status: draft
tags: [session, outline, slides, content, review]
updated: 2026-09-21
---

**In one line:** High-level content for every slide in the deck, for review before the .pptx gets built — 6 sections, 54 section slides + a 10-minute final Q&A, 80 + 10 = 90 minutes.

This is content, not copy — bullets to review and correct, not final on-slide wording. Anything still open is marked `[OPEN]`. See [`06-slide-deck-outline.md`](06-slide-deck-outline.md) for the timing/slide-count rationale this content fills in.

---

## Section 1 — Why Leave the Herd (13 min, 9 slides)

**1. Title + tagline**
"Azure DevOps to GitHub Enterprise: The Great Migration." Tagline: _"Observe the DevOps Engineer in their natural habitat."_

**1.5. Thank you to sponsors**
Boilerplate sponsor thank you slide.

**2. Agenda + the two debates I'm not having**
Six legs of the expedition, roughly 15 min each. Not debating GitHub vs. other CI/CD platforms, or Copilot vs. other AI tools — destination is chosen, this talk is the journey. Many aspects of the journey could apply to migrating to other CI/CD platforms.

**3. Opener card — "Migration Season Has Begun"**
Full-bleed nature photography, documentary voice delivers the line live.

**4. Why migrate — the AI angle**
The honest primary driver: every dollar of Copilot investment (Chat, Coding Agent, Autofix, Agentic Code Review, Agent HQ) lands on GitHub, none on Azure DevOps. If AI-assisted development matters at scale, repos need to live where the AI lives. Also call out the direction of the industry from an AI perspective.

**5. Copilot capability list — GitHub-exclusive** `[QR: GitHub Copilot app docs]`
Bullet list of the GitHub-only capabilities named above, plus the Copilot desktop app as the agent-orchestration surface.

**6. Platform direction: GitHub (AI-native) vs. Azure DevOps (enterprise orchestration)**
Not a replacement — a split in purpose. Azure DevOps has an active roadmap through 2026+. Microsoft's own framing: GitHub for AI-native dev, Azure DevOps for enterprise orchestration (Boards, Test Plans, release governance).

**7. The hybrid pattern, per Microsoft's own recommendation**
Move source code to GitHub, keep Azure Boards for planning. Developers get GitHub + Copilot; managers keep sprint planning and Power BI. GHEC includes free Azure DevOps Basic access. This is the shape the rest of the talk builds toward, not a compromise.

**8. Non-AI reasons**
100M+ developers already on GitHub. 20,000+ community actions vs. a smaller Azure Pipelines task catalogue. Open-source/external contributors are already there.

**9. Q&A pocket**

---

## Section 2 — A Field Guide to the Local Species (10 min, 8 slides)

**1. Opener card — "A Field Guide to the Local Species"**

**2. The scorecard — full reveal**
All seven subsystems, three verdicts (🟢 travels clean / 🟡 needs a decision or rewrite / 🔴 stays behind), one visual. This is the taxonomy-card device from the theme doc — species classifications for subsystems.

**3. Repos: travels clean\* — the asterisk**
Git is git — commit history, PRs, most branch policies migrate. What doesn't: repo permissions (rebuilt as two GitHub teams per team project), Git LFS objects, user-scoped/cross-repo branch policies, TFVC (convert first), anything changed mid-migration (no delta support). Four hard size limits (2 GiB/commit, 2 GiB/push, 255 bytes/ref, 100 MiB/file, 40 GiB/repo). Everything arrives **private** regardless of source visibility.

**4. Wiki: travels clean**
Both are Git repos under the hood — clone-and-push. What's lost: Azure DevOps' richer permissions and its tight Boards/pipeline integration. Kevin's note: content migration is trivial, permissions is the whole conversation.

**5. Packages/Artifacts: needs a decision, not a rewrite**
Three paths: keep Azure Artifacts, move to GitHub Packages, or both during transition. Recommended PoC target: prove path 1 (Actions publishing to an existing Azure Artifacts feed) — the realistic answer for teams that can't repoint every consumer at cutover.

**6. Dashboards: partial equivalent**
GitHub's engineering analytics covers delivery performance, cycle time, PR review load — DORA-metric-adjacent. Doesn't match Boards Analytics + Power BI depth. Framing: use the four DORA metrics as the shared baseline language rather than comparing dashboard widgets. `[OPEN: verify "GitHub Analytics" feature name/availability on Hunter's actual plan before this goes on a slide — flagged unverified in source notes]`

**7. The pattern**
File-based, version-controlled things travel well (repos, wiki). Database-backed enterprise tooling doesn't (dashboards here; boards and test plans coming up next). This line is the whole talk in one sentence — sets up sections 3–4.

**8. Q&A pocket**

---

## Section 3 — Crossing the River (16 min, 11 slides)

**1. Opener card — "Rare Footage of Successful Deployment"**

**2. Pipelines: needs a rewrite — the core problem**
Both YAML. That's where the resemblance ends — different concepts underneath (stages/jobs/tasks vs. workflows/jobs/steps). Budget 1–2 days per complex pipeline.

**3. Three ways to cross the river: Manual, Tooling, AI**
Framework slide introducing the three approaches this section walks — a mental model, not a flat mechanics dump.

**4. Approach 1 — Manual** `[QR: migrate-from-azure-pipelines docs]`
Concept mapping table (Pipeline→Workflow, Agent Pool→Runner, Service Connection→OIDC/secrets, Variable Group→secrets/variables, Task→Action, `condition`→`if`, `dependsOn`→`needs`, stages→separate workflow files). Key syntax differences: no classic-editor equivalent, explicit job structure always required, script steps consolidate to `run`+`shell`, GitHub Actions fails fast by default (Azure Pipelines doesn't), no stderr-triggers-failure equivalent.

**5. Approach 2 — Tooling** `[QR: gh-ado2gh, gh-actions-importer]`
`gh-ado2gh` for repos (inventory-report, generate-script, the `--all` flag for pipeline rewiring/team creation/Boards integration). `gh-actions-importer audit` gives the automatable/partial/manual breakdown per pipeline — per Kevin's note, the single best slide-quantified evidence in the whole PoC.

**6. ELM — the preview service we couldn't PoC**
Continuous sync + scheduled cutover, sub-30-min read-only window at cutover. What it automates (pre-migration checks, org/repo creation, PR/branch-policy sync, Boards connection, pipeline rewiring). What it still requires manually (cleanup, access setup, verification, work-item/wiki/pipeline migration itself). Requires a GHE data-residency tenant Hunter doesn't have — research only, say so plainly on the slide. The honest contrast: the standard GEI CLI already does more than marketing comparisons imply; what ELM genuinely adds is the continuous-sync/scheduled-cutover experience, not a feature list.

**7. Approach 3 — AI** `[QR: neumann1990/Azure_DevOps_To_GitHub, prompts/]`
Prompt-driven mapping: analyze → convert → validate, as three separate prompts rather than one shot. Why three steps: the model that converts shouldn't be the only check on its own conversion. This is where section 1's "AI is the real reason" thesis gets a demonstrable payoff. `[OPEN: none of the three prompts have been run against a real pipeline yet]`

**8. Screenshot walkthrough — high-level steps**
Repo migration → pipeline rewrite, screenshots not video. `[OPEN: which repo(s) — need one clean, one deliberately ugly, per session/03-open-questions.md]`

**9. Key takeaways from the walkthrough**
What actually broke or surprised, in the specific repo(s) used — fill in once the walkthrough is run.

**10. Sequencing rule: install the Pipelines GitHub App _before_ migrating repos**
Not optional — otherwise the migration script can't auto-reconfigure pipelines to point at GitHub, and it becomes a manual repo-by-repo fix while everyone asks why the build is red. Same ordering constraint applies to identity mapping (plan before first migration — mannequins are created at migration time).

**11. Q&A pocket**

---

## Section 4 — Sprint Planning in Its Natural Habitat (13 min, 9 slides)

**1. Opener card — "Watch as the Scrum Master Approaches Carefully"**

**2. Boards: not a easy transplant — where the gap is widest**
Framing slide: Azure Boards is a full enterprise work-tracking system; GitHub Projects is a lightweight kanban board sitting on Issues. Not a feature gap so much as a different tool entirely.

**3. Azure Boards' strengths**
Hierarchical work items (Epics→Features→Stories→Tasks), sprint planning, capacity management, Delivery Plans for cross-team dependencies, Power BI/Analytics reporting. Organizes by Project/Team/Area.

**4. GitHub Projects' strengths**
Lightweight, flexible custom fields (iteration, single-select, date, number), close proximity to actual issues/PRs, fast for small-team daily triage, roadmap layout, built-in or Actions-driven automation. Organizes by Repository/Label/Milestone.

**5. What you lose migrating work items**
Sprint history, capacity data, custom process fields, the whole Project/Team/Area hierarchy. Open-source help exists (`azure-devops-migration-tools`) but expect real manual-mapping time — the data models don't line up.

**6. Test Plans: stays behind — no GitHub equivalent, full stop**
No native GitHub Projects/Issues equivalent for structured manual + exploratory testing. In a regulated environment, this alone can be a reason to keep Azure DevOps in the picture. Kevin's note: shortest section in the deck, probably the best-received — sometimes "it doesn't move, and that's fine" is the honest answer.

**7. The hybrid pattern as the resolution, not the compromise**
Connect Azure Boards to GitHub repos before touching anything else. Developers work in GitHub; managers keep sprint hub, capacity charts, Power BI. Microsoft designed this as the intended shape — reframe internally as "the answer," not "the fallback."

**8. Recommendation: connect Boards, don't migrate work items**
Explicit takeaway slide — don't migrate to GitHub Issues unless PM needs are genuinely simple. Leave the door open to other work planning tooling, if Azure DevOps isn't the right choice.

**9. Q&A pocket**

---

## Section 5 — Preventing the Uprising (14 min, 9 slides)

**1. Opener card — "The Senior Engineer Defends an Ancient Pipeline"**

**2. Thesis: change management wearing an engineering costume**
Migrations that fail, fail on change management, not mechanics — no real selection process, customization started before anyone understood the new tool, or the rollout felt done _to_ people instead of _with_ them.

**3. The disciplined selection process**
Define must-haves → assess current toolchain/data-residency needs → model one real increment in each tool (not a demo) → score with a weighted rubric → run a 4–6 week pilot with measurable outcomes.

**4. Run the pilot first — delay customization until after**
Customizing on day one locks in decisions made by people who didn't understand the tool yet.

**5. Don't judge on sticker price alone**
Compare licensing tiers, GHAS as an add-on, runner/compute minutes, admin/migration effort. Past ~100 engineers, governance/reporting time saved usually outweighs a modest per-seat difference — but run the actual math.

**6. The migration sequence _is_ the change-management plan**
Start hybrid (connect Boards first) → migrate repos in waves, low-stakes first → rewrite pipelines incrementally, old and new in parallel → leave work items alone unless already deliberately decided otherwise.

**7. AI payoff needs structured work items first**
Copilot/agentic tooling only multiplies value when the tickets feeding it are well-structured. Invest in templates and acceptance criteria before expecting the AI payoff — this is a precondition, not a nice-to-have. Ties back to section 1's thesis.

**8. Match the tool to context, not the trend — with a documentary aside**
Startups and one-to-three-squad teams: GitHub Projects' lightweight fit wins. Scaled agile, regulated industries, multi-team portfolios: Azure Boards' hierarchy and reporting earn their keep. Mixed estates: hybrid, deliberately — not a compromise, a fit. Documentary aside, same voice as the opener cards, played for a beat: the Senior Engineer defending the ancient pipeline (this section's opener) isn't wrong to be cautious — they're just defending it with the wrong argument ("it's always worked" instead of "here's the rubric score"). Hear the objection out, then hand them the data.

**9. Q&A pocket**

---

## Section 6 — The Watering Hole Nobody Told to Move (14 min, 8 slides)

**1. Opener card — "The Watering Hole Nobody Told to Move"**

**2. The long tail: hardcoded Azure DevOps URLs**
The single most reliable source of post-migration tickets — scripts, pipeline YAML, IaC, service connections, READMEs, forgotten internal tools. Budget a real sweep, then a second one a month later.

**3. The mannequins nobody claimed — identity's long tail**
Every Azure DevOps user becomes a mannequin at migration time — a placeholder account. Everything except Git commits (issue comments, PR reviews, work-item history) gets attributed to it until someone reclaims it, and only a GitHub organization owner can do the reclaiming. Content stuck on an unreclaimed mannequin may not reliably show up in search either. Documentary beat: a herd of placeholder accounts, grazing quietly in the repo's activity feed at this section's watering hole, waiting for someone to notice they're there. The fix isn't clever — plan the identity mapping before migration, not after; remapping later is the harder path.

**4. The unglamorous truth**
Most migrations aren't a disaster movie — a checklist, run carefully, with a few things that broke in ways nobody predicted and got fixed by people in the room.

**5. Takeaways recap across all six sections**
One line per section: why teams migrate (AI) → what travels clean vs. clings to the doorframe → three ways to rebuild pipelines → why Boards stays hybrid → migration as change management → the long tail that outlasts the cutover.

**6. Links & QR codes** `[QR: master list — neumann1990/Azure_DevOps_To_GitHub]`
Consolidated fallback for anyone who didn't scan one earlier: manual-migration docs, `gh-ado2gh`/`gh-actions-importer`, the AI prompts repo, and the notes repo itself.

**7. Closer**
Documentary line over somebody's inherited 2016 pipeline: _"For some, the city is a place of opportunity. For others, it's a place of danger. But for all of it — it is a world of our making."_

**8. Thank you — hand off to open floor**

---

## Final Q&A (10 min)

Standalone block, not folded into section 6. `[OPEN: consider 1–2 backup slides for common questions in reserve, in case the room is quiet — not part of the main flow but ready if needed]`

---

## Open items this outline surfaces, consolidated

- **War-story placeholders replaced, not filled.** Section 5 slide 8 and section 6 slide 3 no longer wait on a real anecdote — they now carry sourced content (tool-fit guidance; the mannequin/identity long tail) that hadn't made it onto a slide yet, each with a short documentary-voice humor beat. Swap in a genuine story instead if one turns up before 30 Sep.
- **Repo(s) for the screenshot walkthrough** not yet chosen — also blocks testing the AI prompts, since ideally both use the same source material.
- **AI prompts drafted, not yet run** against a real pipeline (section 3, slide 7).
- **Dashboards slide** (section 2, slide 6) cites an unverified third-party feature name ("GitHub Analytics") — confirm against Hunter's actual GitHub plan before it's on a slide.
- **ado2gh / gh-actions-importer exact repo URLs** for the QR codes need verifying right before the talk, not just at outline time.

## Related

- [`06-slide-deck-outline.md`](06-slide-deck-outline.md) — timing and slide count this content fills in
- [`04-section-outline.md`](04-section-outline.md) — the six-section structure and opener cards
- [`03-open-questions.md`](03-open-questions.md) — every `[OPEN]` item above, tracked
- [`../mechanics/07-migration-approaches.md`](../mechanics/07-migration-approaches.md) — full detail behind section 3's three-approach framing
- [`../prompts/README.md`](../prompts/README.md) — the AI prompts referenced in section 3
