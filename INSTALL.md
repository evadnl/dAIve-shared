---
created: 01-07-2026
tags: [meta]
---

# INSTALL — setting up this system on a new device

The second-brain system is three repos: `dAIve-work`, `dAIve-private`, and this one, `dAIve-shared`. `dAIve-work` and `dAIve-private` each symlink `Templates`, `CLAUDE.md`, `IDENTITY.md`, `SOUL.md`, and `USER.md` from `dAIve-shared`, so all three repos must sit as siblings in the same parent folder on every device — the symlinks are relative (`../dAIve-shared/...`) and won't resolve otherwise.

Two more things live *outside* all three repos on each machine and won't follow the clone automatically: the global Claude Code pointer, and the vault stand-up skills (`vault-standup-work` / `vault-standup-private`). Do all of this on every new device (e.g. work laptop) — though on a device meant to hold only Work (device/sync isolation was the point of the split), skip cloning `dAIve-private` and skip installing `vault-standup-private`.

## 1. Clone the three repos as siblings

```
git clone git@github.com:evadnl/dAIve-shared.git
git clone git@github.com:evadnl/dAIve-work.git
git clone git@github.com:evadnl/dAIve-private.git
```

Put them side by side wherever that device's Obsidian vaults live (e.g. `~/dAIve/dAIve-shared`, `~/dAIve/dAIve-work`, `~/dAIve/dAIve-private`). Note each full local path — you'll need `dAIve-work`'s and `dAIve-private`'s below (referred to as `<WORK_VAULT_PATH>` / `<PRIVATE_VAULT_PATH>`).

`dAIve-shared` is not opened as an Obsidian vault — it just needs to exist as a sibling folder so the symlinks in the other two resolve.

## 2. Point Obsidian at each vault, enable auto-sync

For both `dAIve-work` and `dAIve-private`:

1. Open the cloned folder as a vault in Obsidian.
2. Install/enable the **Obsidian Git** community plugin.
3. Configure it the same way as the primary Mac: auto-commit on an interval, auto-push after commit. (Match whatever interval you're running there — check Settings → Community Plugins → Git on that machine if unsure.)

This is what lets changes flow both ways without manual `git` commands. `dAIve-shared` also needs periodic syncing on each device (`git pull` — it has no Obsidian Git plugin of its own since it's not opened as a vault), otherwise Templates/CLAUDE.md/etc. go stale on that device.

## 2a. Community plugins, core plugins, and appearance

Each vault's `.obsidian/` is committed, so plugin files and settings clone with it — but Obsidian only *enables* plugins listed in `.obsidian/community-plugins.json` on startup, and it will silently disable a plugin (without editing that file back) if one throws an error on load. If a folder/table/icon behaves oddly on a new device, check Settings → Community Plugins against this list first. Both `dAIve-work` and `dAIve-private` are seeded with the same plugin set.

Community plugins (`.obsidian/community-plugins.json`), all required:
- **obsidian-git** — two-way git sync (see step 2 above)
- **dataview** — powers dataviewjs queries (e.g. the Private vault's `01. Homelab/04. IPAM.md` active-IP-assignments table)
- **folder-notes** — makes clicking a folder open its matching note/Base table (e.g. `02. Infra`, `03. Services`); also needs the **Bases** core plugin (below)
- **obsidian-icon-folder** — custom folder/file icons; uses the `simple-icons` icon pack under `.obsidian/icons/`
- **obsidian-style-settings** — exposes other plugins'/themes' CSS variables as settings UI

Core plugins (`.obsidian/core-plugins.json`) — mostly defaults, with one non-default flip worth knowing:
- **Bases** — enabled; required for `.base` folder-note tables (`02. Infra.base`, `03. Services.base`)

Appearance (`.obsidian/appearance.json`):
- Theme: **Catppuccin** (community theme, files under `.obsidian/themes/Catppuccin/`, clones with the vault)
- Font: **JetBrainsMono Nerd Font** (interface/text) / **JetBrainsMono Nerd Font Mono** (monospace) — this is an OS-level font, *not* part of the vault, so it won't follow the clone. Install it separately on each new device (e.g. `brew install --cask font-jetbrains-mono-nerd-font`) or Obsidian silently falls back to its default font.

## Keeping this section in sync

If you add, remove, or reconfigure a plugin (or change theme/font/appearance) in either vault, update this section in the same sitting — it's the only place the full list lives outside `.obsidian/` itself, and it drifts silently otherwise.

## 3. Add the global Claude Code pointer

On the new device, edit (or create) `~/.claude/CLAUDE.md` and add:

```
Dave's second-brain system (Obsidian, domain-first structure) is split into three repos, always cloned as siblings: `dAIve-work` (client engagements, at <WORK_VAULT_PATH>), `dAIve-private` (personal life, at <PRIVATE_VAULT_PATH>), and `dAIve-shared` (Templates/CLAUDE.md/identity files symlinked into both, at <SHARED_VAULT_PATH>). If Dave asks to "log this to the vault" from a session elsewhere, open the matching repo as the project directory and write a session summary into its `AI/sessions/DD-MM-YYYY-<topic>.md` — Work for client work, Private for personal life, or dAIve-shared if the session was about the vault/tooling system itself, not a client or personal-life topic. Ask if it's not obvious which repo. Follow the format used in that repo's own `CLAUDE.md`.
```

Replace `<WORK_VAULT_PATH>` / `<PRIVATE_VAULT_PATH>` / `<SHARED_VAULT_PATH>` with the actual local paths from step 1 — they'll differ from the Mac's paths. Omit the `dAIve-private` clause entirely on a device that intentionally doesn't hold Private.

## 4. Install the vault stand-up skills

The two stand-up skills (`vault-standup-work`, `vault-standup-private`) live in a separate git repo, not in any of these three — they're shared tooling, not vault content. There's no scheduled task — both are invoked manually whenever Dave wants a review done.

1. Clone the skills repo, if not already on this device:
   ```
   git clone git@github.com:evadnl/AI.git
   ```
2. Run its setup script — it symlinks every skill (anything with a `SKILL.md`) into `~/.claude/skills/`:
   ```
   bash <path-to-AI-repo>/skills/setup.sh
   ```
3. Confirm they show up: `ls ~/.claude/skills/ | grep vault-standup` should list `vault-standup-work` and `vault-standup-private` (or just the one, on a Work-only or Private-only device).

That's it — no cron, no scheduled-task registration. Run `/vault-standup-work` or `/vault-standup-private` from a Claude Code session with the matching vault as the project directory whenever a review is wanted. See `README.md` for what each one does and when to run them.

## Known limitations (apply on every device, not just this one)

- Both skills only ever `git fetch` and compare local vs. origin — never pull, push, merge, or commit. If a device's clone drifts out of sync, that's on Dave to resolve manually (or let the Obsidian Git plugin's own auto-commit/auto-push cycle catch it up).
- Because these are manual, not scheduled, there's no multi-device race to guard against — run either skill from whichever device has the latest sync'd state.
- The skills repo (`AI`) is separate from these three repos — keep it up to date independently; a `git pull` in one won't touch the others.
- `dAIve-shared` has no Obsidian Git plugin of its own (it's not opened as a vault) — pull it manually on each device, or wire up a plain git-based sync if that becomes tedious.

## Updating this later

The source of truth for what each stand-up actually does is the `SKILL.md` file in the skills repo (`skills/vault/vault-standup-work/SKILL.md`, `skills/vault/vault-standup-private/SKILL.md`) — not this file. If those change, re-running `setup.sh` isn't even needed (they're symlinks to the repo, so edits apply immediately); this section only needs updating if the *install* steps themselves change (e.g. a repo moves, or a new skill needs installing).
