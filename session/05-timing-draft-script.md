## TITLE
Good morning / afternoon. Before we start, a fair warning: this talk has jokes about scrum masters, and at least one of you is going to recognize yourself in the next seventy-five minutes. I'm not sorry.

This session is called "Azure DevOps to GitHub Enterprise: The Great Migration," and I mean that literally — think nature documentary, not corporate case study. We are going to observe the DevOps engineer in their natural habitat, watch them attempt a migration, and see what survives.

Two things I am deliberately not doing today. I am not going to debate whether GitHub is better than some other CI/CD platform. And I am not going to debate whether Copilot is better than some other AI tool. Those are religious wars, and I like all of you too much to start one before lunch. The destination is chosen. This talk is about the journey, not the argument.

Here's the shape of the next seventy-five minutes. Six expeditions. Six species of Azure DevOps subsystem, some of which migrate gracefully and some of which cling to the doorframe like a cat at the vet. Along the way: real mechanics, a couple of recorded walkthroughs, and enough confessions from teams who've already done this that you'll feel better about your own pipeline. Questions welcome as we go — I'd rather answer them in the moment than make you hold seventeen things in your head for an hour.

Let's begin.

## SECTION 1 — WHY WE LEFT THE HERD
[Opener card: "Migration Season Has Begun"]

Every year, without obvious explanation, a percentage of the herd simply leaves. The younger animals go first. The older ones follow, reluctantly, muttering about how the old watering hole was fine, actually.

Why do teams actually migrate from Azure DevOps to GitHub? The honest answer, the one that doesn't make it onto the vendor slide, is AI. Every dollar Microsoft is investing in Copilot — Copilot Chat, the Coding Agent, Autofix, Agentic Code Review, Agent HQ — lands on GitHub. None of it lands on Azure DevOps. If your roadmap includes AI-assisted development at any real scale, your repositories need to live where the AI lives.

That doesn't mean Azure DevOps is going away. Microsoft has an active roadmap for it through 2026 and beyond. What's actually happening is a split in purpose: GitHub is becoming the AI-native development platform, and Azure DevOps is settling into the role of enterprise orchestration layer — the thing that still does Boards, Test Plans, and release governance better than anything on the GitHub side. Microsoft's own recommended path, in writing, is hybrid: move source code to GitHub, keep Azure Boards for planning. Developers get GitHub's collaboration and Copilot; managers keep their sprint planning and Power BI reporting. Nobody has to give up their favorite spreadsheet.

There are non-AI reasons too, and they matter: a hundred million developers already live on GitHub, twenty-thousand-plus community actions in the marketplace versus a much smaller Azure Pipelines task catalogue, and if you have open-source contributors or lean on external collaborators, GitHub is simply where they already are.

So — the real reasons teams migrate. AI is the headline. Ecosystem gravity is the undertow.

## SECTION 2 — A FIELD GUIDE TO THE LOCAL SPECIES
[Opener card: "A Field Guide to the Local Species"]

Before any expedition, you catalogue the terrain. Here is the scorecard — every Azure DevOps subsystem, one verdict each, and whether it travels clean, needs a rewrite, or stays behind.

Let's start with the easy travelers. Repositories: green, travels clean — git is git, full stop. There's an asterisk, and it's an honest one: LFS objects, repo-level permissions, and some branch policies don't come across automatically, and there are four hard size limits you'll want to know about before you promise anyone a clean move. But structurally, this is the easiest leg of the whole migration.

Wiki: also green. Azure DevOps wikis are git repos under the hood on both sides, so it's genuinely a clone-and-push operation. You'll lose a few wiki-specific features, but the content itself travels intact.

Packages and Artifacts: yellow — not hard, but it needs a decision. Keep Azure Artifacts, move everything to GitHub Packages, or run both during the transition. There's no wrong answer here, but there is a wrong amount of time to spend not deciding.

Dashboards: also yellow, partial equivalent. GitHub's engineering analytics covers delivery metrics reasonably well. Nothing on the GitHub side matches the depth of Azure Boards' Power BI integration, and I want to be upfront about that rather than paper over it with a marketing slide.

That's four subsystems down, and notice the pattern: the things that are fundamentally file-based and version-controlled travel well. The things that are database-backed enterprise tooling — dashboards, and as we'll see shortly, boards themselves — don't. Keep that distinction in your head. It's the whole talk in one sentence.

## SECTION 3 — CROSSING THE RIVER
[Opener card: "Rare Footage of Successful Deployment"]

This is the crossing everyone's afraid of, and rightly — this is where the actual engineering work lives. Pipelines: yellow, needs a rewrite. Both Azure Pipelines and GitHub Actions use YAML, and that is precisely where the resemblance ends. Budget one to two days per complex pipeline, not because the tooling is bad, but because the concepts underneath don't map one-to-one.

Here's the vocabulary translation: a Pipeline becomes a Workflow. An Agent Pool becomes a Runner. A Service Connection becomes OIDC, secrets, or credentials, depending on what it was doing. A Variable Group becomes secrets and variables. A Task becomes an Action. `condition` becomes `if`. `dependsOn` becomes `needs`. And stages — Azure Pipelines lets you define stages right in the same YAML file; GitHub Actions makes you split them into separate workflow files entirely. That one catches people every time.

A few sharp edges worth knowing before you're mid-migration: Azure Pipelines has a classic drag-and-drop editor with no YAML required; GitHub Actions has no equivalent, YAML only. Azure Pipelines lets you skip structure for a single-job pipeline; GitHub Actions wants everything explicit. Conditionals go from function calls to infix operators. Script steps consolidate from `script`, `bash`, and `powershell` keys down to just `run` plus a `shell` selector. And here's a fun one: GitHub Actions fails fast on any error by default; Azure Pipelines needs you to configure that behavior explicitly. If your pipelines have been quietly swallowing errors for three years, this migration is when you find out.

You don't have to do this by hand. The GitHub Actions Importer will audit your existing pipelines and tell you what's automatable, what's partial, and what's fully manual — and that breakdown is the single most convincing slide you can put in front of a skeptical engineering manager, because it quantifies the work instead of hand-waving it.

[Recorded walkthrough: pipeline rewrite, clean repo vs. messy repo]

One sequencing rule that is not optional: install the Azure Pipelines GitHub App before you migrate any repositories. Do it after, and the migration script can't automatically reconfigure your pipelines to point at the new location — you'll be doing that by hand, repo by repo, while everyone asks why the build is red.

And a quick word on the fancy option: Microsoft has a preview service called Enterprise Live Migrations, which does continuous sync and a scheduled cutover — you keep working in Azure DevOps right up until a sub-thirty-minute read-only window, then flip. It's genuinely nice, and I can't demo it for you, because it requires a GitHub Enterprise Cloud tenant with data residency, which we don't run. What I can tell you is that the standard tooling — the GEI CLI — already does more than the marketing comparisons give it credit for: it generates scripts that handle pipeline rewiring, team creation, and the Boards connection. The real gap between the two isn't features. It's that continuous-sync, scheduled-cutover experience. That's worth knowing before a vendor tries to upsell you on it.

## SECTION 4 — SPRINT PLANNING IN ITS NATURAL HABITAT
[Opener card: "Watch as the Scrum Master Approaches Carefully"]

And here is where the gap is widest, and where I want to be the most honest with you. Azure Boards: red, clings to the doorframe. GitHub Projects: also relevant here, and also not a replacement.

Azure Boards is a full enterprise work-tracking system — hierarchical work items from Epics down through Features, Stories, and Tasks, sprint planning, capacity management, and Power BI reporting baked in. GitHub Issues, and GitHub Projects sitting on top of them, is a lightweight kanban-style board. It's genuinely good at what it does — flexible custom fields, tight proximity to your actual pull requests, fast for a small team doing daily triage. What it is not is a replacement for a scaled Agile shop's portfolio view.

If you try to migrate your work items wholesale, here's what you lose: sprint history, capacity data, custom process fields, and the entire Project-Team-Area hierarchy that Azure DevOps organizes around, versus GitHub's Repository-Label-Milestone model. There are open-source tools that help — the migration-tools project on GitHub is the one people reach for — but budget real time for manual mapping, because the data models simply don't line up.

Test Plans is the blunt version of the same story: red, stays behind, full stop. There is no GitHub equivalent. If you're in a regulated environment doing structured manual and exploratory testing with detailed tracking, this is the one gap you cannot rewrite your way around.

So what do you actually do? You don't migrate work items to GitHub Issues unless your project management needs are genuinely simple. You connect Azure Boards to your GitHub repos instead — first, before you touch anything else — and you keep planning where planning already works well. Developers live in GitHub. Managers keep their sprint hub, their capacity charts, and their Power BI dashboards. This isn't a compromise you're forced into. Microsoft designed it as the intended shape, and once you stop treating it as a failure to fully migrate, it gets a lot easier to sell internally.

## SECTION 5 — PREVENTING THE UPRISING
[Opener card: "The Senior Engineer Defends an Ancient Pipeline"]

Every herd has one member who will not leave. He built that pipeline in 2019. It has survived three reorgs and one failed platform migration already. He will defend it to the death, and honestly, fair enough — nobody documented it, so he's the only one who understands why it works.

This is the part of the talk that isn't about YAML. It's about the fact that a tool migration is a change-management problem wearing an engineering costume, and the teams that get this wrong don't fail on the technical mechanics — they fail because nobody ran a real selection process, or because customization started before anyone understood the new tool, or because the rollout felt like it was done to people instead of with them.

Here's the disciplined version. Define your must-haves before you evaluate anything. Assess your current toolchain and any data residency requirements. Model one real increment of work in each candidate tool — not a demo, an actual ticket through an actual pipeline. Score it with a weighted rubric so the decision isn't just whoever argued loudest in the meeting. Then run a four-to-six-week pilot with measurable outcomes before you commit the org. And critically: delay heavy customization until after that pilot. Customizing on day one locks in decisions made by people who didn't understand the tool yet.

Don't judge on sticker price alone, either. Compare licensing tiers, GitHub Advanced Security as an add-on, runner and compute minutes, and the administration and migration effort itself. Past a hundred engineers or so, the time you save in governance and reporting usually outweighs a modest per-seat price difference — but you have to actually run that math, not assume it.

The migration sequence itself is the change-management plan, whether you think of it that way or not. Start hybrid — connect Boards to GitHub before moving anything else, so nobody's planning workflow breaks on day one. Migrate repositories in waves, starting with something low-stakes, to build organizational confidence before you touch anything critical. Rewrite pipelines incrementally, running old and new in parallel so a bad migration doesn't take down a release. And leave work items alone unless you've already decided, deliberately, that you need to move them.

One more thing, because AI is the reason half of you are in this room: Copilot and agentic tooling only multiply value when the work items feeding them are well-structured. If your tickets are vague, your AI suggestions will be vague. Invest in templates and acceptance criteria before you expect the AI payoff — that's not a nice-to-have, it's the actual precondition.

## SECTION 6 — THE WATERING HOLE NOBODY TOLD TO MOVE
[Opener card: "The Watering Hole Nobody Told to Move"]

Migration complete. Champagne poured. And then, three weeks later, someone's deployment script quietly fails because it's still pointing at dev.azure.com.

This is the long tail, and it is the single most reliable source of post-migration tickets: hardcoded Azure DevOps URLs. They're in scripts, in pipeline YAML, in Infrastructure-as-Code, in service connections, in README files, in some internal tool nobody remembers who owns. Budget a real sweep for this. And budget a second sweep a month later, because you will find more after you were sure you were done. The old watering hole doesn't know it's been abandoned, and neither does every automated job still pointing at it.

[Space for a team's actual migration confession/war story here]

This is also where the herd looks back at what actually happened, and — if I'm honest with you — most of what happened is unglamorous. Nobody's migration was a disaster movie. It was a checklist, run carefully, with a couple of things that broke in ways nobody predicted, fixed by people who are somewhere in this room right now.

## CLOSER
[Closer line, spoken over whatever's on screen — ideally somebody's inherited 2016 pipeline]

For some, the city is a place of opportunity. For others, it's a place of danger. But for all of it — it is a world of our making.

Thank you.
