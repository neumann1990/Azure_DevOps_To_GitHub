---
title: Packages and Artifacts
status: researched
tags: [artifacts, packages, nuget, npm]
updated: 2026-09-04
---

**In one line:** Azure Artifacts and GitHub Packages can coexist — this is a decision to make, not a migration to run.

**Verdict: 🟡 Needs a decision.**

## The situation

> In Azure DevOps, you may have used Azure Artifacts to publish and consume packages (for example, NuGet packages, npm packages, or Maven packages) and to store build artifacts produced by Azure Pipelines.

> On GitHub, packages are typically published to GitHub Packages and associated with a repository or organization. Depending on how your enterprise completed the migration, you may continue to publish packages to Azure Artifacts, move packages to GitHub Packages, or use a combination of both.

Source: <https://docs.github.com/en/migrations/ado/key-differences-between-azure-devops-and-github>

## Three paths

1. **Keep Azure Artifacts.** Actions publishes to and consumes from the existing feed. Least disruption; keeps an Azure DevOps dependency.
2. **Move to GitHub Packages.** Cleaner end state; requires repointing every consumer.
3. **Both.** Common during transition. Needs a clear rule for which packages live where, or it becomes permanent by accident.

> **Kevin:** For the PoC, prove path 1 — Actions publishing to an existing Azure Artifacts feed. That's the realistic answer for anyone who can't repoint every consumer at cutover, and it's the question people will actually ask.

## Open

- Which authentication path Actions uses against an Azure Artifacts feed (PAT vs. OIDC / workload identity)
- Whether upstream sources / feed views survive the arrangement
