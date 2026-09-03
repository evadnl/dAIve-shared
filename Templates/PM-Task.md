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
- `projectId`: copy the `id` value from the target project note's own frontmatter (e.g. `Kuppersio.md`).
- `id`: a random 16-character lowercase alphanumeric string, unique across every task in the vault (e.g. `jp57wsxr5csmkaag`).
- `parentId`: only set if this is a subtask of another task — copy that task's `id`. Leave blank otherwise.
- `status`: one of `todo`, `in-progress`, `blocked`, `review`, `done`, `cancelled`.
- `priority`: one of `critical`, `high`, `medium`, `low`.
- `Project:` link at the bottom — point it at the project note itself, matching `projectId`.

The project note's own `taskIds` frontmatter array and `## Tasks` checklist also need this task's `id`/title added — the plugin regenerates both from its task files on its own schedule, but adding them by hand keeps the board in sync immediately.
%%
