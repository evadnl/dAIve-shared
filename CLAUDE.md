## About this repo
This is the shared config/resource repo for Dave's second-brain system, which is split into three repos: `dAIve-work` (client engagements), `dAIve-private` (personal life), and this one (`dAIve-shared`). This repo isn't opened as an Obsidian vault itself — `Templates`, `CLAUDE.md`, `IDENTITY.md`, `SOUL.md`, and `USER.md` are symlinked from here into the root of both `dAIve-work` and `dAIve-private`, so a change here applies to both automatically. `Inbox/` and `AI/sessions/` here hold capture and session logs for work on the vault system itself (vault-admin/tooling), not Work or Private content.

For a session about the vault system itself (this repo, either vault's structure, template changes, cross-vault tooling) rather than a specific client engagement or personal-life topic, run Claude Code against this `dAIve-shared` repo directly.

## Vault structure
Both `dAIve-work` and `dAIve-private` use a domain-first method (moved away from PARA — too much duplication between Projects and Resources for the same topic). A **domain** is anything with enough going on to deserve its own top-level folder — a client, a life area, Homelab. Each domain defines its own subfolders freely instead of forcing every topic into the same Projects/Resources buckets. A domain can also have its own index note named after the domain (e.g. `Career & Learning.md`) that summarises what it covers — this is optional, and not every domain has one yet.

Subfolders are numbered to control sort order explicitly, with gaps left on purpose so new domains can be inserted later without renumbering everything:
- Low numbers (`01.`, `02.`, ...): domains and other frequently-used folders, roughly in order of how often they're reached for.
- `25.`: Resources — always a high number so new domains claim the low numbers first.
- `98.`: Archive.
- `99.`: Inbox — always last.

See `VAULT-STRUCTURE.md` in each vault's own root for that vault's specific domain/folder layout.

## Projects
Each project (under a domain's `Projects/` folder) has a note named after the project, with frontmatter (created, client, tags: [project], status: active | paused | done, related), and Objective / Context / Tasks / Notes sections. Dated entries (meetings, updates) go under the Notes section as `### DD-MM-YYYY` subsections. When a project's status becomes `done`, move its whole folder to that domain's `98. Archive/`.

If a project's `## Tasks` list grows unwieldy, completed items and resolved `#to-do`/`#needs-review` flags move out to a sibling `<Project>-archive.md` in the same project folder (from the `Project-Archive` template), linked via `related`. This is separate from a whole finished project moving to `98. Archive/` — the project itself stays active, only its closed clutter moves out. See `VAULT-STRUCTURE.md` for whether this runs automatically in a given vault.

## Templates
Reusable note templates, in this repo's `Templates/` folder (symlinked into both vaults): Project, Project-Archive (the `<Project>-archive.md` sibling a project's note spills its closed Tasks/resolved flags into once the live list gets unwieldy), Client-Meeting, Debug-Note, Daily, Session-Summary, Person, IPAM-Cloud (AWS accounts/VPCs/CIDRs), IPAM-Network (VLANs/subnets, single-note starting point for a new registry), Infra (individual physical-hardware/VM/LXC notes, e.g. Homelab's `02. Infra`), Service (individual deployed-service notes with URL/port + a link back to the Infra note it runs on, e.g. Homelab's `03. Services`), VLAN (individual VLAN notes — the pattern a registry graduates to if it outgrows the single-note IPAM-Network format: individual entity notes + a matching Folder Notes `.base` for the clickable table, same as Infra/`02. Infra.base` or Service/`03. Services.base`; Homelab's `04. IPAM` tried this and folded back to single-note since the VLAN list rarely changes).

## Language
Write all vault content in ASD-STE100 style (Simplified Technical English, the aerospace controlled-language standard), adapted for note-taking:
- One idea per sentence. Aim for 20 words or fewer per sentence.
- Active voice: "Configure the router," not "The router is configured."
- Plain, precise words over technical or fancy ones. Use the same word for the same thing every time — don't swap in synonyms for variety.
- Present tense by default. Use past tense only for things that already happened (e.g. session logs, dated Notes entries).
- No idioms, slang, or jargon used for flavor. A technical term is fine when it's the actual name of the thing.
- Avoid noun stacks (e.g. "network configuration file backup process" → "the process to back up the network configuration file").
- Keep articles (a, the) — don't drop them to save words.
- Use a list instead of one long sentence when a step has multiple parts.

Applies to notes, session summaries, daily logs, and any other content written into the vault. Does not apply to quoted external content (error messages, other people's text) or code.

## Tags
- #needs-review, #to-do: flag items needing follow-up.
- #client/<name>, #topic/<tech>: cross-linking by client or technology.

## Session protocol
Start each session by:

1. Reading this vault's capture: `01. Daily/DD-MM-YYYY-<topic>.md` in the Work vault, or `00. To-do.md` in the Private vault (Private has no daily note). In `dAIve-shared`, read `Inbox/DD-MM-YYYY-<topic>.md` if a matching note exists for today.
2. Scanning `99. Inbox/` (or, in `dAIve-shared`, `Inbox/`) for unprocessed notes.
3. Check for any notes tagged #needs-review or #to-do.

End each session by:
1. If the session touched a project, write it up in the project's own `### DD-MM-YYYY` Notes entry, with a `**Decisions:**` block for any decisions made. This project entry is the single canonical record — don't duplicate the narrative elsewhere.
2. Write a short session summary to `AI/sessions/DD-MM-YYYY-<topic>.md`: what was worked on and which project(s) it touched, linking to the project entries from step 1 instead of restating them. For a session with no project (vault-admin/tooling, run from `dAIve-shared`), this is the full record instead.
3. In the Work vault only: add one line per touched project to today's `01. Daily/DD-MM-YYYY-<topic>.md`, linking to that project's entry (e.g. `- [[Pyriet-MSG#27-06-2026]] — Keycloak↔Entra group mapping design`) instead of a full narrative. In the Private vault: update `00. To-do.md` if the session changed any open items.
