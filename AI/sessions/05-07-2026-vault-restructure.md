---
created: 05-07-2026
project: "[[]]"
tags: [ai-session]
---

# Session Summary - 05-07-2026

## What we did
- Explored alternatives to PARA (Johnny Decimal, Zettelkasten, LATCH, GTD, CODE, tags-as-context, MOC), focused on which ones give a real structural Work/Private boundary rather than just a workflow overlay.
- Diagnosed the actual complaint: PARA organizes by actionability first, so any topic with both active work and reference material (Homelab, a client) ends up split across two separate top-level trees (`Projects/<topic>` and `Resources/<topic>`).
- Designed a custom domain-first method from scratch, collaboratively, before touching any files:
  - Two top levels stay `01. Private` / `02. Work`, but everything else (Inbox, Archive, Areas) now nests inside them instead of sitting as separate top-level siblings.
  - A **domain** = anything with enough going on to deserve its own folder (Homelab, Career, a client) — each defines its own subfolders freely instead of being forced into the same Projects/Resources shape.
  - Numbering convention: low numbers for frequently-used domains, `25.` for Resources (headroom for future domains), `98.` for Archive, `99.` for Inbox.
  - Archive is per-domain (finished projects within an active domain) *and* per-context (`98. Archive` for entire domains/clients that end).
  - Work clients live under a `Clients/` wrapper; Private domains sit directly under Private (not a roster the way clients are).
  - Work gets `01. Daily/` (dated work log); Private drops daily notes entirely in favor of one running `00. To-do.md`.
  - People sits alongside Clients/domains, not nested inside one.
- Executed the full restructure: renumbered/moved every folder, deleted the unused `Areas/Health.md` and `Areas/Finances.md` stubs outright (not migrated), moved `Areas/Work.md` → `01. Private/02. Career/Career.md`, deleted a stray empty duplicate (`Onderlinge/Pyriet-MSG.md` at vault root), rewrote `CLAUDE.md` to describe the new method, and updated `INSTALL.md`, the global `~/.claude/CLAUDE.md` pointer, and the live `vault-daily-review` scheduled task's prompt to match.
- Fixed a Folder Notes bug: `Hosts.base` stopped being clickable via its folder because the plugin requires the folder-note filename to exactly match the folder's name, and the file wasn't renamed when the folder was renumbered.
- Converted Homelab's IPAM from one big table note into the same pattern Hosts already used: 8 individual VLAN notes + a matching Folder Notes `.base` for the clickable table (added a new `VLAN` template). Retired `Homelab IPAM.md`, kept Reserved-ranges/Log content in a new `IPAM Notes.md`, repointed all 17 `[[Homelab IPAM]]` references vault-wide.
- Investigated the Iconic plugin (icons/colors) at Dave's request: confirmed Folder Rules can cascade a color/icon to every folder under a path without touching manually-set colors, but discovered (after Dave saw it happen) that an enabled rule actually overrules per-folder icons entirely — traced this to the plugin's own "overrule" warning mechanism in its code. Fixed by disabling the rule and setting `color` directly on each folder's own icon entry instead, alongside its existing icon.
- Split the 5 physical network devices (routers/switches/APs — identifiable by carrying all 8 VLANs instead of one) out of `Hosts` into a new `Infra` folder with its own Base.
- Renumbered Homelab's subfolders to Dave's final preference — `02. Infra`, `03. Hosts`, `04. IPAM` — cascading the rename through each folder, its Folder Notes `.base` file, its internal filter, every `[[...IPAM.base]]` reference, `CLAUDE.md`, and the Iconic icon assignments (which briefly got orphaned since the rename happened outside Obsidian's own tracking).

## Decisions
- Moved the vault off PARA entirely onto a custom domain-first method — kept PARA's vocabulary (Projects/Resources/Archive) as subfolder concepts, but topic/domain is now the primary organizing axis, not actionability.
- Numbering: low numbers = frequent domains, `25.` Resources, `98.` Archive, `99.` Inbox — gaps left on purpose so new domains can be inserted without renumbering everything.
- Archive is per-domain *and* per-context (whole-domain retirement vs. single finished project).
- Work: `Clients/` wrapper folder for the client roster; `01. Daily/` replaces Inbox's old daily-note role.
- Private: no daily notes — a single running `00. To-do.md` instead; no `Clients`-style wrapper since Private's domains aren't a roster.
- `Areas/Health.md` and `Areas/Finances.md` deleted outright (unused, not migrated) — Dave will re-add if/when needed, per the vault's existing "don't pre-create empty topics" convention.
- Homelab's Hosts/IPAM graduate from a single reference note to individual entity notes + a Folder Notes `.base` once a registry has enough discrete items to justify it (VLAN template added to mirror Host).
- Physical network devices are a distinct domain sub-folder (`Infra`) from compute hosts (`Hosts`), split by whether the device carries all VLANs vs. sits on one.
- Iconic Folder Rules cannot do "color-only, keep custom icon" — an enabled rule overrules matched items' icons entirely. Per-folder individual color assignment is the correct mechanism for that instead.
- Final Homelab subfolder order: `02. Infra`, `03. Hosts`, `04. IPAM` (Dave's explicit final call, reordered once after initial implementation).

## Next steps
- ~~Dave to open Obsidian and confirm the `02. Infra`, `03. Hosts`, and `04. IPAM` Bases still render/click correctly after the renumbering, and re-check/adjust Iconic icons where needed.~~ Confirmed 05-07-2026: Bases render/click correctly and Iconic icons are OK.
- No outstanding to-dos from this session — everything discussed was implemented in-session and verified.
