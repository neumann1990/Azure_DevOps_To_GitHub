---
title: Data residency
status: researched
tags: [data-residency, ghec, emu, compliance, blocker]
updated: 2026-09-04
---

**In one line:** A distinct GHEC deployment model on a dedicated `ghe.com` subdomain — and the gate that blocks ELM for Hunter.

## What it actually is

GitHub Enterprise Cloud with Data Residency is a distinct deployment model where:

- You choose the geographic region where your code and repository data are stored (currently including U.S., EU, Australia and Japan)
- Your enterprise is hosted on a dedicated `ghe.com` subdomain
- The environment is isolated from the broader github.com ecosystem
- It requires Enterprise Managed Users (EMU)

Source: <https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency>

> To help you meet compliance requirements, GitHub Enterprise Cloud includes the option to store your enterprise's code and data in a specific region, on your own subdomain of GHE.com.

## Why it matters here

| | |
|---|---|
| Hunter's status | **Does not currently use data residency** |
| Consequence | Enterprise Live Migrations cannot be trialled → [`03-enterprise-live-migrations.md`](03-enterprise-live-migrations.md) |
| Knock-on | Data residency requires EMU, which changes the whole identity model → [`02-identity-and-org-structure.md`](02-identity-and-org-structure.md) |

## For the talk

This is a genuinely useful ten-second filter for the audience: if you're not on `<enterprise>.ghe.com`, ELM isn't available to you, and the GEI + Actions Importer path is your route. Most of the room will be in the same position.
