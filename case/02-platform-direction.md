---
title: Platform direction
status: researched
tags: [why, roadmap, microsoft, hybrid]
updated: 2026-09-04
---

**In one line:** No, GitHub is not replacing Azure DevOps — the two are diverging in purpose, and Microsoft's own recommended path is hybrid.

## Is GitHub replacing Azure DevOps?

No. Azure DevOps has an active roadmap extending through 2026 and beyond, and Microsoft continues shipping new features. But the platforms are diverging in purpose.

Source: <https://learn.microsoft.com/en-us/azure/devops/release-notes/features-timeline>

Microsoft is positioning:

- **GitHub** as the *AI-native development platform*
- **Azure DevOps** as the *enterprise orchestration layer*

All AI investment (Copilot, Workspace, Autofix, Agentic DevOps) goes to GitHub. Azure DevOps keeps its strengths in Boards, Pipelines, Test Plans and Artifacts.

## What Azure DevOps still does well

- **Azure Boards** — very complete and flexible enterprise project management: hierarchical work items, burndowns, Power BI reporting
- **Azure Pipelines** — a powerful, stable CI/CD automation engine; dedicated release pipelines, deployment groups, pre/post-deployment checks
- **Azure Test Plans** — manual and automated testing with detailed tracking
- **Azure integration** — native connection with Azure services; tight integration with Teams, Visual Studio and Entra ID
- **TFVC** — the only platform that still supports it

## The hybrid pattern

> For many organizations, the ideal strategy is to migrate source code to GitHub while keeping Azure Boards for project management. You thus have the best of both worlds: GitHub's advanced AI for development and Azure DevOps' robustness for project management, with integration between the two platforms allowing AI to be integrated into all stages of the software development lifecycle.

This is the approach Microsoft itself recommends. Use GitHub for source control and AI-powered development; use Azure Boards for enterprise project management. The two integrate natively: Azure Boards links to GitHub commits and PRs, and GitHub Enterprise Cloud includes free Azure DevOps Basic access.

Who gets what:

- **Developers** get GitHub's collaboration UX and Copilot
- **Managers** get Azure Boards' sprint planning, capacity, and Power BI reporting

Sources:
<https://devblogs.microsoft.com/devops/azure-devops-with-github-repositories-your-path-to-agentic-ai/>
<https://devblogs.microsoft.com/all-things-azure/azure-devops-to-github-migration-playbook-unlocking-agentic-devops/>

Common integration patterns in practice:

- Code hosted on GitHub, planning in Boards, CI/CD split between Actions for CI and Pipelines for complex CD
- Vendor toolchains pushing incidents from PagerDuty or ServiceNow into Boards or Projects for unified triage
- Data pipelines exporting work item and project data into a shared warehouse for portfolio analytics

## Timeline

| When | Event |
|---|---|
| February 2025 | Azure DevOps Basic license included with GitHub Enterprise Cloud (Entra ID required) — [sprint 252 notes](https://learn.microsoft.com/en-us/azure/devops/release-notes/2025/sprint-252-update) |
| February 2025 | Microsoft publishes an official migration playbook recommending repos move to GitHub |
| — | Azure DevOps stops accepting new OAuth app registrations (migration to Entra ID) |
| Ongoing | Full Azure DevOps OAuth platform retirement — teams must move to Entra ID |

> ⚠️ **Dates need confirming.** The OAuth retirement milestones had no firm dates in the notebook. Check the [features timeline](https://learn.microsoft.com/en-us/azure/devops/release-notes/features-timeline) before this goes on a slide.
