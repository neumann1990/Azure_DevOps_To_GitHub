---
title: Repositories
status: researched
tags: [repos, gei, tfvc, mannequins, branch-policies, limits]
updated: 2026-09-04
---

**In one line:** The easy leg — but "Git is Git" hides a specific list of what migrates, what doesn't, and four hard size limits.

**Verdict: 🟢 Travels clean, with caveats.**

> Procedure lives in [`mechanics/06-gei-repo-migration-runbook.md`](../mechanics/06-gei-repo-migration-runbook.md). This page is the what-and-why.

## What GEI migrates

Per GitHub's own list:

- Git source, including commit history
- Pull requests
- User history for pull requests
- Work item links on pull requests
- Attachments on pull requests
- Branch policies for the repository — **excluding** user-scoped and cross-repo branch policies

Source: <https://docs.github.com/en/migrations/ado/understand-migrations-from-azure-devops-to-github>

> ⚠️ **Correction to earlier notes.** A third-party guide summarized this as "full history, branches, and tags come over intact." That's roughly true of the Git data, but it omits the exclusions below and implies more than the official list promises. Use the list above.

## What GEI does not migrate

**Repository permissions.** GEI doesn't attempt to migrate them, because the permission models differ. Instead the ADO2GH CLI creates two GitHub teams per Azure DevOps team project:

| Team | Access to migrated repositories |
|---|---|
| `TEAM-PROJECT-Maintainers` | Maintainer |
| `TEAM-PROJECT-Admins` | Admin |

You populate those teams — manually, or via Azure Active Directory group membership if you linked them during migration.

**Git LFS objects.** Repositories *using* LFS migrate fine; the LFS objects themselves do not. Push them to the destination as a follow-up.

**User-scoped and cross-repo branch policies.** Excluded from the branch policy migration.

**Anything changed during the migration.** GEI does not support delta migrations. Halt work, or migrate the changes by hand afterwards.

**TFVC.** Convert to Git first. Azure DevOps is the only platform that still supports TFVC, which is exactly why some repos are still on it.

**Azure DevOps Server.** GEI is Cloud-only. Migrate Server → Azure DevOps Cloud → GitHub.

## Hard limits

| Limit | Source of the limit |
|---|---|
| 2 GiB per Git commit | GitHub |
| 2 GiB per push | GitHub — larger pushes fail with `pack exceeds maximum allowed size` |
| 255 bytes per Git ref | GitHub — non-ASCII characters consume more than one byte |
| 100 MiB per file post-migration (400 MiB during) | GitHub |
| 40 GiB per repository (public preview) | GEI — source code only |
| 400 MiB per file during migration | GEI |

Check a repository against these with [git-sizer](https://github.com/github/git-sizer) before you queue it. It also flags blob size, commit size and tree counts that cause trouble.

> **Kevin:** The LFS gap and the 40 GiB ceiling are the two that will bite a real enterprise estate, and neither appeared in any of the third-party guides I collected. "Git is Git" is true right up until it isn't — that's a slide.

## Other gotchas

**Organization rulesets can fail a migration.** If a ruleset requires, say, commit author emails ending `@monalisa.cat`, non-compliant history fails the migration. Add "Repository migrations" to each ruleset's bypass list rather than disabling rulesets.

**Everything arrives private.** All repositories migrate as private, visible only to the migration runner and org owners. Set visibility deliberately afterwards.

**Code search lags.** Re-indexing takes a few hours; searches return unexpected results until it completes.

**Mannequin content may not be searchable** until reclaimed.

## Identity

User accounts import as **mannequins** — placeholders to which all non-commit activity is attributed. Git commits keep their original attribution. Plan the identity mapping before the first migration; only organization owners can reclaim mannequins. → [`mechanics/02-identity-and-org-structure.md`](../mechanics/02-identity-and-org-structure.md)

## Adjacent work the migration doesn't do

**Security tooling.** Azure Advanced Security maps to GitHub Advanced Security, but with different SKUs, scanning coverage and policy enforcement. Include a security review in the plan.
Source: <https://codepulsehq.com/guides/github-advanced-security-azure-devops-guide> ⚠️ third-party

**Branch policies → rulesets.** Azure DevOps policies tie code quality to work item progress: minimum reviewers, required linked work items, build validation gates. GitHub equivalents are branch rulesets plus CODEOWNERS, and the mapping isn't 1:1 — and the user-scoped and cross-repo policies don't migrate at all.
Source: <https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops>

**Hardcoded URLs.** Scripts, pipeline YAML, service connections, IaC, README links, internal tooling. The long tail everybody forgets.

## Repository visibility on GitHub

> In an enterprise on GitHub, repositories can be public, private, or internal. Private repositories are only visible to people and teams with explicit access, and internal repositories are visible to all members of your enterprise but not to people outside the enterprise. Internal repositories are useful when multiple organizations in the same enterprise need to discover and reuse code. If your enterprise uses Enterprise Managed Users, user accounts cannot create public repositories or other public content.

Source: <https://docs.github.com/en/migrations/ado/key-differences-between-azure-devops-and-github>
