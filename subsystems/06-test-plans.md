---
title: Test Plans
status: researched
tags: [test-plans, compliance, regulated]
updated: 2026-09-04
---

**In one line:** There is no GitHub equivalent. Keep Azure Test Plans or replace it with a third-party tool.

**Verdict: 🔴 Stays behind.**

## The whole story

> Azure Test Plans has no native GitHub Projects equivalent, which often matters in regulated environments.

Source: <https://learn.microsoft.com/en-us/azure/devops/test/overview>

Azure Test Plans provides manual and automated testing with detailed tracking. Nothing on the GitHub side covers structured manual and exploratory test case management.

## What this means

- If you need Azure Test Plans for structured manual and exploratory testing, that alone is a reason to keep Azure DevOps in the picture — see [`case/03-decision-framework.md`](../case/03-decision-framework.md)
- Under the hybrid pattern this is a non-issue: Test Plans stays where it is
- Under a full migration it's a procurement problem, not a migration problem

> **Kevin:** Shortest section in the deck and probably the best-received. Sometimes the honest answer is "it doesn't move, and that's fine."
