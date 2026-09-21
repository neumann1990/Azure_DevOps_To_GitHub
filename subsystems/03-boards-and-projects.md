---
title: Boards → Projects
status: researched
tags: [boards, projects, work-items, hybrid, safe]
updated: 2026-09-04
---

**In one line:** The widest gap in the whole migration — and the subsystem you most likely shouldn't move.

**Verdict: 🔴 Clings to the doorframe.**

## Why it's hard

> This is where the gap is widest. Azure Boards is a full enterprise work tracking system with sprint planning, capacity management, hierarchical work items, and Power BI reporting. GitHub Projects is a lightweight kanban-style board that works well for smaller teams but lacks the depth that enterprise Agile shops need.

> This is where most teams struggle. Azure DevOps work items (Epics, Features, User Stories, Tasks, Bugs) have a richer data model than GitHub Issues. You'll lose sprint history, capacity data, and custom process fields. The conceptual model also differs: Azure DevOps organizes by Project/Team/Area, while GitHub organizes by Repository/Label/Milestone. Open-source tools like [azure-devops-migration-tools](https://github.com/nkdAgility/azure-devops-migration-tools) help with this, but expect manual mapping work.

## What each side leads on

> From a planning perspective, think in terms of strengths rather than feature checklists. Azure Boards leads in hierarchy, portfolio visibility, capacity planning, and analytics integration. GitHub Projects leads in simplicity, flexible fields, and proximity to developer workflows.

### Azure Boards

Hierarchical backlogs from Epics → Features → Stories/Backlog Items → Tasks, with configurable work item types, queries and portfolio views. Designed for scaled teams needing traceability from code through deployment.
Source: <https://learn.microsoft.com/en-us/azure/devops/boards/work-items/about-work-items>

For planning rigor: portfolio backlogs, Delivery Plans across teams, capacity planning, and built-in burndown, cumulative flow and velocity.
Sources: [Set capacity for your team](https://learn.microsoft.com/en-us/azure/devops/boards/sprints/set-capacity) · [Delivery Plans 2.0 GA](https://devblogs.microsoft.com/devops/delivery-plans-2-0-is-now-ga/)

Configuration: configurable columns, swimlanes, WIP limits and state categories across processes, plus branch policies tying code quality to work item progress.

### GitHub Projects

> GitHub Projects functions like a spreadsheet-meets-kanban-roadmap that stays in sync with issues and pull requests. It supports custom fields such as single-select, date, number, text, and iteration, along with multiple saved views and built-in or Actions-driven automation.

Compose your own structure via custom fields — priority, points, owners, start and target dates, iterations. The roadmap layout visualizes items across time or iteration; filters and grouping slice by team, component or risk.

Sources: [Planning and tracking with Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects) · [Customizing the roadmap layout](https://docs.github.com/en/issues/planning-and-tracking-with-projects/customizing-views-in-your-project/customizing-the-roadmap-layout) · [Iteration fields](https://docs.github.com/issues/planning-and-tracking-with-projects/understanding-fields/about-iteration-fields) · [Project insights](https://docs.github.com/en/issues/planning-and-tracking-with-projects/understanding-insights/about-project-insights)

**Automation.** Column and field-based automation with triggers for item added, status changed and value updated. Combine with GitHub Actions to label issues, sync statuses, or post updates to chat. Start with a lightweight rule set — auto-moving cards when PRs close — and layer more gradually. The goal is to preserve flow without brittle rules that break during priority shifts.

**Developer-first workflow.** Issues and discussions feed directly into Projects; code owners plus required reviews keep standards consistent. Table view for bulk triage edits, board view for daily standups. If developers spend their day in GitHub, Projects keeps planning friction low.

## Parity and divergence

**At practical parity:**

- Basic kanban boards and backlog management
- Custom fields and saved views for filtering and grouping
- Automation options via native rules and APIs

**Meaningfully different:**

- Boards' Analytics and Power BI connector provide enterprise reporting out of the box; Projects requires API export or third-party analytics for equivalent depth
- Boards supports Delivery Plans and cross-team dependency views; Projects relies on roadmap views and organization conventions
- Boards integrates deeply with Azure Pipelines for release governance; Projects pairs more naturally with GitHub Actions and repository events

## The pragmatic pattern

> A pragmatic pattern many organizations adopt is to keep the source of truth for portfolio hierarchy in Boards and mirror essential fields to a Projects view for cross-repository triage when most code lives on GitHub. It is often easier to grant broader visibility in Projects while Boards retains the canonical model.

For SAFe portfolio/program/team layers: map Epics, Features and Stories in Boards, and use Projects fields to reflect feature readiness, dependencies or risk on shared visuals. For small product-led teams, Projects' lighter model is often enough — iteration fields and a burn-up chart without a full hierarchy.

> AI and Copilot multiply value only when work items are well structured. Invest in clear templates and acceptance criteria to realize real gains.

## Recommendation

**Don't migrate work items to GitHub Issues unless your PM needs are simple.** Connect Azure Boards to GitHub repos instead, before moving anything else.

Source: <https://www.fjan.nl/en/posts/azure-devops-vs-github-projects-2025-comparison-guide>
