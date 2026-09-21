---
title: Enterprise Live Migrations (ELM)
status: researched
tags: [elm, blocked, data-residency, preview]
updated: 2026-09-04
---

**In one line:** Microsoft's preview zero-downtime migration service — and Hunter can't trial it, because it requires a data residency enterprise.

> 🔴 **Blocked.** ELM requires a GitHub Enterprise Cloud with data residency enterprise (`<enterprise>.ghe.com`), which Hunter does not currently use. Covered as research, not demo. → [`04-data-residency.md`](04-data-residency.md)

Source: <https://learn.microsoft.com/en-us/azure/devops/repos/enterprise-live-migrations/overview?view=azure-devops>

> ⚠️ **Two different things share the name "live migrations."** The ELM described on this page is Microsoft's Azure DevOps → GitHub service. GitHub's own docs have a *Live migrations (GHES to GHE.com)* section covering an unrelated GitHub Enterprise Server → GHE.com service, with its own [ELM CLI reference](https://docs.github.com/en/migrations/elm/elm-cli-reference). Don't conflate them on a slide.

## Core capabilities

**Continuous synchronization.** ELM syncs changes from Azure DevOps to GitHub using incremental sync and delta tracking, so teams can keep working in Azure DevOps until cutover. Plan for a brief read-only window at cutover — typically under 30 minutes for most repositories.

**Customer-scheduled cutover.** You choose and schedule the cutover time to switch the system of record from Azure DevOps to GitHub.

**Post-migration setup made easier.** ELM reduces the manual work after cutover by setting up the Azure Boards connection and rewiring Azure Pipelines to point to the migrated GitHub repository. This makes it easier for teams to keep using Azure DevOps for planning and pipelines while working from GitHub for source code, with less handoff pain and fewer follow-up tasks.

**Multi-repository migrations.** Up to 20 concurrent migration jobs. In the CLI, run the migration command for each repository one at a time. In the UI, select up to 20 repositories to migrate together.

**End-to-end migration workflow.** ELM tracks repository states through initialization, syncing, cutover, validation and completion — visibility into progress and support for troubleshooting.

## What ELM automates

- Runs pre-migration checks
- Creates the target GitHub organization
- Creates the target GitHub repository
- Syncs Git code, including branches, change history and tags to GitHub
- Syncs pull requests, including titles, descriptions, comments and user history
- Migrates branch policies to GitHub branch rulesets
- Creates a Boards connection
- Rewires Azure Pipelines to reference the new GitHub repository
- Cuts over from Azure DevOps to GitHub

## What you still do manually

- Clean up the Azure DevOps repository before migration (large files, pull requests with 10,000+ files, long ref names)
- Set up team and user access in GitHub
- Verify the post-migration repository state (branches, tags, history, pull requests)
- Verify and adjust migrated branch rulesets
- Update hardcoded Azure DevOps repository URLs in scripts, pipelines and tooling
- Migrate or decommission work items, wikis, pipelines and other non-repository data

## Prerequisites

- A GHE with data residency enterprise (`<enterprise>.ghe.com`)
- Which implies Enterprise Managed Users → [`02-identity-and-org-structure.md`](02-identity-and-org-structure.md)
- Preview feature

Related PDF in the original notebook: *GitHub Marketplace App Update - ELM.pdf* (document title: "Complete Prereq 0723 Update", dated 27 July 2026). Not reproduced here — the file lives in Kevin's Downloads.

## Why this is still worth stage time

> **Kevin:** The contrast is the point, but keep it honest. `gh ado2gh generate-script --all` already adds pipeline rewiring, team creation and Azure Boards integration to the generated script, so GEI is not as bare as ELM's marketing implies. What ELM genuinely adds is **continuous sync and a scheduled cutover** — the ability to keep working in Azure DevOps right up to a sub-30-minute read-only window. That's the real difference, and it's a better slide than an unfair feature-list comparison. → [`06-gei-repo-migration-runbook.md`](06-gei-repo-migration-runbook.md)
