---
created: 14-08-2026
project: "[[]]"
tags: [ai-session]
---

# Session Summary - 14-08-2026

## What we did
- Added a Language section to `CLAUDE.md`. It sets ASD-STE100 (Simplified Technical English) as the writing style for vault content: short sentences, active voice, plain consistent vocabulary, present tense by default, no idioms or noun stacks.
- Checked `CLAUDE.md`'s Vault structure section against the actual folder tree, at Dave's request. Dave believed it still described the old PARA method. The PARA line itself was already correct ("moved away from PARA"), but the structure underneath it had drifted.
- Found two Private domains that existed on disk but were undocumented: `02. Home Assistant/` and `03. Home/`.
- Found the Career domain had moved from `02. Career/` to `06. Career & Learning/`, and gained a `01. Learning/` subfolder plus its own domain index note (`Career & Learning.md`).
- Found a new `05. DNS.md` file under Homelab that the file list did not mention.
- Confirmed the open questions with Dave, then updated `CLAUDE.md` to match.

## Decisions
- `03. Home/` domain: general household/physical projects — anything physical around the house that isn't Homelab infra or a Home Assistant automation.
- Documented the domain-index-note pattern (a note named after the domain, e.g. `Career & Learning.md`) as a general, optional pattern any domain can adopt — not unique to Career.
- `05. DNS.md` gets the same treatment as `04. IPAM.md`: a single-file reference note, listed alongside it in Homelab's bullet.

## Next steps
- None outstanding. `CLAUDE.md` now matches the vault's current structure.
