---
title: Subsystem scorecard
status: researched
tags: [scorecard, index, subsystems]
updated: 2026-09-04
---

**In one line:** Every Azure DevOps subsystem, and whether it travels clean, needs a rewrite, or stays behind.

> **Kevin:** This is probably the takeaway slide. One visual, every subsystem, three verdicts.

| Subsystem | Verdict | Why | Detail |
|---|---|---|---|
| **Repos** | 🟢 Travels clean* | Git is Git — but LFS objects, repo permissions and some branch policies don't come across, and four hard size limits apply. | [01](01-repos.md) |
| **Wiki** | 🟢 Travels clean | Wikis are Git repos on both sides — clone and push. Some features lost. | [04](04-wiki.md) |
| **Pipelines** | 🟡 Needs a rewrite | Both are YAML, but stages/jobs/tasks ≠ workflows/jobs/steps. 1–2 days per complex pipeline. | [02](02-pipelines-and-actions.md) |
| **Packages / Artifacts** | 🟡 Needs a decision | Keep Azure Artifacts, move to GitHub Packages, or both. | [05](05-packages-and-artifacts.md) |
| **Dashboards** | 🟡 Partial equivalent | GitHub engineering analytics covers delivery metrics; nothing matches Boards' Power BI depth. | [07](07-dashboards-and-analytics.md) |
| **Boards / work items** | 🔴 Clings to the doorframe | Richer data model than Issues. You lose sprint history, capacity, custom process fields. | [03](03-boards-and-projects.md) |
| **Test Plans** | 🔴 Stays behind | No GitHub equivalent exists. | [06](06-test-plans.md) |

\* The asterisk is the honest part. Repository migration is genuinely the easy leg, and it still has a list of exclusions worth reading before you promise anyone a clean move.

## The three-line summary

- **Repositories** are the easiest. **Pipelines** require rewriting, not porting. **Work items** are the hardest and usually shouldn't move at all.
- The gap is widest at Boards: a full enterprise work tracking system versus a lightweight kanban board.
- Test Plans has no counterpart, which matters most in regulated environments.

## Reading order for the talk

Follow the difficulty gradient — it's also the emotional arc. Start with the easy win (repos), move into the grind (pipelines), end with the things that don't move (Boards, Test Plans) and the hybrid answer that makes that acceptable.
