---
title: Convert an Azure Pipeline to a GitHub Actions workflow
status: researched
tags: [prompts, ai-approach, pipelines, conversion]
updated: 2026-09-21
---

**In one line:** The actual conversion prompt — run it after the analysis pass, not instead of it.

## The prompt

```
You are converting an Azure Pipelines YAML file to an equivalent GitHub
Actions workflow. Apply these mapping rules exactly:

CONCEPT MAPPING
- A Pipeline becomes a Workflow.
- An Agent Pool becomes a `runs-on` runner. Map on-prem agent pools
  selected by *capability* to self-hosted runners selected by *label* —
  these are not the same selection mechanism, so don't assume a 1:1 name
  match.
- A Service Connection becomes OIDC federation, a secret, or a stored
  credential, depending on what it authenticates to. Default to OIDC for
  cloud provider connections (Azure, AWS) unless the pipeline clearly
  depends on a stored credential for a reason (e.g. a service that
  doesn't support OIDC).
- A Variable Group becomes GitHub Actions secrets and/or variables,
  split by whether the value is sensitive.
- A Task becomes an Action — prefer an official or verified Marketplace
  action over a raw `run:` shell command when one exists and matches the
  task's behavior; fall back to an equivalent shell command when it
  doesn't, and say so explicitly rather than silently approximating.
- `condition:` expressions become `if:` expressions, converted from
  function-call syntax to infix operator syntax.
- `dependsOn:` becomes `needs:`.
- Stages defined inline in one Azure Pipelines YAML file must become
  separate GitHub Actions workflow files (or clearly-separated jobs
  within one file, if the stages don't represent genuine sequential
  gating) — GitHub Actions has no single-file multi-stage construct.

SYNTAX AND BEHAVIOR DIFFERENCES — apply these, don't just translate keys
- Azure Pipelines lets a single-job pipeline skip explicit job structure.
  GitHub Actions requires explicit `jobs:` structure always — add it even
  where the source pipeline omitted it.
- All script step variants (`script:`, `bash:`, `powershell:`, `pwsh:`,
  and the Bash/PowerShell tasks) collapse to `run:` with an explicit
  `shell:` key. Always set `shell:` explicitly — do not rely on GitHub
  Actions' default (PowerShell on Windows runners), because the source
  pipeline's default was different (cmd.exe) and an unstated assumption
  here is exactly the kind of bug that surfaces three weeks after cutover.
- GitHub Actions fails fast by default; Azure Pipelines does not. If the
  source pipeline has steps that intentionally continue after a failing
  command, add explicit `continue-on-error: true` or equivalent — do not
  let GitHub Actions' default silently change this pipeline's behavior.
- Azure Pipelines can be configured to treat stderr output as a failure.
  GitHub Actions has no equivalent setting. If the source pipeline relies
  on this, flag it as a behavior that cannot be replicated directly and
  needs a workaround (e.g. explicit exit-code checking in the script).

OUTPUT
1. The complete GitHub Actions workflow YAML.
2. A change log: for every mapping decision above that required a
   judgment call (not a mechanical 1:1 substitution), state what you
   chose and why — especially the service-connection-to-OIDC decision,
   any Marketplace action substituted for a custom task, and any
   behavior difference (fail-fast, stderr, default shell) you had to
   compensate for.
3. A confidence flag (High / Medium / Low) per job, matching the risk
   rating from the analysis pass if one was done — a Manual-rated job in
   the analysis should not come back High confidence here without an
   explanation of what changed.

Do not silently drop anything from the source pipeline. If something has
no clean GitHub Actions equivalent, say so in the change log rather than
omitting it from the output.

<paste azure-pipelines.yml here>
```

## Why the change log matters more than the YAML

The YAML is the easy part to check — it either runs or it doesn't. The change log is where the actual risk lives: a service connection silently mapped to a stored secret instead of OIDC, or a stderr-triggers-failure behavior that just disappears. Reviewing the change log against [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md)'s syntax-differences list is the fastest way to catch a bad conversion before it reaches a real pipeline.

## Related

- [`01-analyze-azure-pipeline.md`](01-analyze-azure-pipeline.md) — run this first
- [`03-validate-converted-workflow.md`](03-validate-converted-workflow.md) — run this after, to check the output above
- [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — every rule above traces back to this doc
