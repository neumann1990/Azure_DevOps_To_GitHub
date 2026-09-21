# Azure DevOps to GitHub Enterprise Presentation

## Prioritized Slide-by-Slide Edit Plan

**Audience:** Mostly senior software engineers  
**Audience size:** 20–100 attendees  
**Target prepared delivery:** 65–72 minutes, plus 10–15 minutes for Q&A  
**Current source deck:** `azure-devops-to-github-the-great-migration-FULL-DECK.pptx`

---

## Priority Definitions

- **P0 — Required before presentation:** Correctness, credibility, unfinished content, or material that could trigger a justified audience challenge.
- **P1 — High-value improvement:** Materially improves technical depth, pacing, clarity, or usefulness.
- **P2 — Polish:** Improves wording, humor, continuity, or delivery without changing the core technical argument.

---

# Global Changes

## P0 — Separate Verified Fact, Firsthand Finding, and Recommendation

Apply a small, consistent label in the speaker notes or at the bottom of applicable slides:

- **Verified capability:** Supported by current product documentation.
- **Observed:** Tested during the proof of concept.
- **Recommendation:** Architectural or migration guidance based on the evidence.
- **Preview / research only:** Not tested firsthand.

This is especially important on slides 6, 17, 21, 27, 28, 30, and 45. Senior SWEs will generally accept uncertainty when it is stated clearly. They are less likely to accept uncertainty presented as certainty.

## P0 — Define “Done” More Rigorously

The current deck treats the first green build as the finish line. Keep it as an important milestone, but define migration acceptance as:

- Repository content reconciled.
- Target visibility and permissions verified.
- Identities mapped.
- Branch protections applied.
- Workflow behavior validated.
- Deployment approvals exercised.
- Artifact and package behavior confirmed.
- Observability and notifications confirmed.
- Rollback procedure documented.
- Legacy repository made read-only or decommissioned according to plan.

## P1 — Reduce Repeated Arguments

The current presentation contains 57 slides, including five interim Q&A slides. The revised target should be:

- **48–51 slides** for a 75–90-minute version.
- **40–43 slides** for a 60-minute version.

The presentation should move more quickly from the platform rationale into the engineering mechanics.

## P1 — Change the Audience Taxonomy

Replace repeated “Developers versus Managers” positioning with:

- **Code-centric workflows**
- **Planning and portfolio workflows**
- **Testing and compliance workflows**
- **Cross-system traceability**

This is more appropriate for staff engineers, architects, SREs, QA engineers, technical leads, and engineering managers who work across those boundaries.

---

# Opening and Agenda

## Slide 1 — Title

**Priority:** P2 — Keep

### Keep

- Title.
- Documentary tagline.
- Cold-open delivery.
- Expedition visual identity.

### Edit

Add one sentence immediately after the cold open:

> This is not a GitHub sales pitch. It is a field report on what transfers, what must be redesigned, and what should deliberately remain in Azure DevOps.

### Reason

This establishes credibility and neutralizes concerns that the conclusion was predetermined.

### Target Delivery

1 minute.

---

## Slide 2 — Sponsor Slide

**Priority:** P1 — Conditional cut

### Action

- Keep only if required by the event.
- Replace the placeholder before the presentation.
- Delete the slide if it is not required.

### Reason

An unresolved placeholder damages polish immediately, while an unnecessary sponsor slide slows the opening.

---

## Slide 3 — Agenda

**Priority:** P1 — Simplify

### Edit

Keep the nature-themed headings, but add plain-language outcomes:

1. **Why move:** What repository location changes.
2. **What migrates:** Data and metadata boundaries.
3. **How pipelines change:** Conversion and validation.
4. **What remains hybrid:** Boards and Test Plans.
5. **How to roll out:** Sequencing and adoption.
6. **What appears later:** Identity, URLs, and decommissioning.

Reduce “Trails We’re Not Hiking” to a single footer:

> Non-goal: comparing GitHub with every competing platform.

Remove the Copilot-versus-other-AI-tools point unless that debate is especially likely with this audience.

### Target Delivery

1–2 minutes.

---

# Section 1 — Strategic Case and Target State

## Slide 4 — Section Opener

**Priority:** P2 — Keep

### Edit

Correct the speaker-note transition that says “move to slide 4.” It should say “move to slide 5.”

### Delivery

Keep the documentary voice, then return immediately to normal delivery.

---

## Slide 5 — Honest Primary Driver

**Priority:** P1 — Revise

### Keep

- AI capability is a major strategic driver.
- GitHub currently receives repository-native agentic capabilities first.

### Change Headline

Replace **“The Honest Primary Driver”** with:

> **Why Repository Location Matters Again**

### Replace Absolute Wording

Use:

> The broadest repository-native Copilot and agentic development experiences are centered on GitHub. Azure DevOps continues to gain AI capabilities, but repository location still determines which workflows are available natively.

### Add Architecture Qualifier

> MCP expands what assistants can reach. It does not make repository-native PR automation, security analysis, workflow controls, and governance independent of the hosting platform.

### Reason

This prepares the audience for slide 7 without allowing MCP to undermine the central migration case.

### Target Delivery

2 minutes.

---

## Slide 6 — Copilot Capability Comparison

**Priority:** P0 — Revalidate and date-stamp

### Required Edits

1. Add a visible date:

   > **Capability status as of September 2026**

2. Verify each row immediately before finalizing:
   - Chat
   - Coding Agent
   - Autofix
   - Agentic Code Review
   - Agent HQ
   - GA versus preview state
   - Product tier and licensing requirements

3. Avoid saying Azure DevOps has an equivalent merely because an assistant can access Azure DevOps through MCP.

4. Add a footer:

   > Preview status, licensing, and repository requirements change quickly. Verify against your tenant before planning around a capability.

### Format Improvement

Use three columns:

- Capability
- GitHub-hosted repository experience
- Azure DevOps-hosted repository experience

### Reason

This is the slide most likely to become obsolete and the one most likely to attract an audience correction.

### Target Delivery

3 minutes maximum. Do not read every cell.

---

## Slide 7 — MCP Timeline

**Priority:** P0 — Add reconciliation

### Keep

The “terrain changed” concept is excellent and intellectually honest.

### Add a Concluding Box

> **What MCP changes:** Agents can reach more systems without custom point-to-point integrations.  
> **What MCP does not change:** Repository-native pull-request, security, workflow, policy, and governance capabilities still depend on where the repository lives.

### Simplify Technical History

Do not narrate every timeline milestone. Use the timeline visually, then spend the spoken time on the implication.

### Optional Humor

> The platform decision did not disappear. It merely acquired more adapters.

### Target Delivery

3 minutes.

---

## Slides 8, 9, and 10 — Purpose Split, Hybrid Pattern, and Non-AI Reasons

**Priority:** P1 — Combine into one slide

### New Slide Title

> **The Target State: GitHub for Repositories, Azure DevOps Where It Still Adds Value**

### Suggested Structure

#### Repository and Code Workflows

- GitHub repositories.
- Pull requests.
- Repository-native Copilot capabilities.
- GitHub Actions where appropriate.
- Security and policy controls.

#### Planning, Portfolio, and Testing Workflows

- Azure Boards where portfolio planning and capacity are needed.
- Azure Test Plans where structured manual testing is needed.
- Azure Pipelines during transition or where retained deliberately.

#### Integration Layer

- Work-item links.
- Commit and PR traceability.
- Pipeline integration.
- Identity and access mapping.

### Retain One Budget Note

> Eligible GitHub Enterprise Cloud users may receive Azure DevOps Basic usage rights through Entra integration. Verify tenant eligibility, Test Plans licensing, Copilot licensing, Advanced Security, and Actions usage separately.

### Remove

- Brittle developer-count claim.
- Exact marketplace count.
- Claim that the hybrid arrangement “costs nothing extra.”
- Persona division between developers and managers.

### Move `act` Content

Move local workflow execution to the pipeline section, where it can be properly qualified.

### Net Effect

Three slides become one, saving approximately four minutes of delivery.

---

## Slide 11 — Q&A Pocket

**Priority:** P1 — Cut

### Action

Delete this slide.

### Delivery Alternative

Say:

> Hold detailed migration questions until the pipeline section. I will pause there.

### Reason

The audience has not yet reached the migration mechanics, where the most valuable questions will arise.

---

# Section 2 — Migration Boundaries

## Slide 12 — Section Opener

**Priority:** P2 — Keep

No structural edit needed.

---

## Slide 13 — Scorecard

**Priority:** P0 — Correct and refine

### Change Repository Explanation

Replace:

> Git is git — history and PRs migrate.

With:

> **Git history moves natively; supported PR metadata and repository-scoped policies move through GitHub Enterprise Importer.**

### Change Wiki Verdict

Replace **“Travels clean”** with:

> **Content travels; behavior needs review**

### Change Pipelines Verdict

Replace **“Needs a decision”** with:

> **Requires conversion and validation**

### Change Boards Verdict

Replace **“Needs a decision”** with:

> **Retain, replace, or migrate deliberately**

### Change Test Plans Explanation

Use:

> **No native GitHub equivalent for structured manual and exploratory test management.**

### Optional Category Labels

- **Portable**
- **Convertible**
- **Retain or replace**
- **No native destination**

These are more precise than “travels clean” versus “stays behind.”

### Target Delivery

2 minutes.

---

## Slide 14 — Repositories

**Priority:** P0 — Correct

### Required Deletion

Remove:

> Every repo arrives private on GitHub, regardless of source visibility.

### Replace With

> **Verify target visibility during the trial migration. Migration configuration, enterprise policy, and account model can affect the final result.**

### Clarify Pull Requests

Separate Git content from importer-supported metadata:

#### Native Git Transfer

- Commits.
- Branches.
- Tags.

#### Importer-Supported Metadata

- Supported pull-request history.
- Supported attachments and links.
- Repository-scoped branch policies.

#### Requires Specific Handling

- Permissions and teams.
- User-scoped and cross-repository policies.
- Identities.
- LFS and large-file cases.
- TFVC conversion.
- Visibility and policy validation.

### Add One Note on Trial Runs

> A trial migration is part of design validation, not merely a rehearsal.

### Target Delivery

3 minutes.

---

## Slide 15 — Wiki

**Priority:** P1 — Revise or merge

### Replace Current Message

Use:

> The underlying Git content is portable. The migration review still needs to cover permissions, links, attachments, navigation, embedded content, and integrations.

### Suggested Takeaway

> **The Markdown is easy. Preserving the user experience is the work.**

### Optional Action

Merge this slide into the scorecard for the 60-minute version.

### Target Delivery

1 minute.

---

## Slide 16 — Packages and Artifacts

**Priority:** P1 — Add decision criteria

### Keep

- Retain Azure Artifacts.
- Move to GitHub Packages.
- Dual-publish temporarily.

### Add Selection Criteria

- Consumer count.
- Package ecosystems.
- Retention requirements.
- Upstream feeds.
- Network access.
- Authentication model.
- Provenance and signing.
- Availability during transition.
- Ownership of the registry after migration.

### Tighten Recommendation

> For a first PoC, prove GitHub Actions can authenticate to, publish to, and consume from the existing feed. Registry consolidation can remain a separate decision.

### Reason

This separates pipeline migration from package-registry migration and reduces scope.

---

## Slide 17 — Dashboards

**Priority:** P0 — Verify or generalize

### Required Action

The current speaker notes mark the GitHub metric feature as unverified. Resolve this before presenting.

### Safe Version if Not Verified

> GitHub provides repository and workflow insights, but do not assume they replace an established Azure Boards Analytics and Power BI reporting estate.

### Keep the DORA Reframe, but Qualify It

> Use delivery metrics as a shared comparison framework, while defining precisely how each metric is calculated in your organization.

### Reason

Even familiar metric names can be calculated differently across tools.

---

## Slide 18 — The Pattern

**Priority:** P0 — Replace taxonomy

### Remove

> File-based and version-controlled survives the crossing. Database-backed enterprise tooling doesn’t.

### Replace With

> **Portable, standards-based artifacts travel best. Platform-specific semantics and data models create the migration work.**

### Examples

#### Usually Most Portable

- Git objects.
- Markdown content.
- Ordinary build scripts.
- Container definitions.

#### Requires Semantic Translation

- Pipeline definitions.
- Approvals and gates.
- Service connections.
- Environment protections.
- Branch policies.

#### Requires Business-Process Decisions

- Work-item models.
- Capacity planning.
- Test management.
- Dashboards and historical reporting.

### Reason

This becomes an architecture principle that senior SWEs can reuse outside this migration.

---

## Slide 19 — Q&A Pocket

**Priority:** P1 — Cut

Move the first formal question pause to the end of the pipeline section.

---

# Section 3 — Repository and Pipeline Conversion

## Slide 20 — Section Opener

**Priority:** P2 — Keep

### Speaker-Note Update

Update any references to the number of slides in the section after the restructure.

---

## Slide 21 — Pipeline Core Problem

**Priority:** P0 — Revise estimate

### Keep

- YAML similarity can create false confidence.
- Concepts and execution semantics differ.

### Replace Absolute Estimate

Replace:

> Budget 1–2 days per complex pipeline.

With:

> **Planning hypothesis: reserve at least one engineering day for a nontrivial pipeline, then recalibrate using the importer audit and one representative migration.**

### Add Complexity Drivers

- Deployment gates.
- Inherited templates.
- Service connections.
- Self-hosted agents.
- Private network access.
- Environment approvals.
- Artifact feeds.
- Custom tasks.
- Condition logic.

### Optional Humor

> Both systems use YAML, in the same way Java and JavaScript both contain “Java.”

Use once, then move on.

---

## Slide 22 — Three Ways to Cross

**Priority:** P1 — Replace framework

### Current Problem

Manual, tooling, and AI are not equivalent migration approaches. They are methods used across different migration layers.

### Replace With a Layered Model

#### Layer 1 — Repository Data

- Git history.
- PR metadata.
- Policies.
- Identities.

#### Layer 2 — Automation Behavior

- Build and deployment semantics.
- Runners.
- Secrets.
- Environments.
- Approvals.

#### Layer 3 — Validation

- Output equivalence.
- Security.
- Deployability.
- Observability.
- Rollback.

### Footer

> Official tooling, manual engineering, and AI assistance can each contribute within these layers.

### Reason

This creates a more accurate mental model for the next slides.

---

## Slide 23 — Manual Mapping

**Priority:** P0 — Correct and deepen

### Revise Mappings

Change:

- **Service Connection → OIDC / secrets**

To:

- **Service connection → OIDC, GitHub App, or managed secret, depending on the target**

Change:

- **Task → Action**

To:

- **Task → Action, script, or reusable workflow**

### Add

- Environment / approval → GitHub environment and protection rules, where equivalent.
- Template → reusable workflow, composite action, or local workflow template.
- Pipeline artifact → uploaded artifact, package, or external registry.

### Remove

> Actions fails fast by default where Pipelines doesn’t.

### Replace With

> **Failure propagation and default execution conditions differ. Validate `if`, `needs`, shell exit handling, matrix behavior, and continue-on-error semantics.**

### Qualify Stages

> The documented migration model may split stages into workflows, but the final design should map each stage to the appropriate job, reusable workflow, environment, or independently governed deployment workflow.

### Add Review Question

> What security or lifecycle boundary did the original stage represent?

### Reason

This encourages design rather than syntax translation.

---

## Slide 24 — `gh ado2gh`

**Priority:** P1 — Keep with terminology refinement

### Change Subtitle

Replace **“For Repos”** with:

> **Repository and Migration Orchestration**

### Explicitly Distinguish

- GitHub Enterprise Importer performs migrations.
- `gh ado2gh` helps inventory, generate, and orchestrate migration commands.
- `--all` adds configuration work such as teams, Boards integration, and pipeline rewiring.

### Add

> Review the generated script. Treat it as migration code, not disposable output.

### Reason

Senior SWEs will appreciate generated artifacts being placed under review and source control.

---

## Slide 25 — Sequencing Rule

**Priority:** P1 — Broaden

### Keep

The GitHub App sequencing point and identity-mapping warning.

### Add a “Before First Migration” Checklist

- Target enterprise and organization model.
- Authentication model.
- Identity mapping.
- Team model.
- Repository naming.
- Visibility policy.
- Boards and Pipelines integration.
- Freeze or change-reconciliation approach.
- Ownership of migration failures.

### Change Slack Reference if Needed

Replace the Slack-specific line with:

> While the team asks why every migrated build is red.

---

## Slide 26 — Actions Importer

**Priority:** P1 — Expand manual-work list

### Keep

- Audit.
- Dry run.
- Conversion.
- Automatable, partial, and manual categorization.

### Add Explicit Manual Areas

- Secrets.
- Service connections.
- Self-hosted agents.
- Environments.
- Approvals and gates.
- Unknown or custom tasks.
- Unsupported triggers.

### Add Deliverable

> Use the audit output to build the migration backlog and effort model.

### Suggested Evidence Box

After conducting the PoC, display:

- Total pipelines audited.
- Automatable count.
- Partial count.
- Manual count.
- Top unsupported construct.

Do not add synthetic numbers.

---

## Slide 27 — Enterprise Live Migrator

**Priority:** P1 — Move to appendix or compress

### Recommendation

Move this slide to the appendix for the main 60–75-minute talk.

### If Retained

Change the title to:

> **Enterprise Live Migrator: Preview Option for Reduced Cutover Disruption**

Put the limitation first:

> Research only. Not tested in our tenant.

Then state only:

- What it adds over the standard approach.
- Tenant or eligibility constraint.
- Remaining manual responsibilities.

### Reason

A preview service that was not exercised provides less main-stage value than runners, rollback, or a real workflow conversion.

---

## New Slide After 27 — Runner and Network Strategy

**Priority:** P1 — Add

### Title

> **The YAML May Convert. The Execution Environment Usually Doesn’t.**

### Decide

- GitHub-hosted versus self-hosted runners.
- Private network access.
- Environment parity.
- Toolchain and cache strategy.
- Ephemeral versus persistent runners.
- Runner groups and repository access.
- Autoscaling.
- Operational ownership.
- Usage cost.

### Validate

- Private endpoints.
- Internal package feeds.
- Signing infrastructure.
- Deployment targets.
- Firewall and proxy rules.
- Credentials or workload identity.
- Artifact performance.

### Humor

> The workflow converted successfully. It merely has no credentials, no network route, and nowhere to deploy.

### Reason

This is one of the highest-value additions for enterprise SWEs.

---

## Slide 28 — AI-Assisted Conversion

**Priority:** P1 — Revise

### Keep

Analyze, convert, and validate as separate activities.

### Change Claim

Do not imply that a separate prompt automatically provides independent validation. Use:

> **Use a separate validation pass with an explicit checklist and, where possible, a different reviewer, model, or deterministic test.**

### Add Validation Requirements

AI output **MUST** be checked for:

- Unsupported actions.
- Fabricated parameters.
- Unsafe permissions.
- Unpinned third-party actions.
- Lost conditions.
- Secret exposure.
- Environment and approval behavior.
- Shell differences.
- Output equivalence.

### Keep Honest Status

> Prompts drafted and reviewed; not yet validated against a production pipeline.

### Reason

This disclosure increases rather than decreases trust.

---

## Slide 29 — Crossing Mapped

**Priority:** P1 — Expand from four to six steps

### Revised Sequence

1. **Inventory and classify.**
2. **Trial-migrate repository.**
3. **Audit and convert automation.**
4. **Rebuild identity, access, and environments.**
5. **Validate behavior and deployability.**
6. **Cut over, monitor, and decommission.**

### Change Finish Line

Replace **“First Green Build”** with:

> **First Verified Delivery**

Subtext:

> Green build, equivalent artifact, controlled deployment, traceability, and rollback.

### Reason

A green build alone does not prove migration success.

---

## Slide 30 — Key Takeaways From the Crossing

**Priority:** P0 — Complete or cut

### Option A — Preferred

Replace the placeholder with actual PoC findings:

- Selected repository and why.
- Importer classification.
- Unsupported construct.
- Largest manual task.
- First-green-build effort.
- Validation result.
- Surprise.
- What you would do differently.

### Option B

Delete the slide entirely if the work has not occurred.

### Do Not

Present prompts or hypothetical findings as conclusions.

### Reason

This is the deck’s largest current credibility gap.

---

## New Slide After 30 — Migration Acceptance Checklist

**Priority:** P1 — Add

### Title

> **“Migrated” Is a Checklist, Not a Repository URL**

### Checklist

- Target repository visibility verified.
- Branches, tags, and sampled commits reconciled.
- PR history and attachments sampled.
- Identity attribution verified.
- Teams and permissions tested.
- Branch and environment protections enforced.
- LFS and large-file behavior tested.
- Build artifact compared.
- Deployment tested.
- Secrets and OIDC reviewed.
- Monitoring and notifications confirmed.
- Boards links and traceability verified.
- Rollback owner and procedure documented.
- Old repository state and decommission date defined.

### Value

This should be one of the deck’s downloadable takeaways.

---

## Slide 31 — Q&A Pocket

**Priority:** P1 — Keep but rename

### New Title

> **Pipeline and Migration Clarifications**

### Instructions

- Allow 3–5 minutes.
- Take questions on migration mechanics.
- Defer strategic product debate to the end.

This becomes the first formal question pause.

---

# Section 4 — Planning and Test Management

## Slide 32 — Section Opener

**Priority:** P2 — Keep

The Scrum Master line works. Deliver it warmly rather than as a caricature.

---

## Slide 33 — Boards versus Projects Framing

**Priority:** P0 — Modernize

### Remove

> GitHub Projects is a lightweight kanban board sitting on top of Issues.

### Replace With

> **GitHub Projects is a flexible, code-adjacent planning system built around issues and pull requests. Azure Boards is a mature enterprise work-tracking and portfolio system with stronger formal planning, process, capacity, and reporting capabilities.**

### Add

> They overlap, but they optimize for different operating models.

### Reason

This prevents knowledgeable GitHub users from dismissing the comparison as outdated.

---

## Slide 34 — Azure Boards Strengths

**Priority:** P1 — Keep and sharpen

### Add

- Inherited and customized process models.
- Capacity and sprint planning.
- Area and iteration paths.
- Portfolio and dependency reporting.
- Mature analytics integration.
- Test-management integration.

### Caveat

> These features matter only if the organization actually depends on them.

---

## Slide 35 — GitHub Projects Strengths

**Priority:** P0 — Update

### Add

- Table, board, and roadmap views.
- Iterations.
- Custom fields.
- Configurable charts.
- Automation.
- Dependencies.
- Issue types.
- Nested sub-issues.
- Organization-level projects.

### Replace Organization Model

Remove:

> Repository → Label → Milestone.

Use:

> **Organizations and repositories → projects and views → issues, pull requests, fields, issue types, milestones, dependencies, and sub-issues.**

### Takeaway

> GitHub Projects is no longer only a team kanban board. The decision turns on formal process, capacity, analytics, and portfolio needs.

---

## Slide 36 — What Is Lost Migrating Work Items

**Priority:** P1 — Make conditional

### Change Headline

> **What Does Not Map Cleanly from Azure Boards**

### Retain

- Historical sprint and capacity information.
- Custom process fields.
- Area and iteration path semantics.
- Reporting history.
- Process rules.

### Add

- Identity and comment attribution.
- Link relationships.
- Attachments.
- Query and dashboard dependencies.
- Integrations using work-item IDs.

### Change Tooling Statement

> Migration tooling can move portions of the data, but data-model mapping, validation, and reporting reconstruction remain project work.

---

## Slide 37 — Test Plans

**Priority:** P0 — Use a precise headline

### Change Title

> **Azure Test Plans: No Native GitHub Equivalent**

### Keep

- Regulated environments may retain Azure DevOps specifically for this capability.
- “It does not move, and that is fine.”

### Add

> A third-party test-management platform is a separate product decision, not an automatic part of repository migration.

### Target Delivery

1 minute.

---

## Slides 38 and 39 — Hybrid Resolution and Recommendation

**Priority:** P1 — Combine

### New Title

> **Recommendation: Decouple Repository Migration from Planning-Tool Replacement**

### Content

- Move repositories where repository-native capabilities justify it.
- Connect Azure Boards for traceability.
- Retain Test Plans where required.
- Evaluate GitHub Projects independently against actual planning needs.
- Do not migrate work items merely because the source repository moved.
- Reconsider Azure Boards later if a different planning tool wins on its own merits.

### Replace Personas

Use workflow categories, not developers versus managers.

### Reason

One strong recommendation slide is better than two repetitions.

---

## Slide 40 — Q&A Pocket

**Priority:** P1 — Keep for long version only

### Rename

> **Planning and Test-Management Clarifications**

### Timing

2–3 minutes for the 90-minute version.

Delete it from the 60-minute version and send questions to final Q&A.

---

# Section 5 — Rollout and Operational Adoption

## Slide 41 — Section Opener

**Priority:** P2 — Keep

The ancient-pipeline joke is one of the deck’s best humor beats.

---

## Slide 42 — Change Management in Engineering Costume

**Priority:** P1 — Make more technical

### Replace Generalized Failure Language

Replace:

> The tooling almost always works.

With:

> **Migration failures are rarely only tool failures. They emerge at the boundaries between tooling, ownership, access, process, and operational readiness.**

### Replace the Three Current Points With

- No agreed target architecture.
- No authoritative source during transition.
- Unclear ownership of conversion failures.
- Insufficient pilot evidence.
- Rollout perceived as imposed rather than co-designed.

### Reason

This avoids an unsupported absolute and grounds change management in engineering controls.

---

## Slides 43 and 44 — Selection Process and Pilot Defaults

**Priority:** P1 — Combine

### New Title

> **Pilot One Real Delivery Path Before Standardizing**

### Sequence

1. Define required outcomes and constraints.
2. Select one representative, noncritical repository.
3. Preserve enough default behavior to learn the platform.
4. Migrate repository, build, deployment, traceability, and ownership.
5. Measure the predefined outcomes.
6. Standardize only after evidence exists.

### Add Measurable Outcomes

- Time to first verified delivery.
- Manual conversion effort.
- Unsupported constructs.
- Developer friction.
- Operational incidents.
- Security exceptions.
- Support demand.

### Keep

> Customize afterward, with real usage data instead of guesses.

### Reason

This tells a stronger engineering story than a generic tool-evaluation process.

---

## Slide 45 — Cost Model

**Priority:** P0 — Remove unsupported threshold

### Delete

> Past roughly 100 engineers…

Unless an explicit model or source supports it.

### Replace With a Cost Equation

> **Total cost = licenses + security add-ons + compute and runners + migration effort + platform administration + dual-running + training + opportunity cost**

### Add

> Run the calculation over the migration and steady-state periods separately.

### Recommendation

> Do not use seat price as a proxy for total cost.

### Reason

Senior engineers and architects will trust an explicit model more than a broad headcount threshold.

---

## Slide 46 — Migration Sequence

**Priority:** P1 — Revise

### Revised Sequence

1. Connect traceability and define authority.
2. Trial-migrate a representative repository.
3. Migrate in waves using explicit entry criteria.
4. Convert automation and validate delivery.
5. Operate a controlled parallel period where needed.
6. Make the old system read-only.
7. Decommission only after long-tail checks pass.

### Add Wave Entry Criteria

- Named owner.
- Supported repository size.
- Identity mapping ready.
- Pipeline classification complete.
- Runner path available.
- Rollback defined.
- Downstream consumers identified.

### Reason

This turns sequencing into a deployable program model.

---

## Slide 47 — Structured Work Items

**Priority:** P1 — Keep but make actionable

### Add a Minimum Agent-Ready Work-Item Template

- Problem or user outcome.
- Scope and explicit non-goals.
- Acceptance criteria.
- Relevant repository or service.
- Constraints.
- Test expectations.
- Security or compliance considerations.
- Definition of done.

### Suggested Line

> AI amplifies specification quality. It does not replace it.

### Reason

This reinforces governance and developer enablement without adding unnecessary red tape.

---

## Slide 48 — Match Tool to Context

**Priority:** P1 — Simplify

### Replace Audience-Size Categories

#### GitHub Projects Is Favored When

- Planning is code-adjacent.
- Process flexibility is desired.
- Formal capacity management is not required.
- Reporting needs are modest.
- Issues and PRs are the center of coordination.

#### Azure Boards Is Favored When

- Formal hierarchy and process control matter.
- Capacity planning is required.
- Multiple teams share portfolio reporting.
- Historical analytics are important.
- Test Plans integration matters.

#### Hybrid Is Favored When

- Repository-native GitHub capabilities are wanted.
- Boards or Test Plans still provide material value.
- Migration scope must be reduced.

### Keep Senior-Engineer Callback

Shorten it to:

> The senior engineer is right to demand evidence. Replace “it has always worked” with “here is what the pilot proved.”

---

## Slide 49 — Q&A Pocket

**Priority:** P1 — Cut

Questions can flow into the long-tail section or final Q&A. Another formal pause adds more pacing risk than value.

---

# Section 6 — Long Tail and Decommissioning

## Slide 50 — Section Opener

**Priority:** P2 — Keep

No substantive edit needed.

---

## Slide 51 — Hardcoded URLs

**Priority:** P1 — Strengthen

### Add Search Domains

- Source repositories.
- Pipeline and release definitions.
- Infrastructure-as-code.
- Wiki and README content.
- Package configuration.
- Service hooks and webhooks.
- Dashboards and reports.
- Internal portals.
- Scripts and scheduled tasks.
- Browser bookmarks and onboarding guides.

### Add Ownership

> Every discovered reference needs an owner, replacement, and disposition.

### Add Second Sweep

Keep the later sweep after monthly and infrequent processes have run.

### Humor

> The migration is complete until the first monthly process remembers it exists.

---

## Slide 52 — Mannequins

**Priority:** P0 — Verify detailed behavior and simplify

### Required Fact Check

Revalidate:

- Which migrated content is attributed to mannequins.
- Which content is excluded.
- Who can reclaim.
- Current search behavior.
- Differences for Enterprise Managed Users or other account models.

### Main Slide Content

Reduce to:

> **Identity mapping is a pre-migration design decision.**  
> Migrated collaboration history may initially be attributed to placeholder identities. Reclaiming and attribution depend on account mapping and administrative action.

### Move Detailed Edge Cases

Place them in speaker notes or the appendix.

### Keep Humor

> Nothing says successful migration like a pull request reviewed by twelve people named Mannequin.

Use only if it remains technically consistent with the verified behavior.

---

## Slide 53 — Unglamorous Truth

**Priority:** P2 — Keep

### Optional Wording Improvement

> Most migrations are not a disaster movie. They are a checklist, an ownership model, and a few failures that reveal where the checklist was incomplete.

---

## Slide 54 — Takeaways Recap

**Priority:** P0 — Correct

### Required Correction

Replace:

> Repos and Actions travel clean.

With:

> **Git content is the most portable. Pipelines require semantic conversion and behavioral validation.**

### Revised Six Takeaways

1. **Repository location matters**
   - It affects native agentic, security, and workflow capabilities.

2. **Portability varies**
   - Git travels well; platform-specific metadata and behavior need validation.

3. **Pipelines are redesigned, not transliterated**
   - Use importer audits, engineering review, and independent validation.

4. **Planning is a separate decision**
   - Connect Boards first; replace it only when another planning model is proven sufficient.

5. **The migration sequence is an operating model**
   - Ownership, waves, rollback, and decommissioning matter as much as conversion tooling.

6. **The long tail is real**
   - Identity, URLs, consumers, scheduled jobs, and historical reporting survive the cutover.

### Delivery

One sentence per item. Do not re-teach the deck.

---

## Slide 55 — Links and QR Codes

**Priority:** P0 — Verify every target

### Required Checks

- QR resolves from the projected slide.
- Repository is accessible to the audience.
- Paths are public if the audience is external.
- AI prompt folder exists.
- Links reflect renamed or moved content.
- No internal secrets or private documentation are exposed.

### Add Downloadable Artifacts

The repository should ideally contain:

- Migration acceptance checklist.
- Pipeline review checklist.
- Decision matrix for Boards versus Projects.
- Example importer audit output.
- Example before-and-after pipeline.
- URL-sweep checklist.
- Source links and verification dates.

### Delivery

Hold for 10–15 seconds without talking continuously.

---

## Slide 56 — Documentary Closer

**Priority:** P2 — Keep

The closer is memorable and earned by the recurring conceit.

### Caution

Do not immediately add another joke. Preserve the two-second pause.

---

## Slide 57 — Thank You and Q&A

**Priority:** P2 — Keep

### Add Three Seed Questions

- Which pipeline construct would be hardest in your estate?
- What would prevent you from keeping Boards hybrid?
- What would you require before declaring a repository migrated?

This supports both a 20-person and a 100-person room.

---

# Proposed New Deck Order

## Opening

1. Title.
2. Sponsor, only if required.
3. Agenda.
4. Section 1 opener.
5. Why repository location matters.
6. Capability comparison.
7. MCP changed the boundary.
8. Target hybrid architecture.

## Migration Surface

9. Section 2 opener.
10. Migration scorecard.
11. Repository data and metadata.
12. Wiki and documentation.
13. Packages and registries.
14. Dashboards and metrics.
15. Portability principle.

## Pipeline and Execution

16. Section 3 opener.
17. Semantic conversion problem.
18. Migration layers.
19. Manual mapping.
20. `gh ado2gh`.
21. Sequencing prerequisites.
22. Actions Importer.
23. Runner and network strategy.
24. AI assistance.
25. End-to-end migration sequence.
26. Real PoC findings.
27. Migration acceptance checklist.
28. Clarification pause.

## Planning and Testing

29. Section 4 opener.
30. Boards versus Projects framing.
31. Azure Boards strengths.
32. GitHub Projects strengths.
33. Data-model mismatch.
34. Test Plans.
35. Recommendation.

## Rollout

36. Section 5 opener.
37. Engineering boundaries of change management.
38. Pilot before standardization.
39. Total-cost model.
40. Wave and cutover sequence.
41. Agent-ready work items.
42. Context-based tool selection.

## Long Tail and Close

43. Section 6 opener.
44. Hardcoded references.
45. Identity mapping and mannequins.
46. Unglamorous truth.
47. Takeaways.
48. Links and QR.
49. Documentary closer.
50. Thank you and final Q&A.

---

# Recommended Execution Order

## First Pass — P0 Credibility Fixes

1. Correct slide 54.
2. Remove the slide 14 visibility claim.
3. Modernize the GitHub Projects description on slides 33–36.
4. Replace the slide 18 portability taxonomy.
5. Complete or delete slide 30.
6. Verify slide 6 capability statuses.
7. Verify slide 17 metrics claims.
8. Remove the unsupported slide 45 headcount threshold.
9. Revalidate slide 52 mannequin details.
10. Verify all QR targets.

## Second Pass — P1 Value Additions

1. Add runner and network strategy.
2. Add real before-and-after pipeline material.
3. Add migration acceptance checklist.
4. Add rollback and authority model.
5. Combine slides 8–10.
6. Combine slides 38–39.
7. Combine slides 43–44.
8. Reduce Q&A pockets.
9. Add decision criteria to packages and planning sections.
10. Rework section 3 around repository, automation, and validation layers.

## Third Pass — P2 Delivery Polish

1. Tighten documentary transitions.
2. Insert four or five engineering humor lines.
3. Standardize fact, finding, recommendation, and preview labels.
4. Add final Q&A seed questions.
5. Rehearse the 60-minute cut and the 75-minute default.
6. Ensure transitions and speaker notes reflect the final slide numbering.

---

# Final Target

The revised presentation should feel like:

> **A practical enterprise migration field guide, grounded in architecture boundaries and operational evidence, with enough personality to remain memorable.**

The key shift is from explaining why GitHub is attractive to showing senior engineers exactly:

- What changes.
- What does not.
- How they prove equivalence.
- How they manage identity, access, runners, and downstream dependencies.
- How they preserve rollback options.
- How they avoid declaring victory too early.
