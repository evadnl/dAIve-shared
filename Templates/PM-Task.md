---
pm-task: true
projectId: ""
parentId:
id: ""
title: "{{title}}"
type: "task"
status: "todo"
priority: "medium"
start: "{{date:YYYY-MM-DD}}"
due: ""
progress: 0
assignees: []
tags: []
subtaskIds: []
dependencies: []
createdAt: "{{date:YYYY-MM-DDTHH:mm:ss.SSS}}"
updatedAt: "{{date:YYYY-MM-DDTHH:mm:ss.SSS}}"
---

Description

Project: [[]]

%%
Fill in by hand before using — the project-manager plugin has no scripting engine to generate these:
- `projectId`: copy the `id` value from the target project note's own frontmatter (e.g. `kuppers.io.md`).
- `id`: a random 16-character lowercase alphanumeric string, unique across every task in the vault (e.g. `jp57wsxr5csmkaag`).
- `parentId`: only set if this is a subtask of another task — copy that task's `id`. Leave blank otherwise.
- `status`: one of `todo`, `in-progress`, `blocked`, `review`, `done`, `cancelled`.
- `priority`: one of `critical`, `high`, `medium`, `low`.
- `title`: keep the value on one line. The plugin makes this card's filename from the title, so a newline in it breaks both the filename and the board link.
- `Project:` link at the bottom — point it at the project note itself, matching `projectId`.

Add this task's `id` to the project note's `taskIds` frontmatter array. That array is the board's record of which tasks belong to it.

Do not hand-edit the project note's `## Tasks` checklist, or write anything else into that note's body. The plugin generates the whole body from the task cards and overwrites what is there. The checklist follows on its own once `taskIds` holds the new `id`.
%%
