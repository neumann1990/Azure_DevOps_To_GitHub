---
title: GEI repository migration runbook
status: researched
tags: [gei, gh-ado2gh, runbook, cli, procedure]
updated: 2026-09-20
---

**In one line:** The official six-part GitHub procedure for migrating repositories from Azure DevOps to GitHub Enterprise Cloud with the `gh-ado2gh` extension, start to finish.

Source: <https://docs.github.com/en/migrations/ado> — all six steps captured below. Where these notes previously relied on third-party summaries, this page supersedes them.

---

## 0. Hard constraints, before anything else

**Azure DevOps Cloud only.** GEI cannot migrate from Azure DevOps _Server_. If you're on Server, migrate to Azure DevOps Cloud first ([Microsoft's migration service](https://azure.microsoft.com/en-us/services/devops/migrate/)), then run GEI.

**Decide your enterprise type before creating the enterprise account.** Whether you use Enterprise Managed Users affects how members authenticate and how you manage identities and access — and it's not a decision you want to revisit later. → [`02-identity-and-org-structure.md`](02-identity-and-org-structure.md)

**No delta migrations.** The Importer doesn't support them. Any change made during the migration will not migrate, and has to be moved by hand afterwards. GitHub recommends halting work in the repositories being migrated.

**Pipelines are out of scope.** "If you want to migrate Azure Pipelines to GitHub Actions, contact your GitHub account manager." Both Azure Pipelines and Azure Boards can stay fully integrated with GitHub instead. → [`subsystems/02-pipelines-and-actions.md`](../subsystems/02-pipelines-and-actions.md)

Source: [Understand migrations](https://docs.github.com/en/migrations/ado/understand-migrations-from-azure-devops-to-github)

---

## Step 1 — Understand what actually migrates

### Data that is migrated

- Git source (including commit history)
- Pull requests
- User history for pull requests
- Work item links on pull requests
- Attachments on pull requests
- Branch policies for the repository — _user-scoped branch policies and cross-repo branch policies are **not** included_

### Limitations of GitHub

| Limit                     | Detail                                                                                                                       |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **2 GiB per Git commit**  | No single commit can exceed 2 GiB. Split larger commits.                                                                     |
| **2 GiB per push**        | Larger pushes fail with `pack exceeds maximum allowed size`.                                                                 |
| **255 bytes per Git ref** | Usually ~255 characters, but non-ASCII characters (emoji) consume more than one byte. A clear error is returned if exceeded. |
| **100 MiB per file**      | After migration completes. During migration the limit is raised to 400 MiB. Use Git LFS for large files.                     |

### Limitations of GitHub Enterprise Importer

| Limit                                          | Detail                                                                                                                                                                                                                          |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **40 GiB per Git repository** (public preview) | Applies to source code only. Check with [git-sizer](https://github.com/github/git-sizer) and review total blob size. git-sizer also surfaces large-file, blob-size, commit-size and tree-count problems that affect migrations. |
| **400 MiB per file**                           | During migration.                                                                                                                                                                                                               |
| **Git LFS objects are not migrated**           | Repositories _using_ LFS migrate fine, but the LFS objects themselves don't come across. Push them to the destination as a follow-up task.                                                                                      |
| **Delayed code search**                        | Re-indexing can take a few hours; code searches may return unexpected results until it finishes.                                                                                                                                |
| **Org rulesets can fail the migration**        | E.g. a rule requiring commit author emails to end `@monalisa.cat` will fail a migration containing non-compliant commits. See Step 2.                                                                                           |
| **Mannequin content may not be searchable**    | Content attributed to a mannequin (assigned issues, etc.) may not surface in search until the mannequin is reclaimed.                                                                                                           |

> **Kevin:** The LFS gap and the 40 GiB ceiling are the two that will bite a real enterprise estate, and neither appeared in the third-party guides I'd collected. Worth a slide — "Git is Git" is true right up until it isn't.

---

## Step 2 — Manage access

Source: [Manage access](https://docs.github.com/en/migrations/ado/manage-access)

### Who performs the migration

If the person running the migration is **not** a GitHub organization owner, an organization owner must first grant them the **migrator role**. Do this before they start the rest of the setup.
See [Granting the migrator role](https://docs.github.com/en/migrations/ado/granting-the-migrator-role).

### GitHub personal access token (classic)

> **Classic tokens only.** Fine-grained PATs are not supported. This means GEI cannot be used if your organization enforces the _"Restrict personal access tokens (classic) from accessing your organizations"_ policy.

> **Kevin:** Confirmed hands-on during the PoC — `gh-ado2gh` rejects a fine-grained `GH_PAT` outright. Had to generate a classic token instead. Budget time for this if your org defaults to fine-grained tokens or has started phasing out classic ones. You'll also need to explicitly assign your PAT access to your organization.

Required scopes depend on role and task:

| Task                                                      | Organization owner              | Migrator                       |
| --------------------------------------------------------- | ------------------------------- | ------------------------------ |
| Assigning the migrator role for repository migrations     | `admin:org`                     | —                              |
| Running a repository migration (destination organization) | `repo`, `workflow`, `admin:org` | `repo`, `workflow`, `read:org` |
| Downloading a migration log                               | `repo`, `workflow`, `admin:org` | `repo`, `workflow`, `read:org` |
| Reclaiming mannequins                                     | `repo`, `workflow`, `admin:org` | —                              |

### Azure DevOps personal access token

Scopes: `work item (read)`, `code (read)`, `identity (read)`.

GitHub recommends granting **full access** so the `inventory-report` command works in Step 4. To migrate from multiple organizations, allow the token to access all accessible organizations.

See [Use personal access tokens](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=preview-page#create-a-pat).

### GitHub IP allow list

If you use GitHub's IP allow list, add these ranges for the source and/or destination organizations:

```
192.30.252.0/22
185.199.108.0/22
140.82.112.0/20
143.55.64.0/20
135.234.59.224/28   (added July 28, 2025)
2a0a:a440::/29
2606:50c0::/32
20.99.172.64/28     (added July 28, 2025)
```

### IdP restrictions

If you use an identity provider's IP allow list (such as Azure CAP) to restrict access to your GitHub enterprise, disable those restrictions in enterprise account settings until the migration is complete.

### Ruleset bypass

If the destination organization or enterprise has rulesets enabled, migrated history may violate them. Rather than disabling rulesets:

1. Navigate to each enterprise or organization ruleset.
2. In the **Bypass list** section, click **Add bypass**.
3. Select **Repository migrations**.

The bypass applies only during migration; rulesets are enforced on all new contributions afterwards.

---

## Step 3 — Install and configure the importer

Source: [Install and configure GitHub Enterprise Importer](https://docs.github.com/en/migrations/ado/install-and-configure-github-enterprise-importer)

### Install

GitHub CLI **2.4.0 or newer** is required — check with `gh --version`.

```shell
gh extension install github/gh-ado2gh
```

The extension is updated **weekly**. Before each migration session:

```shell
gh extension upgrade github/gh-ado2gh
```

Help is available per-command:

```shell
gh ado2gh --help                  # list all commands
gh ado2gh migrate-repo --help     # options for one command
```

### Environment variables

`GH_PAT` for the destination organization, `ADO_PAT` for the source.

Terminal / bash:

```shell
export GH_PAT="TOKEN"
export ADO_PAT="TOKEN"
```

PowerShell:

```shell
$env:GH_PAT="TOKEN"
$env:ADO_PAT="TOKEN"
```

If migrating to GHE.com (data residency), also set the base API URL — replace `SUBDOMAIN` with your enterprise subdomain, e.g. `acme` → `https://api.acme.ghe.com`:

```shell
export TARGET_API_URL="https://api.SUBDOMAIN.ghe.com"
```

```shell
$env:TARGET_API_URL="https://api.SUBDOMAIN.ghe.com"
```

Used with the `--target-api-url` option on subsequent commands. → [`04-data-residency.md`](04-data-residency.md)

---

## Step 4 — Prepare

Source: [Prepare for your migration](https://docs.github.com/en/migrations/ado/prepare-for-your-migration-from-azure-devops-to-github)

### Take inventory

> Migration timing is largely based on the **number of pull requests** in a repository. If you want to migrate 1,000 repositories, and each repository has 100 pull requests on average, your migration will likely be very quick. If you want to migrate only 100 repositories, but the repositories each have 75,000 pull requests on average, the migration will take much longer and require more planning and testing.

```shell
gh ado2gh inventory-report --ado-org YOUR_ADO_ORG
```

Connects to the Azure DevOps API and writes several CSV files. `repos.csv` contains repository information including pull request counts.

> **Kevin:** PR count, not repo count, is the thing that drives the schedule. That's counter-intuitive enough to be a good slide — the instinct is to size a migration by number of repos.

Then weigh inventory against timeline:

- Higher tolerance for change → migrate everything at once, done in a few days
- Teams that can't move together → batch and stagger, extending the effort

### Plan the org structure

- **Azure DevOps:** Organization → team project → repositories
- **GitHub:** Enterprise → organization → repositories

Target end state: **one enterprise account** and a small number of organizations. Each Azure DevOps organization should correspond to a single GitHub organization.

> The concept of a team project, which is used to group repositories in ADO, does not exist in GitHub. We do not recommend creating an organization on GitHub for each team project on ADO, as this may result in a large list of ungrouped repositories within each organization. However, you can manage access to groups of repositories by creating teams.

If batching: with more than one Azure DevOps organization, and each organization's repositories a reasonable batch size, batch by organization.

### Repository permissions are not migrated

Because permissions work differently, GEI **does not attempt to migrate repository permissions** from Azure DevOps.

Instead, the ADO2GH CLI creates **two GitHub teams per Azure DevOps team project**:

| Team                       | Access to migrated repositories |
| -------------------------- | ------------------------------- |
| `TEAM-PROJECT-Maintainers` | Maintainer                      |
| `TEAM-PROJECT-Admins`      | Admin                           |

Grant access by adding people to these teams — manually, or by managing group membership in Azure Active Directory if you linked the teams to AAD groups during migration.

---

## Step 5 — Migrate

Source: [Migrate your repositories](https://docs.github.com/en/migrations/ado/migrate-your-repositories-from-azure-devops-to-github)

### Generate a migration script

Produces one migration command per repository.

> **Note:** the generated script is **PowerShell**. On macOS or Linux, give it a `.ps1` extension and install PowerShell to run it.

```shell
gh ado2gh generate-script --ado-org SOURCE --github-org DESTINATION --output FILENAME
```

| Placeholder   | Value                                         |
| ------------- | --------------------------------------------- |
| `SOURCE`      | Name of the source organization               |
| `DESTINATION` | Name of the destination organization          |
| `FILENAME`    | Filename for the generated script; use `.ps1` |

Additional arguments:

| Argument                          | Description                                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------------------------ |
| `--target-api-url TARGET-API-URL` | For GHE.com. Base API URL for your enterprise subdomain, e.g. `https://api.octocorp.ghe.com`     |
| `--all`                           | Adds rewiring pipelines, creating teams, and configuring Azure Boards integrations to the script |
| `--download-migration-logs`       | Downloads the migration log for each migrated repository                                         |

> **Kevin:** `--all` is the flag that does the Boards-connection and pipeline-rewiring work — the same class of post-migration setup ELM automates. Worth naming explicitly when I draw the ELM-versus-GEI contrast, so the comparison is honest rather than flattering to ELM. → [`03-enterprise-live-migrations.md`](03-enterprise-live-migrations.md)

### Review and edit the script

- Delete or comment out lines for repositories you don't want to migrate
- Change a destination name via that line's `--target-repo` flag
- Change visibility via `--target-repo-visibility`; by default it matches the source

### Trial run

Trial runs can happen any time and don't require halting work. They tell you whether a repository migrates successfully, whether you can get it back to a workable state, and how long it takes.

1. Create a test organization — one for all trials, or one per intended destination. Suffix names with `-sandbox` to make their purpose obvious.
2. Run the trial migrations. Schedule batches back-to-back to compress elapsed time; users validate on their own schedule.
3. Confirm you can complete the Step 6 follow-up tasks.
4. Ask users to validate the results.
5. Resolve issues found.
6. Optionally delete the test organization.

### Production migration

> **Warning:** halt work in the repositories being migrated. Any changes made during or after the migration must be migrated manually.

```shell
./FILENAME      # Terminal
```

```shell
.\FILENAME      # PowerShell
```

---

## Step 6 — Follow-up tasks

Source: [Follow-up tasks](https://docs.github.com/en/migrations/ado/follow-up-tasks)

### Check migration status

Run in the foreground, the CLI reports the outcome:

```text
Migration completed (ID: RM_123)! State: SUCCEEDED
```

With `--queue-only`, the process exits immediately after queueing and reports nothing. Check with the `wait-for-migration` command or the migration log.

### Review the migration log

One per migrated repository, readable by anyone with read access:

1. Navigate to the migrated repository in the destination organization
2. Click **Issues**
3. Open the issue titled **"Migration Log"**

### Set repository visibility

All repositories migrate as **private**, accessible only to the migration runner and organization owners. Change visibility in the browser, or in bulk:

```bash
export ORG=YOUR_ORG
gh repo list "$ORG" --limit 100000 --json name -q '.[].name' | xargs -I{} gh repo edit "$ORG/{}" --visibility internal
```

### Reclaim mannequins

All user activity in the migrated repository **except Git commits** is attributed to mannequins.

> **Note:** only organization owners can reclaim mannequins. If you hold the migrator role, you need an owner for this step.

1. Decide whether to reclaim
2. Plan when
3. Reclaim — via GitHub CLI (supports bulk) or browser. See [Reclaiming mannequins](https://docs.github.com/en/migrations/using-github-enterprise-importer/completing-your-migration-with-github-enterprise-importer/reclaiming-mannequins-for-github-enterprise-importer)
4. Give members repository access if they don't already have it via team membership

### Restore network restrictions

Remove the GEI IP ranges from the destination organization's allow list, and re-enable the IdP IP allow list restrictions disabled in Step 2.

### Reconnect Azure Pipelines and Azure Boards

- [Connect Azure Pipelines to GitHub](https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/github)
- [Configure the Azure Boards app for GitHub](https://learn.microsoft.com/en-us/azure/devops/boards/github/install-github-app)

### Support your developers

Share [Key differences between Azure DevOps and GitHub](https://docs.github.com/en/migrations/ado/key-differences-between-azure-devops-and-github). → [`02-identity-and-org-structure.md`](02-identity-and-org-structure.md)

---

## Beyond the six steps

- [Migrate with the GraphQL API](https://docs.github.com/en/migrations/ado/use-graphql-to-migrate-repositories-from-azure-devops-to-github-enterprise-cloud) — for scripted or custom migration flows
- [Granting the migrator role](https://docs.github.com/en/migrations/ado/granting-the-migrator-role)
- [Troubleshooting your migration](https://docs.github.com/en/migrations/troubleshooting/troubleshooting-your-migration-with-github-enterprise-importer)
- [Accessing migration logs](https://docs.github.com/en/migrations/using-github-enterprise-importer/completing-your-migration-with-github-enterprise-importer/accessing-your-migration-logs-for-github-enterprise-importer)
