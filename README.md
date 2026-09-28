# Azure DevOps → GitHub Enterprise

Working knowledge base for the **Cloud & AI Summit** session _"Azure DevOps to GitHub Enterprise: The Great Migration"_ (30 September 2026, 90 minutes) and the supporting proof of concept.

---

## Session feedback

<img src="assets/session-feedback-qr.png" alt="QR code linking to the session feedback form" width="180" />

Scan the code above, or use the link directly: **[Leave feedback on this session](https://www.cloudandaisummit.com/content/sessionfeedback/1168888)**

---

## Documentation & tooling from the talk

Everything named or QR-coded on a slide, in one place — the fallback for anyone who didn't scan one live. See [`session/07-qr-and-links-plan.md`](session/07-qr-and-links-plan.md) for which slide each one came from.

**This repo**

- [neumann1990/Azure_DevOps_To_GitHub](https://github.com/neumann1990/Azure_DevOps_To_GitHub) — these notes, the PoC, and the AI prompts below

**Migrating repositories**

- [GitHub Enterprise Importer overview](https://docs.github.com/en/migrations/using-github-enterprise-importer)
- [github/gh-ado2gh](https://github.com/github/gh-ado2gh) — the CLI extension used for repository migration
- [Introduction to Enterprise Live Migrations (ELM)](https://learn.microsoft.com/en-us/azure/devops/repos/enterprise-live-migrations/overview?view=azure-devops)

**Migrating pipelines**

- [Migrating from Azure Pipelines to GitHub Actions](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines) — the manual-migration approach
- [github/gh-actions-importer](https://github.com/github/gh-actions-importer) — the tooling approach
- [Azure Pipelines app on GitHub Marketplace](https://github.com/marketplace/azure-pipelines) — install before migrating repos, not after

**Work items and boards**

- [nkdAgility/azure-devops-migration-tools](https://github.com/nkdAgility/azure-devops-migration-tools) — for teams that insist on moving work items

**AI and MCP**

- [Model Context Protocol](https://modelcontextprotocol.io)
- [microsoft/azure-devops-mcp](https://github.com/microsoft/azure-devops-mcp) — the Azure DevOps MCP server referenced on the Copilot comparison slide
- [`prompts/`](prompts/) — the three AI prompts used for the pipeline-conversion approach (analyze, convert, validate)

---

## Map

| Folder                           | What lives here                                                                                   | Read it when                        |
| -------------------------------- | ------------------------------------------------------------------------------------------------- | ----------------------------------- |
| [`session/`](session/)           | The talk itself — abstract, scope, narrative theme, open decisions                                | Working on the deck                 |
| [`case/`](case/)                 | Why anyone migrates — platform direction, decision framework, pricing                             | Building the "why" section          |
| [`subsystems/`](subsystems/)     | One file per Azure DevOps subsystem and its GitHub counterpart                                    | Answering "what happens to X?"      |
| [`mechanics/`](mechanics/)       | How the migration is actually performed — tools, identity, ELM, sequencing                        | Running the PoC                     |
| [`prompts/`](prompts/)           | AI prompts for the section-3 "AI approach" — analyze, convert, validate Azure Pipelines → Actions | Building or demoing the AI approach |
| [`reference/`](reference/)       | DORA metrics, source links, glossary                                                              | Looking something up                |
| [`presentation/`](presentation/) | The slide deck itself (`.pptx`)                                                                   | Presenting or reviewing slides      |

Start here:

- **[`session/01-brief.md`](session/01-brief.md)** — what the talk promises and what it deliberately isn't
- **[`subsystems/00-scorecard.md`](subsystems/00-scorecard.md)** — the one-page verdict on every subsystem
- **[`mechanics/06-gei-repo-migration-runbook.md`](mechanics/06-gei-repo-migration-runbook.md)** — the full repository migration procedure, from GitHub's official guide
- **[`session/03-open-questions.md`](session/03-open-questions.md)** — what's still undecided

---

## How these files work

Every file opens with YAML frontmatter and a one-line summary:

```yaml
---
title: Repositories
status: verified # verified | researched | unverified | stub
tags: [repos, gei, tooling]
updated: 2026-09-04
---
```

`status` means:

| Value        | Meaning                                                                |
| ------------ | ---------------------------------------------------------------------- |
| `verified`   | Kevin has confirmed this hands-on in the PoC                           |
| `researched` | Sourced from docs or articles, not yet tested                          |
| `unverified` | From a low-authority or marketing source — treat as a lead, not a fact |
| `stub`       | Placeholder; needs writing                                             |

## Conventions

Two callout styles carry meaning. Please keep using them.

> **Kevin:** My own opinion, experience, or decision. Not sourced from anywhere.

> ⚠️ **Unverified.** Claim from a source I don't fully trust, or a number that may have moved. Check before it goes on a slide.

Source attribution goes on its own line directly under the claim it supports:

```markdown
Source: <https://docs.github.com/en/migrations/using-github-enterprise-importer>
```

## Adding notes

Drop new material into the folder it belongs to, or into `session/03-open-questions.md` if you're not sure yet. A rough bullet with a source link is more useful than nothing — polish later. If a new topic doesn't fit an existing file, make a new one and add a row to the folder's index.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the short version of the conventions, and [`AGENTS.md`](AGENTS.md) for how AI agents should navigate this repo.

---

## Using this repo with Claude

The point of keeping these notes in Git is that they stay editable from anywhere and Claude can read the current version rather than a stale upload.

- **Link the repo to your Claude project** so every conversation in it starts from these files. Claude projects can start threads from a project's files and repositories — see [What are projects?](https://support.claude.com/en/articles/9517075-what-are-projects).
- **Or clone it locally** and point Claude Cowork or Claude Code at the folder.

Either way, edit the markdown, commit, and the next conversation picks up the change. Don't paste notes into a chat and expect them to persist — chats don't share context unless it's in the project knowledge or the repo.
