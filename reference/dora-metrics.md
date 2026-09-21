---
title: DORA metrics
status: unverified
tags: [dora, metrics, delivery-performance]
updated: 2026-09-04
---

**In one line:** The four delivery metrics both platforms can produce — useful as the common language when comparing dashboards, and as a section on how not to game them.

> ⚠️ **Source caveat.** The benchmark bands and framing below come from CodePulse's guides, a vendor with a product in this space. The four metrics themselves are standard (DORA / Accelerate); the specific band boundaries here should be checked against the official DORA reports before they go on a slide.
>
> Sources: <https://codepulsehq.com/guides/dora-metrics-guide> · <https://codepulsehq.com/guides/dora-metrics-guide#four-key-metrics>

## The four metrics

**1. Deployment Frequency** — how often your organization deploys code to production.

> Deployment frequency is a proxy for batch size. Teams that deploy frequently ship smaller changes. Smaller changes are easier to review, easier to test, and easier to roll back when something breaks.

*Gamed by:* splitting PRs into tiny fragments or deploying empty changes. A team deploying 10 times a day while shipping nothing meaningful isn't "elite" — they're just busy.

**2. Lead Time for Changes** — the time from code commit to production deployment.

> Lead time reveals the friction in your delivery pipeline. Long lead times point to bottlenecks — slow code review, manual testing gates, complex deployment processes, or approval bureaucracy.

*Gamed by:* skipping reviews or reducing test coverage. "Your lead time dropped from 3 days to 3 hours — but now you're shipping bugs straight to production."

> "A 3-day lead time with thorough review beats a 3-hour lead time with no review. The metric doesn't capture what you skipped."

**3. Change Failure Rate** — the percentage of deployments that cause a failure requiring remediation (rollback, hotfix, or patch).

> Change failure rate is the quality counterbalance to velocity metrics. High deployment frequency only matters if those deployments work. This metric catches teams that game velocity by shipping broken code.

*Gamed by:* under-reporting failures or defining "failure" narrowly. "If hotfixes don't count and rollbacks are 'planned,' your 5% failure rate is a lie."

**4. Mean Time to Recovery (MTTR)** — how long it takes to restore service when an incident occurs.

> MTTR measures your incident response capability. Low MTTR requires good monitoring (you detect problems fast), good runbooks (you know what to do), and practiced response (you've done this before).

*Gamed by:* not declaring incidents, or declaring resolution before customers are actually unaffected.

## Benchmark bands

⚠️ Band boundaries unverified — see caveat above.

**Deployment frequency**

| Band | Value |
|---|---|
| Elite | Multiple deploys per day |
| High | Between once per day and once per week |
| Medium | Between once per week and once per month |
| Low | Less than once per month |

**Lead time for changes**

| Band | Value |
|---|---|
| Elite | Less than one hour |
| High | Less than one day |
| Medium | Between one day and one week |
| Low | More than one week |

**MTTR**

| Band | Value |
|---|---|
| Elite | Less than one hour |
| High | Less than one day |
| Medium | Between one day and one week |
| Low | More than one week |

> ⚠️ The notebook captured overlapping band values ("between one week and one month", "more than one month") without clearly attributing them to a specific metric. Reconstruct from the source before use.

## Improving them without gaming them

> The right way to improve DORA metrics is to improve the capabilities they reflect — not to optimize for the numbers directly.

**To improve deployment frequency**

- *Automate deployments.* Manual deployment processes are the biggest barrier.
- *Use feature flags.* Decouple deployment from release — ship code that's not yet visible to users.
- *Build confidence.* Good monitoring lets you deploy with less fear.

**To reduce lead time**

- *Speed up code review.* Usually the biggest bottleneck.
- *Reduce batch size.* Smaller PRs are easier to review, test and deploy.
- *Parallelize CI.* Slow test suites add hours to every PR.
- *Eliminate manual gates.* Each approval step adds delay. Question whether each gate adds value.
- *Practice trunk-based development.* Long-lived branches accumulate merge conflicts that slow everything down.

**To reduce change failure rate**

- *Improve test coverage.* Automated tests catch issues before production.
- *Use progressive rollouts.* Canary deployments limit blast radius.
- *Build better staging environments.* Production-like environments catch environment-specific issues.
- *Invest in code review.* Human review catches what tests miss.

**To reduce MTTR**

- *Invest in observability.* You can't fix what you can't see.
- *Enable easy rollbacks.* The ability to undo a deployment instantly drops MTTR dramatically.
- *Create runbooks.* Documented procedures speed recovery.
- *Practice incident response.* Game days build muscle memory.

## Why this is in the deck

Both platforms can produce these four numbers. Comparing DORA metrics is a more honest comparison than comparing dashboard widgets, and it sidesteps the feature-matrix argument the talk is deliberately not having. → [`subsystems/07-dashboards-and-analytics.md`](../subsystems/07-dashboards-and-analytics.md)
