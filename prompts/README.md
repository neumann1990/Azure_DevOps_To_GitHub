# AI prompts — Azure Pipelines to GitHub Actions

Companion material to section 3 ("Crossing the River") of the *Azure DevOps to GitHub Enterprise: The Great Migration* talk — the "AI approach" to pipeline migration, alongside the Manual and Tooling approaches covered in [`../mechanics/07-migration-approaches.md`](../mechanics/07-migration-approaches.md).

**Status: drafted, not yet tested against a real pipeline.** These prompts encode the concept-mapping and syntax-difference rules from [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) as instructions for an AI coding assistant, rather than as prose documentation a human has to translate by hand. Before they go on stage, run all three against at least one real `azure-pipelines.yml` — ideally the same repo(s) used for the section 3 screenshot walkthrough (see the still-open "which repos" question in [`../session/03-open-questions.md`](../session/03-open-questions.md)) — and fix whatever they get wrong.

## The three prompts

1. [`01-analyze-azure-pipeline.md`](01-analyze-azure-pipeline.md) — feed it an `azure-pipelines.yml`, get back an inventory of what's in it and a first-pass estimate of automatable vs. manual work, in the same spirit as the GitHub Actions Importer's `audit` command but usable on a pipeline you haven't run the importer against yet.
2. [`02-convert-pipeline-to-actions.md`](02-convert-pipeline-to-actions.md) — the actual conversion. Give it the same pipeline, get back a GitHub Actions workflow YAML plus a list of anything it wasn't confident about.
3. [`03-validate-converted-workflow.md`](03-validate-converted-workflow.md) — feed it both files (the original pipeline and the converted workflow), get back a side-by-side check for behavior parity, not just syntax validity.

Run them in that order. The analyze step is what makes the convert step's output trustworthy — skipping straight to conversion is how you get a workflow that looks plausible and quietly drops a conditional.

## How these differ from the Tooling approach

`gh-actions-importer` (see [`../mechanics/01-tooling.md`](../mechanics/01-tooling.md)) applies a fixed, vendor-maintained rule set — reliable, but you can't ask it "why" or hand it a judgment call it wasn't built for. These prompts are meant for the pipelines that importer flags as partial or manual: the ones where a human has to decide what the equivalent behavior actually is, and an AI assistant that can reason about the specific YAML in front of it is more useful than a fixed rule table.

## Source material

Every rule encoded in these prompts is traceable to [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — the concept mapping table, the key syntactic differences, and the linked GitHub docs. If a prompt gets something wrong, check whether the source doc already covers it before assuming the AI hallucinated it.
