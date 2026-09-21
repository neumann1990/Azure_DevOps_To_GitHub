---
title: Slide content outline (pre-build review)
status: draft
tags: [session, outline, slides, content, review]
updated: 2026-09-21
---

**In one line:** High-level content for every slide in the deck — 6 sections, 57 section slides + a 10-minute final Q&A, 82.5 + 10 = 92.5 minutes. **Sections 1, 3, and 4 are now built** (not just outlined); their entries below reflect the actual .pptx, not the pre-build plan.

This is content, not copy — bullets to review and correct, not final on-slide wording. Anything still open is marked `[OPEN]`. See [`06-slide-deck-outline.md`](06-slide-deck-outline.md) for the timing/slide-count rationale this content fills in.

---

## Section 1 — Why Leave the Herd (15 min, 11 slides — BUILT)

Status: built and QA'd (font sizes bumped for auditorium legibility; see delivered `.pptx`). This entry reflects the actual deck, which grew by two slides and two minutes past the pre-build plan — see [`06-slide-deck-outline.md`](06-slide-deck-outline.md#what-changed-from-the-previous-draft) for why.

**1. Title + tagline**
"Azure DevOps to GitHub Enterprise: The Great Migration." Tagline: _"Observe the DevOps Engineer in their natural habitat."_

**1.5. Thank you to sponsors**
Boilerplate sponsor thank you slide.

**2. Agenda + "Trails We're Not Hiking"**
Six legs of the expedition, roughly 15 min each. Right panel reframed from "the two debates I'm not having" into expedition-themed copy: not debating GitHub vs. other CI/CD platforms, or Copilot vs. other AI tools — destination is chosen, this talk is the journey. Many aspects of the journey could apply to migrating to other CI/CD platforms.

**3. Opener card — "Migration Season Has Begun"**
Full-bleed nature photography, documentary voice delivers the line live.

**4. "The Honest Primary Driver" — why migrate, the AI angle**
Rewritten as one flowing paragraph plus two comparison pill-cards (GitHub: "Full agentic Copilot suite, shipping now" / Azure DevOps: "AI features arriving, roadmap still catching up") rather than three disjointed text blocks. Every dollar of Copilot investment (Chat, Coding Agent, Autofix, Agentic Code Review, Agent HQ) has landed on GitHub first; Microsoft is adding AI to Azure DevOps too, just not as quickly or as feature-complete yet. If AI-assisted development matters at scale, repos need to live where the AI lives now.

**5. "Copilot's Head Start on GitHub"**
Replaces the originally-planned flat "GitHub-exclusive" bullet list. Fact-checking (prompted by Kevin, since Azure DevOps now exposes its own MCP server to Copilot) found the exclusivity claim didn't hold for 3 of 5 capabilities. Now a native comparison table — Capability / On GitHub / On Azure DevOps — covering Copilot Chat, Coding Agent, Autofix, Agentic Code Review, and Agent HQ, with a full-width note below acknowledging "the gap is real, but closing" and a QR to `github.com/microsoft/azure-devops-mcp`.

**6. "The Terrain Changed Since I Proposed This Talk" — NEW, not in original plan**
Added per Kevin's explicit request. A 5-point horizontal timeline (Nov 2024: Anthropic introduces MCP → Mar–Apr 2025: OpenAI and Google DeepMind adopt it → Jun 2025: Microsoft ships the Azure DevOps MCP Server public preview → Sep 2025: the official MCP registry launches in preview → Dec 2025: Anthropic donates MCP governance to the Linux Foundation's Agentic AI Foundation), with two field-cards: one on how MCP opens doors beyond CI/CD platform migration entirely, and a self-aware note that the talk's own premise shifted underneath it since it was proposed. Plain-text URL to `modelcontextprotocol.io` (no QR — slide was already visually dense).

**7. "A Split in Purpose, Not a Replacement"**
Not a replacement — a split in purpose. Azure DevOps has an active roadmap through 2026+. Microsoft's own framing: GitHub for AI-native development, Azure DevOps for enterprise orchestration (Boards, Test Plans, release governance).

**8. "The Hybrid Pattern — Microsoft's Own Recommendation"**
Redesigned into 3 icon-badge columns (Developers / Managers / Budget) instead of one big dark block, per Kevin's feedback that the original looked "cobbled together." Move source code to GitHub, keep Azure Boards for planning. Developers get GitHub + Copilot; managers keep sprint planning and Power BI. GHEC includes free Azure DevOps Basic access. This is the shape the rest of the talk builds toward, not a compromise.

**9. "And the Non-AI Reasons, for Completeness"**
Grew from 3 stat-cards to a 5-item list, per Kevin's request. Original three: 100M+ developers already on GitHub; 20,000+ community Actions vs. a smaller Azure Pipelines task catalogue; open-source/external contributors already default to GitHub. Two new: GitHub Actions' flexibility (reusable workflows, matrix builds, marketplace, self-hosted runners), and running a workflow locally to troubleshoot (tools like `act` execute a specific Actions definition on your own machine, no hosted-runner queue).

**10. Q&A pocket**

---

## Section 2 — A Field Guide to the Local Species (10 min, 8 slides — BUILT)

Status: built and QA'd, matches this plan's slide count and order exactly. Two notes from the build: the scorecard's "Boards" row landed as a `NEEDS A DECISION` verdict (hybrid — connect it, don't migrate it) rather than a flat red, since section 4 resolves it as a decision, not a dead end; and the Dashboards slide deliberately avoids naming a specific GitHub feature ("GitHub's built-in engineering metrics," not a product name) until the `[OPEN]` verification below is resolved.

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

## Section 3 — Crossing the River (16.5 min, 12 slides — BUILT, one slide is a placeholder)

Status: built and QA'd. Revised from the first build: tooling is now two dedicated slides instead of one, the old standalone sequencing-rule slide is folded into a new `gh-ado2gh` caveats slide, and the walkthrough slide is now a real, screenshot-free timeline. **Only slide 11 (the takeaways) is not real content yet** — see the `[OPEN]` note below and in [`06-slide-deck-outline.md`](06-slide-deck-outline.md#what-changed-from-the-previous-draft).

**1. Opener card — "Rare Footage of Successful Deployment"**

**2. Pipelines: needs a rewrite — the core problem**
Both YAML. That's where the resemblance ends — different concepts underneath (stages/jobs/tasks vs. workflows/jobs/steps). Budget 1–2 days per complex pipeline.

**3. Three ways to cross the river: Manual, Tooling, AI**
Framework slide introducing the three approaches this section walks — a mental model, not a flat mechanics dump.

**4. Approach 1 — Manual** `[QR: migrate-from-azure-pipelines docs]`
Concept mapping table (Pipeline→Workflow, Agent Pool→Runner, Service Connection→OIDC/secrets, Variable Group→secrets/variables, Task→Action, `condition`→`if`, `dependsOn`→`needs`, stages→separate workflow files). Key syntax differences: no classic-editor equivalent, explicit job structure always required, script steps consolidate to `run`+`shell`, GitHub Actions fails fast by default (Azure Pipelines doesn't), no stderr-triggers-failure equivalent.

**5. Approach 2 — `gh-ado2gh` (for repos)** `[QR: gh-ado2gh]`
Split out from the old combined "Tooling" slide, per Kevin's request — there was enough content on each tool to earn its own slide. What it does: inventory-report surveys before anything moves, generate-script produces the real migration script, the --all flag also rewires pipelines/creates teams/connects Boards. What it doesn't do: doesn't touch pipeline logic (that's the next tool), doesn't bring Git LFS objects automatically, doesn't decide identity mapping for you. Why choose it: the default answer for repo migration at any real scale — free, official, GitHub-maintained.

**6. `gh-ado2gh` — caveats & the one sequencing rule**
New slide, absorbing the content that used to be its own standalone slide 10: install the Pipelines GitHub App _before_ migrating repos with gh-ado2gh — not optional, otherwise the migration script can't auto-reconfigure pipelines to point at GitHub and it becomes a manual repo-by-repo fix while everyone asks why the build is red. Same ordering constraint applies to identity mapping (plan before first migration — mannequins are created at migration time, section 6 covers the cost of waiting).

**7. Approach 2 — `gh-actions-importer` (for pipelines)** `[QR: gh-actions-importer]`
The other half of the old combined slide. What it does: audit classifies every pipeline as automatable/partial/manual, dry-run previews the converted workflow, converts the automatable parts rather than just diagnosing them. What it doesn't do: doesn't touch repos, the "partial" bucket still needs a human, faithfully translates whatever's already broken in the source. Why choose it: per Kevin's note, the audit breakdown is the single best slide-quantified evidence in the whole PoC — turns "this will take a while" into an actual number.

**8. ELM — the preview service we couldn't PoC**
Continuous sync + scheduled cutover, sub-30-min read-only window at cutover. What it automates (pre-migration checks, org/repo creation, PR/branch-policy sync, Boards connection, pipeline rewiring). What it still requires manually (cleanup, access setup, verification, work-item/wiki/pipeline migration itself). Requires a GHE data-residency tenant Hunter doesn't have — research only, say so plainly on the slide. The honest contrast: the standard GEI CLI already does more than marketing comparisons imply; what ELM genuinely adds is the continuous-sync/scheduled-cutover experience, not a feature list.

**9. Approach 3 — AI** `[QR: neumann1990/Azure_DevOps_To_GitHub, prompts/]`
Prompt-driven mapping: analyze → convert → validate, as three separate prompts rather than one shot. Why three steps: the model that converts shouldn't be the only check on its own conversion. This is where section 1's "AI is the real reason" thesis gets a demonstrable payoff. `[OPEN: none of the three prompts have been run against a real pipeline yet]`

**10. The Crossing, Mapped**
Replaces the old screenshot-walkthrough slide — per Kevin's request, no screenshots at all now, just a four-step horizontal timeline (repo migration with gh-ado2gh → pipeline audit with gh-actions-importer → YAML rewrite using the Approach 1 mapping → first green build, the real finish line). This is real, presentable content: the sequence is the same regardless of which repo runs through it, so unlike the old version it isn't blocked on picking a repo. Closes with a one-line pointer that the next slide is where real, repo-specific findings land once this is actually run.

**11. Key takeaways from the crossing — PLACEHOLDER, not built**
Built as a list of fill-in-the-blank prompts (which task type caused the most rework and did the audit call it correctly; did the "clean" repo turn out clean; how did the "ugly" repo's actual time compare to the 1–2 day estimate; did the AI-prompt approach get tried and how did it compare) rather than invented findings. `[OPEN: depends entirely on slide 10's sequence actually being run against a real repo, which in turn depends on picking one clean repo and one deliberately ugly one — see session/03-open-questions.md]` — fill in once that happens, or cut the slide rather than pad it with generic takeaways.

**12. Q&A pocket**

---

## Section 4 — Sprint Planning in Its Natural Habitat (13 min, 9 slides — BUILT)

Status: built and QA'd, matches this plan's slide count, order, and timing exactly — no open items.

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

## Section 5 — Preventing the Uprising (14 min, 9 slides — BUILT, matches this plan exactly)

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

## Section 6 — The Watering Hole Nobody Told to Move (14 min, 8 slides — BUILT, matches this plan exactly)

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
