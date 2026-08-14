---
created: 13-07-2026
tags: [meta]
---

# README — manual actions

The second-brain system runs mostly on its own conventions (see `CLAUDE.md`), but a few things are deliberately manual — nothing here fires on a schedule. This file is the checklist for what Dave needs to trigger or decide himself.

## Vault stand-ups

- **`/vault-standup-work`** — Monday rolls up the prior Mon-Fri (bullet overview + links, added resources called out); Tue-Fri summarizes the day before; Sat/Sun no-ops. Writes into today's `01. Daily/DD-MM-YYYY-daily.md` (in `dAIve-work`) under `## Stand-up`. Re-running the same day appends only what's changed since the last run, it doesn't overwrite.
- **`/vault-standup-private`** — no schedule logic, run whenever. Refreshes the `## Daily` section in `00. To-do.md` (in `dAIve-private`) with open items, what changed since the last run, and flags. Same append-only behaviour on rerun.

Both also do light housekeeping (orphan notes, dedup, MOC links) scoped to their own vault, and surface two things for Dave to decide, never auto-applied:
- **Flagged `#to-do` / `#needs-review` items** touched in the period — just surfaced, not resolved.
- **Unconfirmed to-dos** — content that reads like an action item but isn't tagged yet. Shown as a question; tag it (or don't) yourself.

## Git

Both stand-ups only ever `git fetch` and compare local vs. origin — they will tell you if you're behind/ahead/diverged, but never pull, push, merge, or commit. If one flags you out of sync, resolve it yourself (or wait for the Obsidian Git plugin's own auto-commit/auto-push cycle to catch up). This applies per-repo — `dAIve-work`, `dAIve-private`, and `dAIve-shared` each sync independently.

## Periodic pruning

Nothing auto-deletes. These grow unless Dave trims them:
- `00. To-do.md` (in `dAIve-private`) — `## Active`/`## Someday` (done items) and `## Daily` (old stand-up entries).
- Any `#needs-review` flag, once actually resolved — strike it or remove it, the tag doesn't clear itself.

## Also see

- `CLAUDE.md` — shared conventions (language, tags, templates, session protocol); `VAULT-STRUCTURE.md` in each vault's own root for that vault's structure.
- `INSTALL.md` — new-device setup, including cloning all three repos and symlinking the two stand-ups above.
