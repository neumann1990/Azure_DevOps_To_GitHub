---
title: Glossary
status: verified
tags: [reference, glossary]
updated: 2026-09-04
---

**In one line:** Acronyms and product names that appear across these notes.

| Term | Meaning |
|---|---|
| **ADO** | Azure DevOps |
| **GHEC** | GitHub Enterprise Cloud |
| **GHES** | GitHub Enterprise Server (self-hosted) |
| **GHAS** | GitHub Advanced Security — vulnerability analysis, secret scanning, dependency review, code quality |
| **GEI** | GitHub Enterprise Importer, formerly Octoshift — API-first migration offering, wrapped by the GEI-CLI |
| **`gh-ado2gh`** | GitHub CLI extension for Azure DevOps → GitHub migration |
| **`gh-gei`** | GitHub CLI extension for GitHub → GitHub migration |
| **Actions Importer** | `gh-actions-importer` — plans and automates pipeline migration to GitHub Actions |
| **ELM** | Enterprise Live Migrations — Microsoft's preview zero-downtime migration service. Requires data residency. |
| **EMU** | Enterprise Managed Users — GitHub enterprise type where you provision and control user accounts |
| **Data residency** | GHEC deployment on a dedicated `<enterprise>.ghe.com` subdomain, region-pinned, isolated from github.com. Requires EMU. |
| **Mannequin** | Placeholder GitHub account created for an Azure DevOps user during migration, later remapped to a real identity. All migrated user activity except Git commits is attributed to one. |
| **Migrator role** | GitHub role an organization owner grants so a non-owner can run migrations. Cannot assign the role itself, or reclaim mannequins. |
| **`git-sizer`** | GitHub tool for sizing a repository against the GEI limits (blob size, commit size, tree counts) before migrating |
| **`GH_PAT` / `ADO_PAT`** | Environment variables the ADO2GH extension reads for the destination and source personal access tokens |
| **TFVC** | Team Foundation Version Control — Azure DevOps' pre-Git version control. Must be converted to Git before migrating. |
| **DORA** | The four delivery metrics: deployment frequency, lead time for changes, change failure rate, mean time to recovery |
| **Agent HQ** | GitHub's AI control center for managing tasks across agents |
| **Delivery Plans** | Azure Boards feature for multi-team roadmaps and cross-team dependency views |
| **Analytics / Power BI connector** | Azure DevOps' enterprise reporting layer over work item data |
| **Entra ID** | Microsoft's identity platform, formerly Azure AD. Required for the free ADO Basic + GHEC arrangement. |
