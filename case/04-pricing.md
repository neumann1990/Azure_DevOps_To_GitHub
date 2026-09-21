---
title: Pricing
status: unverified
tags: [pricing, licensing, ghec]
updated: 2026-09-04
---

**In one line:** GitHub charges per user with generous free tiers; Azure DevOps gives five users free then charges per user plus per-service costs — and since Feb 2025, GHEC includes Azure DevOps Basic for free.

> ⚠️ **Every figure on this page is unverified.** They come from a third-party comparison site and were captured in August 2026. Re-check against the vendors' own pricing pages before any of this goes on a slide.
>
> Source: <https://codepulsehq.com/guides/azure-devops-vs-github-guide>

## The headline

> The two platforms structure pricing differently. GitHub charges per user with generous free tiers. Azure DevOps gives five users free, then charges per user plus per-service costs.

## Captured figures

| Line item | GitHub | Azure DevOps |
|---|---|---|
| Free tier | Unlimited public repos, 2,000 Actions min/mo, 500 MB Packages | First 5 users free (Basic), 1 parallel job (1,800 min/mo), unlimited stakeholders |
| Entry paid | $4/user/mo, 3,000 Actions min/mo | $6/user/mo (after first 5) |
| Enterprise | $21/user/mo (GHEC), 50,000 Actions min/mo | $52/user/mo (Basic + Test Plans) |
| Additional CI/CD | $0.008/min overage (Linux) | $40/mo per additional parallel job (Microsoft-hosted) |
| Security scanning | Free for public repos, GHAS add-on for private | Azure Advanced Security: $49/active committer/mo |

## The unified licence — the detail most comparisons miss

> Since February 2025, the Basic Azure DevOps license is now included with GitHub Enterprise Cloud (GHEC). This means users can access both platforms without additional cost, provided they connect to Azure DevOps via Microsoft Entra ID. Their access level is automatically updated to "GitHub Enterprise", eliminating additional fees for Azure DevOps. This integration greatly simplifies the adoption of a hybrid approach, allowing enterprises to benefit from the best of both worlds.

Sources:
<https://learn.microsoft.com/en-us/azure/devops/release-notes/2025/sprint-252-update>
<https://devblogs.microsoft.com/devops/azure-devops-basic-usage-included-with-github-enterprise/>

> **Kevin:** This is the thing that makes the "just use both" answer genuinely free rather than a cop-out, and it's worth a slide of its own. It's also the least-known fact in the whole deck — most people in the room won't have heard it.

## Related

- [`03-decision-framework.md`](03-decision-framework.md) — "do not judge on sticker price alone"
