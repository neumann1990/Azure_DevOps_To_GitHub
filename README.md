# Azure DevOps → GitHub Enterprise

Working knowledge base for the **Cloud & AI Summit** session *"Azure DevOps to GitHub Enterprise: The Great Migration"* (30 September 2026, 90 minutes) and the supporting proof of concept.

Source: the `ADOS - GHE` OneNote notebook, unpacked and reorganized. Nothing has been invented; where the notebook was ambiguous or a claim came from a low-authority source, that is flagged in place.

---

## Map

| Folder | What lives here | Read it when |
|---|---|---|
| [`session/`](session/) | The talk itself — abstract, scope, narrative theme, open decisions | Working on the deck |
| [`case/`](case/) | Why anyone migrates — platform direction, decision framework, pricing | Building the "why" section |
| [`subsystems/`](subsystems/) | One file per Azure DevOps subsystem and its GitHub counterpart | Answering "what happens to X?" |
| [`mechanics/`](mechanics/) | How the migration is actually performed — tools, identity, ELM, sequencing | Running the PoC |
| [`reference/`](reference/) | DORA metrics, source links, glossary | Looking something up |

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
status: verified          # verified | researched | unverified | stub
tags: [repos, gei, tooling]
updated: 2026-09-04
---
```

`status` means:

| Value | Meaning |
|---|---|
| `verified` | Kevin has confirmed this hands-on in the PoC |
| `researched` | Sourced from docs or articles, not yet tested |
| `unverified` | From a low-authority or marketing source — treat as a lead, not a fact |
| `stub` | Placeholder; needs writing |

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
