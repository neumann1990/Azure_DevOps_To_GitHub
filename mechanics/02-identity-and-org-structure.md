---
title: Identity and org structure
status: researched
tags: [identity, emu, entra, permissions, org-structure]
updated: 2026-09-04
---

**In one line:** The structural mismatch nobody plans for — team projects don't exist on GitHub, and the enterprise-type choice (EMU vs personal accounts) is close to irreversible.

## The structural difference

**Azure DevOps:** repositories are nested inside *team projects*.

```
Organization → Team Project → Repository
```

Permissions and visibility flow from the team project.

**GitHub:** repositories are nested directly inside *organizations*, which also contain teams.

```
Enterprise → Organization → Repository
                         └→ Team
```

Permissions and visibility are determined by a combination of organization membership, team membership, and individual permissions.

> The concept of a team project, which is used to group repositories in Azure DevOps, does not exist in GitHub and treating organizations in GitHub as the equivalent of team projects is not recommended.

> While you may initially find each migrated organization on GitHub has a long unorganized list of repositories, you can grant access and permissions via teams of organization members, which makes navigating the organization's repositories a lot easier.

Source: <https://docs.github.com/en/migrations/ado/key-differences-between-azure-devops-and-github>

## Permissions are not migrated — teams are created instead

GEI does not attempt to migrate repository permissions, because the models differ. The ADO2GH CLI instead creates **two GitHub teams per Azure DevOps team project**:

| Team | Access to migrated repositories |
|---|---|
| `TEAM-PROJECT-Maintainers` | Maintainer |
| `TEAM-PROJECT-Admins` | Admin |

Populate them manually, or link them to Azure Active Directory groups during the migration and manage membership in AAD.

Source: <https://docs.github.com/en/migrations/ado/prepare-for-your-migration-from-azure-devops-to-github>

## Target structure

One enterprise account, and a small number of organizations owned by it. **Each Azure DevOps organization maps to a single GitHub organization** — not one organization per team project, which produces a large list of ungrouped repositories. Group repositories with teams instead.

## The migrator role

If the person running the migration isn't a GitHub organization owner, an owner must grant them the **migrator role** first. Two things stay owner-only regardless: assigning the migrator role, and reclaiming mannequins.

Source: <https://docs.github.com/en/migrations/ado/granting-the-migrator-role>

## Mannequins

During migration, Azure DevOps user accounts are imported as **mannequins** — placeholder accounts you then remap to real GitHub identities. All user activity in the migrated repository **except Git commits** is attributed to them. Plan the identity mapping before starting the migration, not after. Content attributed to a mannequin may not appear in search until the mannequin is reclaimed.

## Enterprise type: EMU vs personal accounts

Source: <https://docs.github.com/en/enterprise-cloud@latest/admin/concepts/enterprise-fundamentals/choose-an-enterprise-type>

### Enterprise Managed Users (EMU)

> Enterprise Managed Users may be right for your enterprise if you don't want enterprise members to use their own personal accounts to access your enterprise's resources.

> If you currently require your users to create a new personal account on GitHub.com to contribute to your company's resources, Enterprise Managed Users might be a better alternative.

What EMU gives you:

- You provision the accounts for your users
- You ensure user accounts conform with company identity, by controlling usernames and email addresses
- Users must authenticate with your identity management system, using SAML or OIDC
- A true SSO experience
- Users cannot create public repositories or other public content

### Personal accounts

> If you do not choose Enterprise Managed Users: each user must create, manage, and sign in to a personal account on GitHub.com.

- You can configure SAML authentication so users must authenticate to your external identity management system. GitHub links the personal account to an external identity.
- User provisioning is not available. You can use SCIM to provision to individual organizations.

> Consider personal accounts if using your external identity management system as the source of truth for user and access management would add too much complexity. For example, you do not have an established process for onboarding new users in the system.

## Decide before you create the enterprise account

GitHub's own guidance: decide whether your enterprise will use Enterprise Managed Users **before** creating the enterprise account. It determines how members authenticate and how you manage identities and access, and it is not a comfortable decision to revisit.

## The constraint that matters here

**Data residency requires EMU.** If Hunter ever pursues GHEC with data residency — the prerequisite for ELM — EMU comes with it. → [`04-data-residency.md`](04-data-residency.md)

## Entra ID

- Azure DevOps Basic is free with GHEC **only** when connecting via Entra ID → [`case/04-pricing.md`](../case/04-pricing.md)
- Azure DevOps has stopped accepting new OAuth app registrations; full OAuth platform retirement is coming, and teams must move to Entra ID
