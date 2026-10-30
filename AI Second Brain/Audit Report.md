# Obsidian Second Brain Audit

**Refreshed:** 2026-10-30  
**Vault root:** `Primary/`  
**Scope:** 40 Markdown files, one `.canvas` file, and 21 regular folders. This refresh supersedes the earlier snapshot; the earlier claims that the structure canvas was absent and no community plugins were enabled are no longer current.

I inspected the current note contents, indexes, templates, workflow notes, Canvas JSON, Excalidraw text/link metadata, filenames, and relevant Obsidian plugin identifiers/settings. I did not read the contents of the two protected `Databases/` files or the file in `.trash/`; the database files are both zero bytes. I did not inspect credentials or plugin data values. The original [[The Start/Start Here|Start Here]] page remains unchanged. This audit writes only this report.

## 1. Current structure overview

```text
Primary/
├── Current weakness.md
├── Rules and Structure.md
├── Sorting System.md
├── TO do list.md
├── The Structure Overview.canvas
├── AI Second Brain/
│   └── Audit Report.md
├── Business/AI Creator Business/
│   └── AI Creator Business Model.md
├── Databases/
│   ├── Coding database.md                 [0 bytes; content not read]
│   └── Timer app/Timer Database.md        [0 bytes; content not read]
├── Excalidraw/
│   ├── Drawing 2026-10-30 11.01.34.excalidraw.md
│   └── Start Here Notebook.excalidraw.md
├── Inbox/
│   └── Inbox.md
├── Knowledge/                              [empty]
├── LOGS/
│   ├── 25102026A.md
│   └── Logs.md
├── Memori/
│   ├── AI Stuff.md                         [empty]
│   ├── GitHub.md                           [empty]
│   ├── Memory.md
│   └── Q Notes/
│       ├── Coding quick notes.md           [empty]
│       ├── Other.md                        [empty]
│       ├── Temporary.md                     [empty]
│       └── quick notes.md
├── Planning/
│   ├── 2026-11-01 - My Weekly System.excalidraw.md
│   ├── Weekly Second Brain Review.md
│   └── to do list/
│       ├── To Do 181020261843.md
│       └── To do lists.md
├── Projects/                               [empty]
├── Resources/
│   ├── Resources.md
│   └── Youtube/
│       └── important tutorials.md
├── Reuse block/
│   ├── Obsidian Notes Template.md
│   └── Templates/
│       ├── Concept learned template.md
│       ├── Error log template.md
│       ├── GitHub repository Template.md
│       ├── Resource template.md
│       ├── Study Logs.md
│       ├── The Project Template.md
│       ├── Troubleshooting guide by me.md
│       └── Weekly Study time records Template.md
├── The Start/
│   └── Start Here.md
└── workflows/
    ├── Daily Task Completion.md
    ├── Daily Workflow.md
    ├── Kaizen%20Day%20Workflow.md
    ├── Weekly Completions and Documentation.md
    └── to do list/                          [empty]
```

Operational areas are outside the regular note tree: `.obsidian/`, `.stfolder/`, and `.trash/`. `.trash/` contains a file named `Weekly Study time records.md`; its contents were not inspected. `.stfolder/` contains a Syncthing marker. The vault has the Excalidraw and Git community plugins enabled; core Canvas, Templates, Properties, Bases, and Sync are enabled. `alwaysUpdateLinks` is true. No Notion community plugin or vault-root `AGENTS.md` was found in the inspected inventory. The vault root is not a Git working tree, so the installed Git plugin should not be treated as proof of a working backup.

## 2. Organizational principles inferred from the notes

- Notes are meant to have one primary home, with links between projects, reusable concepts, and sources rather than duplicated copies.
- `Inbox/Inbox.md` is a raw temporary capture point; `Memori/Q Notes/` is intended for brief, topic-known captures; `Temporary.md` is described in the rules as a review queue.
- `Knowledge/` is intended for reusable concepts, `Projects/` for multi-step work, `Resources/` for external sources, `LOGS/` for dated events, `Planning/` for schedules/review/tasks, and `workflows/` for repeatable execution/completion routines.
- `Databases/` is explicitly protected. Existing names and paths should be preserved unless a specific task authorizes a change.
- Frontmatter is optional. The rules favor small useful fields, ISO dates, and lowercase tags rather than a mandatory vault-wide schema.
- The Markdown Start Here page is a protected original; the Excalidraw notebook is a separate visual entry point.

## 3. Strengths worth preserving

- [[Rules and Structure]] and [[Sorting System]] set clear safeguards against deletion, bulk moves, accidental database edits, duplicate notes, and unsupported claims.
- The vault distinguishes durable learning, projects, resources, logs, tasks, and procedures. The business model has a dedicated home and clearly labels its prices and targets as hypotheses rather than validated outcomes.
- [[Planning/Weekly Second Brain Review]] gives a concrete review routine and explicitly says not to claim external Notion work was done without access. The Kaizen workflow defines a monthly rotation and a compulsory improvement block; the weekly timetable contains dated weekday topics and the Friday Kaizen Day plan.
- [[Excalidraw/Start Here Notebook.excalidraw|Start Here Notebook]] provides a visual companion with links to current destinations while the original Start Here page remains intact.
- Existing mixed capitalization and folder names are explicitly to be preserved. That avoids unnecessary high-risk renaming.

## 4. Confirmed issues and evidence

1. **The Inbox path in the rules does not match the vault.** The actual file is `Inbox/Inbox.md`, but [[Rules and Structure]] and [[Sorting System]] repeatedly direct agents to a root-level `Inbox.md`. No root-level `Inbox.md` exists. This can cause new captures to be created in the wrong location.

2. **Two current note links do not match existing targets.** `Planning/Weekly Second Brain Review.md` links to `Planning/2026-11-01 - My Weekly System`, while the actual file is `Planning/2026-11-01 - My Weekly System.excalidraw.md`. The tutorial embed in `Resources/Youtube/important tutorials.md` targets `How to use claude code and combine different AI models to one`, but no matching note exists in the vault inventory. The Structure Overview canvas has a file card for that same absent tutorial target. The weekly-timetable mismatch should be verified in Obsidian because Excalidraw uses a specialized `.excalidraw.md` note format.

3. **The current folder map is incomplete relative to the actual vault and its own rules.** [[The Structure Overview.canvas]] parses and has 33 file cards, but one card points to the missing tutorial above. Its folder frames do not show the current `Business/`, `Excalidraw/`, `Inbox/`, `Knowledge/`, or `Projects/` folders, and the map omits `workflows/Kaizen%20Day%20Workflow.md`. [[Rules and Structure]] says the canvas reflects the current folders, so that statement is stronger than the present map supports. The canvas may be intended as a selected-note map rather than a full inventory; its scope needs to be clear.

4. **The workflow guide and map omit a current workflow.** The actual `workflows/` folder has four Markdown notes, including [[workflows/Kaizen%20Day%20Workflow]], while the folder description in [[Rules and Structure]], [[Sorting System]], and the canvas accounts for only three. The Kaizen workflow has no inbound or outbound wikilinks. Its filename contains literal `%20` sequences; this is an observed filename, while whether that spelling was intended is unknown. The file was not renamed.

5. **Task tracking is split between two active locations.** Root-level [[TO do list]] contains several actions, while `Planning/to do list/` has its own index and dated task note. The lists do not contain an exact duplicate task in the inspected samples, but there are two places to check for next actions.

6. **Several navigation lists have unfinished numbered entries.** `The Start/Start Here.md` ends with `7)`, `Memori/Memory.md` with `3)`, `Resources/Resources.md` with `2)`, and `Reuse block/Obsidian Notes Template.md` with `9)`. These may be placeholders, but they read as incomplete indexes. The original Start Here page is unchanged and should stay protected unless the user changes that instruction.

7. **Four templates have unclosed code fences.** Odd fence counts occur in `Reuse block/Templates/Concept learned template.md`, `Error log template.md`, `Study Logs.md`, and `The Project Template.md`. This can make the remainder of each note render as code when copied or previewed.

8. **The Study Logs file is not a clean fill-in template.** `Reuse block/Templates/Study Logs.md` includes explanatory prose and points to `05 - Development Logs/Study Logs/`, a path absent from the current vault and inconsistent with `LOGS/`.

9. **Some templates contain sample defaults that could be mistaken for real data.** `Weekly Study time records Template.md` includes a dated period, study totals, highlights, and next-week tasks. `Error log template.md` is prefilled with a resolved example and date. The same weekly-summary filename also exists in `.trash/`; its content and relationship to the active file were not checked.

10. **The vault has seven zero-byte Markdown files.** Two are in protected `Databases/`; five are the linked Memori/quick-note stubs `AI Stuff.md`, `GitHub.md`, `Coding quick notes.md`, `Other.md`, and `Temporary.md`. Emptiness is confirmed, but intent is not; the stubs should not be filled or removed automatically.

## 5. Potential issues that require a decision

- The capture notes describe overlapping ideas: the Inbox says to paste temporary material, while the quick-notes index says to capture first and judge importance later. The rules distinguish raw Inbox capture from topic-known quick notes, but the intended boundary should be confirmed.
- `workflows/Weekly Completions and Documentation.md` and the Planning review both discuss weekly review and next-week preparation, though one focuses on coding/project completion and the other on vault maintenance. Their separate scopes are plausible; a short distinction in the navigation guide could prevent duplication.
- `Current weakness.md` is a personal reflection at the vault root, outside the `Memori/` home described by the rules. Keeping it at the root may be intentional.
- `Knowledge/`, `Projects/`, and `workflows/to do list/` are empty. They may be planned homes or a leftover folder; an empty folder is not by itself a problem.
- `Reuse block/Templates/Weekly Study time records Template.md` may be an example, a reusable template, or a real record. The active note and the same-named trash item need a user decision before either is blanked, restored, or removed.
- The `Excalidraw/Drawing 2026-10-30 11.01.34.excalidraw.md` drawing is not linked from the inspected Markdown indexes. It may be an intentional scratch drawing. I checked its file wrapper, not its rendered visual content.
- The core Templates plugin is enabled, but the inspected `app.json` had no template-folder preference. Confirm whether `Reuse block/Templates/` is configured for the core plugin or used manually.
- Workflow notes refer to GitHub and Notion. Git is enabled as a community plugin, but the vault root is not a Git repository; no Notion plugin is enabled in the vault. External applications or scripts may still exist outside this vault.

## 6. Recommended target architecture and current-to-target mapping

Keep the existing layout as the baseline; no broad restructure or new top-level folder is needed. These are recommendations, not completed moves.

| Current item | Recommended home/role |
|---|---|
| `Inbox/Inbox.md` | Keep as the single raw-capture note. Align the written routing rules to this actual path. |
| Root `TO do list.md` and `Planning/to do list/` | Choose one canonical task system; if consolidating, move individual actions only after review and approval. |
| `Current weakness.md` | Keep at root or place with personal context in `Memori/` after the user decides. |
| `Memori/` and `Memori/Q Notes/` | Preserve for durable personal context and brief known-topic captures; decide what the empty stubs mean before filling or removing. |
| `Knowledge/` and `Projects/` | Keep as empty planned homes until real notes need them. Do not add subject folders preemptively. |
| `Business/AI Creator Business/` | Keep the business model and related business strategy here; do not duplicate in `Projects/`. |
| `Resources/` and `Resources/Youtube/` | Keep source notes here; restore the missing tutorial target or decide whether its embed/card should be removed. |
| `Planning/` | Keep the dated timetable, Second Brain review, and task list here. |
| `workflows/` | Keep the daily learning, daily completion, Kaizen Day, and weekly coding completion routines here for now, preserving the recent instruction to leave the new workflow/completion files in place. |
| `LOGS/` | Keep dated records and event histories here. Preserve existing legacy filenames. |
| `Reuse block/Templates/` | Keep optional templates; distinguish blank forms from examples and correct stale paths/fences only after confirming intended sample data. |
| `Excalidraw/` and `The Structure Overview.canvas` | Keep visual navigation and drawings; update the canvas only after confirming whether it should show every folder or selected destinations. |
| `Databases/` | Protected. Do not inspect or move contents without task-specific authorization. |

## 7. Recommended naming and frontmatter standards

- Preserve current folder names and existing filenames. For new ordinary notes, use descriptive words and spaces consistent with nearby notes; avoid writing URL-encoded `%20` into a filename. Rename the existing Kaizen file only after confirming intent and checking all Obsidian/Excalidraw links.
- Use `YYYY-MM-DD - Short topic.md` for new dated logs. Retain older names such as `25102026A.md` and `To Do 181020261843.md` unless individually approved for change.
- Use exact vault-relative targets for ambiguous internal links, such as [[Planning/Weekly Second Brain Review|weekly review]]. Check embedded links and Canvas file paths as well as ordinary wikilinks. For Excalidraw files, include the actual `.excalidraw` stem and verify the link opens in Obsidian.
- Keep YAML optional. When a field serves retrieval or a workflow, prefer small fields such as `type`, `status`, `created`, and lowercase `tags`; use ISO dates. Do not require metadata on every note or bulk-normalize existing frontmatter.
- Mark examples clearly and keep reusable forms blank. Do not carry sample dates, completion statuses, study hours, or project results into a new record accidentally. Do not use `updated` unless a process maintains it.

## 8. Prioritized implementation roadmap

### Phase 1 — Resolve destinations and intent

Confirm the Inbox path, canonical task list, the role of `Current weakness.md`, the literal `%20` filename, missing tutorial, and the active/trash study-summary relationship. Keep the original Start Here page and protected database files untouched.

### Phase 2 — Repair navigation and routing after approval

Align `Rules and Structure.md` and `Sorting System.md` to `Inbox/Inbox.md`; include the Kaizen workflow; correct the weekly-timetable link; resolve the missing tutorial embed and Canvas card; refresh the structure map with current folders and its declared scope. Preserve existing paths unless a specific move is approved.

### Phase 3 — Make templates safe to reuse

Close the four unclosed code fences, replace the stale `05 - Development Logs/Study Logs/` example path, and separate blank templates from sample records after confirming which populated values are real examples or retained data. Verify the core Templates folder setting before relying on plugin commands.

### Phase 4 — Triage individual notes

Review the root task list, personal reflection, empty quick-note stubs, and empty folders one at a time. Link or move only after choosing a destination; do not bulk-delete, archive, or rename.

### Phase 5 — Revalidate

Check wikilinks, embeds, Excalidraw link maps, Canvas nodes, and the weekly review/timetable together after approved changes. Confirm sync and backup state before any path migration.

## 9. Risks involving links, templates, plugins, databases, and workflows

- The current file-path scan found two unresolved note links and one missing Canvas file target. Filesystem moves can break wikilinks, embeds, Excalidraw URI links, and Canvas node paths even when `alwaysUpdateLinks` is enabled; verify changes in Obsidian.
- Obsidian Git is enabled, but no `.git` repository was detected at the vault root. Obsidian Sync is enabled and a Syncthing marker exists. Confirm the actual backup/sync arrangement and whether any external automation is active before bulk moves.
- The Excalidraw plugin is enabled and the visual notebook contains `obsidian://open` links. Preserve exact target paths and test them in the plugin after any approved rename.
- `Databases/` has two zero-byte Markdown files. No schema or application data was inspected; filenames alone do not establish whether an external app relies on them.
- `.trash/Weekly Study time records.md` is retained by Obsidian and was not restored or deleted. Do not treat `.trash/` as an archive or as safe to purge.
- No secret values were copied into this report. Plugin script and data files were not read.

## 10. Questions before destructive or large-scale reorganization

1. Should `Inbox/Inbox.md` be the canonical Inbox path, with the rules updated to match, or is a root-level `Inbox.md` intended?
2. Which task list should be canonical: root `TO do list.md` or `Planning/to do list/`?
3. Should `Current weakness.md` remain at the root or live with personal reference in `Memori/`?
4. Is the literal filename `Kaizen%20Day%20Workflow.md` intentional? It remains untouched until naming and link behavior are confirmed.
5. Should the missing YouTube note be restored, or should the embed in `Resources/Youtube/important tutorials.md` and corresponding Canvas card be removed after review?
6. Is the populated weekly study summary a sample template or an actual record, and what should happen to the same-named file in `.trash/`?
7. Are the five empty Memori/quick-note files intentional placeholders? What should Inbox, Q Notes, and Temporary each hold?
8. Are the two empty database files placeholders, or are their paths used by an external application? Their contents remain protected and unread.
9. Should the structure canvas show every current folder or only selected navigation destinations?
10. Before any large move, are Obsidian Sync, Syncthing, Git, or external scripts actively syncing or relying on these paths?

---

**Audit boundary:** This report is an assessment and proposed plan only. No note content, links, frontmatter, folders, database files, plugins, Obsidian settings, trash contents, or original Start Here page were changed during this audit. The only write is this report.
