---
title: Migration tooling
status: researched
tags: [gei, gh-ado2gh, actions-importer, cli, setup]
updated: 2026-09-04
---

**In one line:** Three tools — `gh-ado2gh` for repositories, `gh-actions-importer` for pipelines, and the Azure Pipelines GitHub app, which must be installed first.

> For the full step-by-step repository migration procedure — access, scopes, script generation, trial run, follow-up — see [`06-gei-repo-migration-runbook.md`](06-gei-repo-migration-runbook.md). This page is the tooling overview.

## GitHub Enterprise Importer (GEI)

> The GitHub Enterprise Importer (GEI, formerly Octoshift) is a highly customizable API-first migration offering designed to help you move your enterprise to GitHub Enterprise Cloud. The GEI-CLI wraps the GEI APIs as a cross-platform console application to simplify customizing your migration experience.

Sources:
<https://docs.github.com/en/migrations/using-github-enterprise-importer>
<https://docs.github.com/en/migrations/ado>

**Azure DevOps Cloud only** — GEI cannot migrate from Azure DevOps Server.

## Setup

**1. GitHub CLI** — version 2.4.0 or newer (`gh --version`).
Source: <https://github.com/cli/cli#installation>

**2. ADO2GH extension**

```shell
gh extension install github/gh-ado2gh
gh extension upgrade github/gh-ado2gh   # updated weekly — upgrade before each session
```

**3. Actions Importer extension**

```shell
gh extension install github/gh-actions-importer
```

> GitHub Actions Importer helps you plan and automate the migration of Azure DevOps, Bamboo, Bitbucket, CircleCI, GitLab, Jenkins, and Travis CI pipelines to GitHub Actions.

Source: <https://github.com/github/gh-actions-importer>

**4. Environment variables**

```shell
export GH_PAT="TOKEN"      # destination org
export ADO_PAT="TOKEN"     # source org
```

PowerShell uses `$env:GH_PAT="TOKEN"`. Token scopes matter and differ by role — see the runbook.

## The Azure Pipelines GitHub app

> Before migrating your repositories, you need to install the Azure Pipelines application on your GitHub target organization(s). This application connects your Azure DevOps pipelines with your GitHub repositories, ensuring continuity of your CI/CD processes after migration.

> **Order is crucial:** Install the Azure Pipelines application first, then migrate your repositories. This ensures that the migration script can automatically reconfigure your pipelines to point to GitHub.

Source: <https://github.com/marketplace/azure-pipelines>

GitHub's own follow-up guidance points at the same reconnection: [Connect Azure Pipelines to GitHub](https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/github) and [Configure the Azure Boards app for GitHub](https://learn.microsoft.com/en-us/azure/devops/boards/github/install-github-app).

## Commands worth knowing

**Verified against the docs:**

| Command | What it gives you |
|---|---|
| `gh ado2gh --help` | All available commands |
| `gh ado2gh migrate-repo --help` | Options for a single command |
| `gh ado2gh inventory-report --ado-org YOUR_ADO_ORG` | CSV files including `repos.csv` with per-repo pull request counts |
| `gh ado2gh generate-script --ado-org SOURCE --github-org DESTINATION --output FILENAME` | A PowerShell script, one migration command per repository |
| `gh ado2gh wait-for-migration` | Status of a migration queued with `--queue-only` |

Useful flags on `generate-script`: `--all` (adds pipeline rewiring, team creation and Azure Boards integration), `--download-migration-logs`, `--target-api-url` (GHE.com), and per-line `--target-repo` / `--target-repo-visibility`.

**Actions Importer:**

| Command | What it gives you |
|---|---|
| `gh actions-importer audit azure-devops` | Automatable / partial / manual breakdown per pipeline |

> ⚠️ **Unverified syntax.** The Actions Importer `dry-run` and `migrate` subcommand shapes in these notes came from memory, not from the docs. Confirm against <https://github.com/github/gh-actions-importer> before demoing or putting a command on a slide. The ADO2GH commands above are verified.

> **Kevin:** The `inventory-report` and `audit` outputs are the best slide material in the whole PoC — they turn "this will be hard" into a number. And PR count, not repo count, is what actually drives the schedule.

## Work item tooling

For teams that insist on moving work items: [azure-devops-migration-tools](https://github.com/nkdAgility/azure-devops-migration-tools). Open source, helps, but expect manual mapping work. See [`subsystems/03-boards-and-projects.md`](../subsystems/03-boards-and-projects.md) for why this is usually the wrong call.

## Related

- [`06-gei-repo-migration-runbook.md`](06-gei-repo-migration-runbook.md) — the full procedure
- [`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — what the rewrite involves
