---
created: 01-07-2026
tags: [ai-session]
---

# Session Summary - 01-07-2026

## What we did
- Interviewed Dave on working style, values, communication preferences, and what he wants from an AI assistant; drafted `IDENTITY.md`, `SOUL.md`, `USER.md`.
- Persona named **Argus** after iterating through several options.
- Assessed the vault's existing PARA skeleton (Inbox, Areas, Projects, Resources, Archive, AI/sessions, Templates) — sound, but missing conventions.
- Built out subfolders under Areas (Work, Health, Finances) and Resources (AWS, Kubernetes, Terraform, Consulting), each with an index note.
- Created 5 note templates: Project, Client-Meeting, Debug-Note, Daily, Session-Summary. Removed the orphaned root `TEMPLATE.md`.
- Discussed multi-device sync (private Mac + work MacBook Pro): Obsidian Sync vs. Git — recommendation given, no decision made yet.
- Clarified that separate Claude Code sessions (different working directories) don't share this vault's context automatically. Added a one-line pointer in `~/.claude/CLAUDE.md` so any session knows the vault's path when told to "log this to the vault."
- Added 5 projects under `Projects/<client>/<project>`:
  - `Onderlinge/Pyriet-MSG` — AWS infra + EKS via CDK, ArgoCD-managed.
  - `homelab/kuppers.io` — full homelab automation (Proxmox → Terraform/OpenTofu, Kubernetes, Forgejo, ArgoCD, Atlantis, Renovate, Technitium DNS, domain migration).
  - `homelab/Zigbee-PoE-Coordinator` — USB → PoE Zigbee coordinator (SLZB-MR4U candidate), no-re-pair migration path.
  - `homelab/Unifi-Refresh` — Dream Machine → Cloud Gateway Max/Ultra, AP and camera refresh.
  - `Sawiday/DevOps` — advisory engagement assisting DevOps engineer Jeroen.
- Logged a dated update to `Sawiday/DevOps` covering Kubecost, EKS Pod Network Observability retention gap, Elasticsearch StackConfigPolicy changes, Osman/hours discussion, and Atlantis permissions.
- Updated root `CLAUDE.md` to reflect the actual structure: subfolder scheme, project note conventions, Archive trigger rule, template list, tag taxonomy.
- Caught and fixed a dating error (four notes created with `02-07-2026` instead of the actual `01-07-2026`).
- Added an end-of-session rule: decisions made in a session get logged both in the daily note (`## Decisions`) and in the related project's dated Notes entry (`**Decisions:**` block) — applied it retroactively to today's Sawiday entry, and added the format to `Templates/Project.md` as a hidden `%% %%` reminder block.
- Added a `People/` folder (parallel to Projects/Areas/Resources) and `Templates/Person.md`, documented in `CLAUDE.md`. Filed under full name (first + last) to avoid collisions, with first name as an `aliases` field for search convenience only.
- Created people notes: Jeroen Jans, Osman Yucekaya, Dennes Meeusen (Sawiday-related), and Daniel Vermeulen, Ronnie de Bont, Harry Huisman, Coen Griepsma, Peter Kruithof (Onderlinge Nederland) — linked from their respective project notes.
- Normalized `Onderlinge/Pyriet-MSG`'s `client` frontmatter from `Onderlinge` to `Onderlinge Nederland`.

## Decisions
- Persona: Argus.
- Vault structure: PARA, with the subfolder/template/tag conventions above.
- Cross-session vault logging: manual trigger ("log this to the vault"), not a global automatic protocol.

## Next steps
- Decide on multi-device sync method (Obsidian Sync vs. Git).
- Establish the weekly Inbox-review habit — the structure doesn't enforce itself.
- Flesh out task lists on the newer projects as scope clarifies (kuppers.io, Zigbee, Unifi-Refresh, Sawiday DevOps).
