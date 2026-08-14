---
created: 01-07-2026
tags: [daily]
---

# 01-07-2026

## Agent Log
- Interviewed Dave to draft IDENTITY.md, SOUL.md, USER.md — persona named Argus.
- Reviewed vault structure, proposed and built out PARA-based organization: subfolders under Areas (Work, Health, Finances) and Resources (AWS, Kubernetes, Terraform, Consulting), each with an index note.
- Created 5 templates (Project, Client-Meeting, Debug-Note, Daily, Session-Summary), removed orphaned root TEMPLATE.md.
- Discussed multi-device sync options (Obsidian Sync vs. Git) — no decision made yet.
- Clarified that a Claude Code session elsewhere doesn't know this vault's path automatically; added a one-line pointer to `~/.claude/CLAUDE.md` (global) so "log this to the vault" works from any session.
- Added 5 projects: Onderlinge/Pyriet-MSG, homelab/kuppers.io, homelab/Zigbee-PoE-Coordinator, homelab/Unifi-Refresh, Sawiday/DevOps — each with objective/context/tasks.
- Logged today's Sawiday DevOps update (Kubecost, EKS Pod Network Observability, Elasticsearch StackConfigPolicy, Osman hours discussion, Atlantis permissions).
- Updated root `CLAUDE.md` to document the actual folder structure, project note conventions, Archive rule, and tag taxonomy.
- Added end-of-session rule: decisions get logged both here and in the related project's Notes section.
- Added a `People/` folder and `Templates/Person.md`; documented it in `CLAUDE.md`.
- Created people notes for Sawiday (Jeroen Jans, Osman Yucekaya, Dennes Meeusen) and Onderlinge Nederland (Daniel Vermeulen, Ronnie de Bont, Harry Huisman, Coen Griepsma, Peter Kruithof); linked them from the relevant project notes.
- Resolved the multi-device sync question raised earlier (see Decisions): vault is now a git repo with the Obsidian Git plugin auto-pushing. Set up a nightly scheduled task (`vault-daily-review`, 00:01) that fetches/compares HEAD before acting, creates orphan People/Project notes, consolidates duplicates, updates MOCs, and flags strategic items — with an idempotency check so it's safe to run on both this Mac and the work laptop.

## Decisions
- Multi-device sync: chose git over relying solely on Obsidian Sync. Obsidian Git plugin configured with auto-push on this Mac; vault has a private remote. Work laptop got a matching clone + Git plugin setup on 02-07-2026 (confirmed done).
- [[Sawiday/DevOps]]: Kubecost not adopted for now (manual Helm install instead); Elasticsearch StackConfigPolicy lifecycle policies moved into product cluster values as a plain list, `base_path` defaults to `elasticsearch` with per-environment override.
- People notes are filed under full name (first + last) to avoid collisions, with first name as an `aliases` entry for search convenience only — not a guaranteed link target.
- [[Onderlinge/Pyriet-MSG]]: normalized the project's `client` frontmatter from `Onderlinge` to `Onderlinge Nederland` to match the People notes.
