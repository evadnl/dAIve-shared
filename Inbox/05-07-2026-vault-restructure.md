---
created: 05-07-2026
tags: [daily]
---

# 05-07-2026

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
- Moved the vault off PARA onto a custom domain-first method, designed collaboratively with Dave, then implemented it in full: renumbered/moved every folder under `01. Private`/`02. Work`, deleted unused `Areas/Health.md`/`Areas/Finances.md`, moved Career out of Areas, rewrote `CLAUDE.md`, and updated `INSTALL.md`, the global `~/.claude/CLAUDE.md` pointer, and the live `vault-daily-review` scheduled task to match.
- Fixed a Folder Notes bug (folder-note filename must match its folder's name) and converted Homelab's IPAM from one big note into individual VLAN notes + a Base, mirroring the existing Hosts pattern.
- Investigated the Iconic plugin's Folder Rules vs. per-folder icons at Dave's request — found rules fully overrule matched items' icons, fixed by using per-folder color assignment instead.
- Split physical network devices out of Hosts into a new Infra folder, then renumbered Homelab's subfolders to Dave's final order (`02. Infra`, `03. Hosts`, `04. IPAM`).
- Dave confirmed the renumbered Bases render/click correctly and the Iconic icons are OK — no outstanding follow-up from this session.
- Full detail in [[05-07-2026-vault-restructure]].
- Migrated icon plugins: confirmed Iconic can't do custom icon packs, removed its config from `community-plugins.json`/`workspace.json` ahead of Dave uninstalling it, and helped set up Iconize in its place (including diagnosing that the sudden all-folders icon was the Catppuccin theme's own CSS, not Iconize). Set Iconize per-folder icon colors for Homelab, Resources (using official brand colors for Kubernetes/Terraform/AWS pulled from the Simple Icons pack), and Work. Also fixed a `hitrail` → `Hitrail` client-name casing inconsistency across the vault. Full detail in [[05-07-2026-icon-plugin-migration]].
- Found and fixed a gap left over from the Work/Private split: `02. Work` had no `99. Inbox/` folder (Private's had one), and two pre-split daily notes with real client content were stranded in root `/Inbox` instead of being migrated to Work like Private's were. Created the folder, moved the two files into `02. Work/01. Daily/`, confirmed no links broke, confirmed the `vault-daily-review` scheduled task already expected the folder to exist, and gave the new folder Private-Inbox's icon in Work's red. Full detail in [[05-07-2026-work-inbox-fix]].

## Decisions
- See [[05-07-2026-vault-restructure]] for the full set of decisions (domain-first method replacing PARA, numbering convention, per-domain + per-context Archive, Work Clients wrapper + Daily, Private To-do.md instead of dailies, Hosts/IPAM/Infra Base pattern, Iconic color-vs-icon precedence, final Homelab subfolder order).
- See [[05-07-2026-icon-plugin-migration]] for icon-plugin decisions (Iconic config removed but historical mentions kept, Catppuccin theme identified as the real cause of the all-folders icon issue, icon color scheme for Homelab/Resources/Work, and fixing "hitrail" casing everywhere including historical logs).
