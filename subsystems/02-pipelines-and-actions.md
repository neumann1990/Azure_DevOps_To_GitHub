---
title: Pipelines → Actions
status: researched
tags: [pipelines, actions, ci-cd, yaml, importer]
updated: 2026-09-04
---

**In one line:** Both are YAML and that's where the resemblance ends — budget 1–2 days per complex pipeline and expect to rewrite, not port.

**Verdict: 🟡 Needs a rewrite.**

## The core problem

> Despite both using YAML, the syntax and concepts are different enough that you'll need to rewrite pipelines rather than port them. Azure Pipelines uses stages, jobs, and tasks with a different schema than GitHub Actions' workflows, jobs, and steps. Plan for 1-2 days per complex pipeline.

## Concept mapping

| Azure Pipelines | GitHub Actions |
|---|---|
| Pipeline | Workflow |
| Agent Pool | Runner |
| Service Connection | OIDC / Secrets / Credentials |
| Variable Group | Secrets / Variables |
| Task | Action |
| `condition` | `if` |
| `dependsOn` | `needs` |
| `stages` | Separate workflow or job |

## Key syntactic differences

Source for all of the following: <https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines>

**Classic editor.** Azure Pipelines supports a legacy classic editor — a GUI instead of YAML. GitHub Actions uses YAML files only and does not support a graphical editor.

**Structure cannot be omitted.** Azure Pipelines lets you skip structure in job definitions; with a single job you can define only its steps. GitHub Actions requires explicit configuration.

**Stages.** Azure Pipelines supports stages defined in the YAML file for deployment workflows. GitHub Actions requires you to separate stages into separate YAML workflow files.

**Conditionals.** Azure Pipelines uses functions within expressions; GitHub Actions uses infix notation. Replace function calls with operators.
[Migrating conditionals and expression syntax](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines#migrating-conditionals-and-expression-syntax)

**Script steps.** In Azure Pipelines, scripts use the `script` key, or `bash` / `powershell` / `pwsh` keys, or the [Bash task](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/bash?view=azure-devops) / [PowerShell task](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops). In GitHub Actions, all scripts use the `run` key, with `shell` to select a particular shell.
[Migrating script steps](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines#migrating-script-steps) · [Workflow syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#jobsjob_idstepsrun)

**Default Windows shell.** Azure Pipelines: Command shell (`cmd.exe`). GitHub Actions: PowerShell.

**Error handling.** GitHub Actions configures shells to "fail fast" wherever possible — a script stops immediately if a command exits with an error code. Azure Pipelines requires explicit configuration to exit immediately on error.

**stderr.** Azure Pipelines scripts can be configured to error if any output goes to `stderr`. GitHub Actions does not support this configuration.

**Runner selection.** On-premises Azure Pipelines build agents are selected by *capabilities*. GitHub Actions self-hosted runners are selected by *labels*.

## Tooling

**GitHub Actions Importer** plans and automates migration of Azure DevOps, Bamboo, Bitbucket, CircleCI, GitLab, Jenkins and Travis CI pipelines to GitHub Actions.

Source: <https://github.com/github/gh-actions-importer>

The `audit` command's automatable / partial / manual breakdown is the single most useful artifact for a slide — it quantifies the rewrite in a way people believe.

## Sequencing advice

- Rewrite pipelines incrementally
- Run old and new pipelines in parallel during transition
- Install the Azure Pipelines GitHub app **before** migrating repos, so pipelines can be reconfigured automatically → [`mechanics/01-tooling.md`](../mechanics/01-tooling.md)

## Related

- [`mechanics/01-tooling.md`](../mechanics/01-tooling.md) — installing the importer
- [`05-packages-and-artifacts.md`](05-packages-and-artifacts.md) — where build outputs go
