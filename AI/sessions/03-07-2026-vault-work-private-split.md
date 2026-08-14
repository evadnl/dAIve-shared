---
created: 03-07-2026
project: "[[]]"
tags: [ai-session]
---

# Session Summary - Vault Work/Private Split

## What we did
- Follow-up to the Work/Private split below: renamed the three top-level folders with numeric prefixes so they sort above Areas/Archive/Templates/AI in the file explorer — `Inbox` → `01. Inbox`, `Private` → `02. Private`, `Work` → `03. Work` (order as Dave specified: Inbox, then Private, then Work). Areas/Archive/Templates/AI deliberately left unprefixed; digits already sort before letters so no changes were needed there.
- Updated all references to the renamed top-level paths in `CLAUDE.md`, the live nightly-review `SKILL.md`, and — while doing so — discovered `INSTALL.md` (the vault's own new-device setup doc) was already stale from the *original* Work/Private split, still describing the old flat `/People`, `/Projects` layout and an old commit/push step the live task no longer has. Confirmed via `list_scheduled_tasks` that the live task's prompt file is the actual source of truth, then brought `INSTALL.md` fully in sync with both the split and the rename.
- Left nested subfolders named "Work"/"Private" untouched (e.g. `01. Inbox/Work`, `AI/sessions/Private`) — those are context labels nested inside other folders, not the renamed top-level folders, so they keep their plain names.
- Confirmed via `git log` that the Obsidian Git plugin's auto-commit had already picked up the renames from its regular backup cycle by the time we checked — no manual commit needed.
- Restructured the vault (3 days old, previously fully mixed) into two confidentiality contexts: `/Work` (client engagements) and `/Private` (personal life), kept in one vault/git repo (folder-level separation only, not a repo split).
- Moved via `git mv` (history preserved):
  - Projects: Sawiday, Hitrail, Onderlinge → `Work/Projects/`; homelab → `Private/Projects/`.
  - People: all 14 existing notes → `Work/People/` (all were client-context people; `Private/People/` intentionally not created yet — on demand only).
  - Resources: `Consulting` → `Work/Resources/Consulting` (inherently work). `AWS`, `Kubernetes`, `Terraform` mirrored into both `Work/Resources/<Topic>` and `Private/Resources/<Topic>` (Dave confirmed he touches all three in both contexts, e.g. future homelab IPAM vs. client IPAM notes) — both stub index notes reworded to match their context.
  - Sessions: the 5 client-work session files from 02-07-2026 → `AI/sessions/Work/`. Vault-admin/meta sessions (`01-07-2026-second-brain-setup`, `01-07-2026-vault-review`, `03-07-2026-vault-review`) stay at `AI/sessions/` root.
  - Inbox: `02-07-2026-daily.md` (100% client-work content that day) → `Inbox/Work/`. `01-07-2026-second-brain-setup.md` and `03-07-2026-daily.md` stay at `Inbox/` root (meta content).
- Areas stays shared/unsplit at the vault root — the one deliberate exception.
- Rewrote `CLAUDE.md`'s vault structure and session protocol sections to document the new Work/Private convention, including the on-demand-creation rule for `Private/People` and any new Resources topic not yet needed in both contexts.
- Updated `~/.claude/CLAUDE.md` (global pointer used from other Claude Code sessions) so "log this to the vault" now routes into `AI/sessions/Work/` or `AI/sessions/Private/`, asking if context is unclear, falling back to the unsplit root only for vault/tooling-meta logs.
- Updated the nightly automation (`~/.claude/scheduled-tasks/vault-daily-review/SKILL.md`, outside the vault repo) to scan/create under the new Work/Private paths for orphan people/projects, treat Work↔Private mirrored Resources topics as intentional (not duplicates to merge), and write Overnight Review Flags into the correct context's daily note instead of a single shared one. The nightly review's own session summary stays at the vault root (it's a meta artifact, not Work or Private).
- Verified: `git status`/`diff --stat` showed clean renames only (no content loss besides the intentional AWS/Kubernetes/Terraform stub rewording); grepped the vault for any `[[Resources/...]]`, `[[People/...]]`, `[[Projects/...]]`-style links — found a few historical narrative references to `[[Resources/Consulting]]` in past session/daily logs, left as-is since Obsidian resolves wikilinks by filename fallback when the literal path doesn't match, and editing historical logs to reflect a location they didn't have at the time would misrepresent the record.

## Decisions
- One vault/git repo, split by top-level folder (`Work`/`Private`) rather than two separate vaults or repos — folder-level separation is sufficient for Dave's confidentiality concern; no repo-history isolation needed.
- Areas and Templates stay shared/unsplit; Resources splits (revised mid-session once Dave clarified he'll use it for context-specific reference material like IPAM).
- People all filed under Work for now; Private/People created only when an actual private-context person comes up, not pre-created.
- Resources topics: `Consulting` is Work-only; `AWS`/`Kubernetes`/`Terraform` mirrored under both contexts now since Dave already touches all three in both; new topics (e.g. Networking/IPAM) are created on demand under whichever context needs them first, mirrored to the other side only when genuinely needed there too.
- Vault-admin/tooling sessions and daily notes (nightly review, this restructuring) are exempt from the Work/Private split and stay at the root of `AI/sessions/` and `Inbox/`.
- Numbered top-level folders (`01. Inbox`, `02. Private`, `03. Work`) to force sort order in the file explorer; only these three get numbered since they're the ones Dave wants surfaced first, other top-level folders (Areas, Archive, Templates, AI) stay as-is.

## Next steps
- Dave to set up the matching clone + Git plugin on the work laptop (pre-existing open item from 01-07-2026) — now also means confirming that laptop only needs to see `03. Work` in practice, though the repo itself isn't split so both trees will be present either way.
- First time a private-context person or a new shared-topic Resources note comes up, confirm the on-demand-creation convention documented here is actually followed by future sessions/the nightly automation.
- Worth a periodic check that `INSTALL.md` hasn't drifted from the live `SKILL.md`/`CLAUDE.md` again — it silently went stale after the original split and was only caught because this session happened to grep for old paths.
