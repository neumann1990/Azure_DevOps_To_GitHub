---
title: Validate a converted GitHub Actions workflow against its source
status: researched
tags: [prompts, ai-approach, pipelines, validation]
updated: 2026-09-21
---

**In one line:** Feed it both files — the original Azure Pipeline and the converted workflow — and ask it to check for behavior parity, not just YAML validity.

## The prompt

```
You are reviewing a GitHub Actions workflow that was converted from an
Azure Pipelines YAML file. Both files are attached. Do not just check
that the GitHub Actions YAML is syntactically valid — check that it
actually behaves the same as the original pipeline.

Go through this checklist explicitly, item by item, and answer for each:

1. STAGE/JOB PARITY: Does every stage and job in the original have a
   corresponding job in the converted workflow? List any that are
   missing, merged, or split, and whether that was called out in a
   change log.

2. DEPENDENCY PARITY: Do the `needs:` relationships in the converted
   workflow produce the same execution order as the `dependsOn:`
   relationships in the original? Trace through at least one full path
   from first job to last and confirm the order matches.

3. CONDITIONAL PARITY: For every `condition:` in the original, find its
   corresponding `if:` in the converted workflow and confirm the logic
   is equivalent, not just superficially similar. Watch specifically for
   sign errors (a condition that ran on failure now running on success,
   or vice versa) — this is the single most common conversion mistake.

4. SECRET/CREDENTIAL PARITY: For every service connection and variable
   group reference in the original, confirm the converted workflow
   authenticates to the same target using an appropriate GitHub Actions
   mechanism (OIDC, secret, or variable). Flag anything that looks like
   it lost a permission scope or changed authentication method without
   explanation.

5. SHELL AND ERROR-HANDLING PARITY: For every script step, confirm the
   converted workflow sets `shell:` explicitly rather than relying on
   GitHub Actions' Windows default (which differs from Azure Pipelines'
   default). Confirm any step that Azure Pipelines allowed to fail
   silently still fails silently in the converted workflow (via explicit
   `continue-on-error:`), rather than now stopping the whole workflow.

6. UNEXPLAINED GAPS: Anything in the original with no trace in the
   converted workflow, and no explanation in a change log for why it was
   dropped.

For each checklist item, answer PASS, FAIL, or NEEDS HUMAN REVIEW, with a
one-line reason. Do not mark anything PASS unless you actually traced the
logic — a structural resemblance is not parity.

<paste azure-pipelines.yml here>
<paste converted workflow.yml here>
<paste change log from the conversion step here, if one exists>
```

## Why this is a separate step from conversion

The same model that did the conversion is not a reliable check on its own
work — it tends to confirm its own assumptions rather than re-derive them.
Running validation as a distinct prompt, ideally in a fresh context or
even a different model, is what catches the sign-flipped conditional or
the quietly-dropped stderr behavior before it reaches a real pipeline.
This mirrors the general principle in [`../session/05-timing-draft-script.md`](../session/05-timing-draft-script.md)'s
adjacent point about not trusting a single pass at anything that matters.

## Related

- [`02-convert-pipeline-to-actions.md`](02-convert-pipeline-to-actions.md) — produces the two files this prompt checks
- [`../subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md) — source material for what parity actually means here
