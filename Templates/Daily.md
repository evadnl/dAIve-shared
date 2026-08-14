---
created: {{date}}
tags: [daily]
---

# {{date}}

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
