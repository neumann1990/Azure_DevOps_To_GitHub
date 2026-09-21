---
title: Analyze an Azure Pipeline before converting
status: researched
tags: [prompts, ai-approach, pipelines, analysis]
updated: 2026-09-21
---

**In one line:** Run this first, against the raw `azure-pipelines.yml`, before attempting any conversion.

## The prompt

```
You are analyzing an Azure Pipelines YAML file to prepare for migrating it to
GitHub Actions. Do not convert anything yet — this is an inventory pass.

Read the attached azure-pipelines.yml and produce:

1. STRUCTURE: List every stage, job, and task in the pipeline, in order,
   with their names and what each one does in one line.

2. CONSTRUCTS USED: Flag every use of the following, with the line or
   section it appears in:
   - Stages (note whether they're used for genuine deployment gating or
     just organizational grouping — this changes how hard they are to
     port, since GitHub Actions has no direct "stages within one workflow
     file" equivalent)
   - Service connections and what they authenticate to
   - Variable groups and library variables
   - Conditions (`condition:`) and their expressions
   - `dependsOn` relationships between jobs/stages
   - The classic editor markers, if any (implies no YAML source of truth
     exists for part of the pipeline — flag this loudly, it means someone
     has to reconstruct it by hand regardless of tooling)
   - Custom or third-party tasks (not built-in Microsoft tasks) — these
     need a GitHub Actions Marketplace equivalent or a custom script
   - Any `script`, `bash`, `powershell`, or `pwsh` steps, and note the
     assumed shell (Azure Pipelines defaults to cmd.exe on Windows;
     GitHub Actions defaults to PowerShell — flag every step that
     depends on that default rather than declaring its shell explicitly)
   - Explicit error-handling configuration (Azure Pipelines does not
     fail-fast by default; GitHub Actions does — flag any step that
     relies on a command failing silently and pipeline execution
     continuing anyway)
   - stderr-triggers-failure configuration, which GitHub Actions has no
     equivalent for

3. RISK RATING: For each stage/job, rate it Automatable / Partial / Manual,
   matching the categories gh-actions-importer's audit command uses, and
   say why. A stage with only built-in tasks, standard scripts, and no
   classic-editor content is Automatable. A stage with custom tasks,
   complex conditionals, or classic-editor content is Manual or Partial.

4. OPEN QUESTIONS: List anything you're not confident about — a task
   whose exact behavior you can't infer from its name and inputs, a
   condition whose intent isn't obvious, or a variable group reference
   you can't resolve without seeing the variable group itself.

Output this as a structured report, not as YAML. The goal is a shared
understanding of what this pipeline actually does before anyone — human
or AI — tries to rewrite it.

<paste azure-pipelines.yml here>
```

## Why this step exists

The GitHub Actions Importer's `audit` command already does a version of this against pipelines it can parse — see [`../mechanics/01-tooling.md`](../mechanics/01-tooling.md). This prompt exists for two cases the importer doesn't cover well: pipelines with meaningful classic-editor content (nothing for the importer to parse), and getting a plain-English explanation of *why* something is flagged manual, which the importer's CSV output doesn't give you.

## Related

- [`02-convert-pipeline-to-actions.md`](02-convert-pipeline-to-actions.md) — the next step, once this inventory looks right
- [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — source material for every construct flagged above
