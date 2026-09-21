---
title: Wiki
status: researched
tags: [wiki, docs]
updated: 2026-09-04
---

**In one line:** Both are Git repos, so the content moves easily — you lose permissions granularity and Boards/pipeline integration.

**Verdict: 🟢 Travels clean** (content), with feature loss.

## GitHub wikis

> Every repository on GitHub comes equipped with a section for hosting documentation, called a wiki. You can use your repository's wiki to share long-form content about your project, such as how to use it, how you designed it, or its core principles. A README file quickly tells what your project can do, while you can use a wiki to provide additional documentation.

> Wikis are part of Git repositories, so you can make changes locally and push them to your repository using a Git workflow.

Sources: [About wikis](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis) · [About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)

## Migration mechanics

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.wiki.git
# Clones the wiki locally
```

> Once you have cloned the wiki, you can add new files, edit existing ones, and commit your changes. You and your collaborators can create branches when working on wikis, but only changes pushed to the default branch will be made live and available to your readers.

Source: [Cloning wikis to your computer](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages#cloning-wikis-to-your-computer)

Azure DevOps wikis are also Git-backed, so the migration is effectively clone-and-push.

## Azure DevOps Wiki vs GitHub Wiki

Both are Markdown-based and version-controlled, but target slightly different needs.

**Azure DevOps Wiki**

- Rich enterprise permissions management
- Tight integration with pipelines and boards
- Less visibility for external contributors

**GitHub Wiki**

- Hosted alongside repositories; tied closely to the repo
- Ideal for GitHub-based projects, developer communities, open source and internal code-centric teams
- Simple to set up
- Fewer enterprise features — no granular ACLs, weaker advanced search

> **Kevin:** In practice the content migration is trivial and the permissions story is the whole conversation. Worth one slide, not more.
