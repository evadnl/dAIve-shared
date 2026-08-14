---
created: 06-07-2026
tags: [daily]
---

# 06-07-2026

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


## Agent Log
- Audited Obsidian plugins/settings after the vault-restructure merge: found and removed a stale `metadata-menu` entry in `community-plugins.json` (plugin was fully removed 2026-07-03, list was never updated), staged the pending merge resolution (`workspace.json`) and removed a leftover `conflict-files-obsidian-git.md` artifact, then found and re-enabled `folder-notes` after it got disabled separately from Obsidian's own plugin-error handling. Documented the full plugin/core-plugin/appearance setup in `INSTALL.md` as the ongoing source of truth. Full detail in [[06-07-2026-obsidian-plugins-settings]].

## Decisions
- See [[06-07-2026-obsidian-plugins-settings]] for the full set of decisions (stale `metadata-menu` entry removed rather than reinstalled, `INSTALL.md` chosen as the documentation home for Obsidian setup, and a standing rule to update that documentation in the same sitting as any future plugin/settings change).
