---
created: 14-08-2026
tags: [daily]
---

# 14-08-2026

## Inbox check


## Open Items (#to-do / #needs-review)

```dataviewjs
const exclude = ["Templates/", "AI/sessions/", "CLAUDE.md"];
const keep = p => !exclude.some(pre => p.file.path.startsWith(pre)) && p.file.path !== dv.current().file.path;
// strip inline code spans first, since Dataview's tag scan otherwise counts
// backtick-quoted mentions (e.g. narrative "`#to-do`" in a Decisions log) as real tags
const realTags = text => (text.replace(/`[^`]*`/g, "").match(/#[\w-]+/g) || []);

for (const [tag, label] of [["to-do", "To-Do"], ["needs-review", "Needs Review"]]) {
  dv.header(3, label);
  let rows = [];
  for (const page of dv.pages().where(keep)) {
    for (const item of page.file.lists) {
      // a ticked box is done, regardless of whether the tag was removed
      if (!item.completed && realTags(item.text).includes("#" + tag)) {
        rows.push([item.text.replace(/#(to-do|needs-review)/g, "").trim(), dv.fileLink(page.file.path)]);
      }
    }
  }
  if (rows.length) {
    dv.table(["Item", "Source"], rows);
  } else {
    dv.paragraph("*none*");
  }
}
```

## Today
- Set the vault's language preference to ASD-STE100 (Simplified Technical English) — added to `CLAUDE.md`.
- Fixed `CLAUDE.md`'s Vault structure section, which had drifted from the actual folder tree: two undocumented domains (`02. Home Assistant/`, `03. Home/`), Career's move to `06. Career & Learning/` with a `01. Learning/` subfolder, and a missing `05. DNS.md` under Homelab.

## Agent Log
- Read `CLAUDE.md` and compared it against the live folder tree under `01. Private/` and `02. Work/`.
- Confirmed scope and naming for the undocumented domains with Dave before editing.
- Updated `CLAUDE.md`'s Vault structure section: added `02. Home Assistant/` and `03. Home/` bullets, renumbered and expanded the Career bullet to `06. Career & Learning/`, added `05. DNS.md` to Homelab's file list, and documented the optional domain-index-note pattern.
- Wrote this session summary at [[14-08-2026-claude-md-sync]] (AI/sessions).
