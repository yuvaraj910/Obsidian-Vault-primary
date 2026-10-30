---
type: workflow
tags:
  - obsidian
  - inbox
  - organization
---

# Sorting System

Use this guide to choose one primary home for a new note. For vault-wide safety, writing, and metadata rules, see [[Rules and Structure]]. Search for an existing note before creating another. Do not move or delete existing notes as part of sorting unless the task explicitly authorizes it.

## Current Destinations

| Information | Destination |
|---|---|
| Unclassified capture | Root Inbox.md. There is no Memori/Q Notes/Inbox path. |
| Short note with a known topic | Existing topical note in Memori/Q Notes/; use Temporary.md only for intentionally temporary material that will be reviewed. |
| Durable concept or reusable technical explanation | Knowledge/ (created for this system; no subject subfolders yet). |
| Active or completed software, hardware, homelab, or learning project | Projects/<Project Name>/ (create the project folder when a real project needs a home; no project subfolders currently exist). |
| AI creator business strategy | Existing Business/AI Creator Business/. Do not copy it into Projects/. |
| Personal memory, career plan, or private long-term plan | Memori/; keep Memori/Memory.md as its overview. |
| External source or annotated reference | Resources/; YouTube notes belong in existing Resources/Youtube/. |
| Daily learning or coding execution workflow | Existing workflows/ notes; keep the current daily workflow here. |
| Daily task-completion record or weekly coding-completion procedure | Existing workflows/ notes; keep the current completion files here. |
| Personal weekly schedule, Second Brain review, and vault-maintenance procedure | Planning/. |
| Tasks and next actions | Existing Planning/to do list/. |
| Dated record of something that happened | LOGS/. Keep project-specific engineering records inside that project's folder when they are part of its history. |
| Reusable note structure | Existing Reuse block/Templates/, only when a template helps. |
| Vault audits and AI second-brain architecture | Existing AI Second Brain/. |
| Application database file, schema, view, or record | Protected Databases/; do not touch without explicit permission for that specific task. |

Knowledge/ and Projects/ were created without moving any existing notes. Create Knowledge/<Subject>/ or Projects/<Project Name>/ only when real notes need grouping. No Archive/ folder exists; do not create one or move material there automatically. Do not create separate top-level folders for Programming, DSA, AI, Career, Ideas, or Logs unless later volume and an approved task justify them.

## A. Programming and Technical Learning

### Quick captures

- If the topic is clear and the note is a short reminder, use the matching existing note under Memori/Q Notes/ (for example, Coding quick notes.md).
- If it is unclassified, use root Inbox.md.
- Promote a quick capture to Knowledge/ when it becomes a reusable explanation or study note. Search first; preserve useful context and do not delete the capture without approval.

### Durable concepts and structured study notes

Use Knowledge/ for reusable explanations across Python fundamentals and advanced Python, libraries and modules, DSA, Java and OOP, C++, SQL, web development, machine learning and AI, game development, operating systems, computer science, and exam preparation.

- Keep one note per coherent concept, not one note per tiny fact.
- Update an existing note when it already explains the same concept; add a related section or example rather than creating a near-duplicate.
- Use the existing Concept learned template only when its structure is useful. Templates are optional and some contain unfinished code fences; inspect before copying.
- Keep a small practical example beside the concept it teaches. Give a larger exercise set its own note only when it is reusable or substantial.
- Put course handouts or external study sources in Resources/; keep your own explanation in Knowledge/ and link the two.

### Exercises, study sessions, errors, and projects

- A completed study session or dated progress record belongs in LOGS/; use an ISO date for new dated logs, such as 2026-10-25 - Python Study.md or 2026-10-25.md.
- A one-off error and its fix belongs in LOGS/ if it is useful to revisit. Use the existing error-log template only after checking its example content and code fence.
- A reusable coding or learning procedure belongs in workflows/. Personal planning and Second Brain maintenance procedures belong in Planning/. A durable explanation of the underlying technical behavior belongs in Knowledge/; link to the error record if useful.
- An exercise that is part of a real project belongs with that project. A multi-step learning project goes in Projects/<Project Name>/; keep general concepts in Knowledge/ and link rather than copy them.

## B. Software Projects and Engineering

Use Projects/<Project Name>/ for a real project that needs its own plan, requirements, architecture, implementation notes, technical decisions, project-specific bugs, and progress history. The Projects/ root exists; create one subfolder when the project is real, not for an unreviewed idea. The existing Project Template may help for a substantial project, but do not fill every field if a short project note is enough.

- Keep requirements, architecture, implementation choices, and project-specific database schemas with that project.
- Keep project-specific bug reports and debugging steps with the project. Use a dated project log when the sequence of events matters.
- Put general concepts in Knowledge/ and link to them from the project; do not duplicate the explanation in each project.
- Put a public repository worth revisiting in Resources/ as a short source note. Link it from the project if relevant; do not copy the repository README into the vault.
- Hardware experiments, DIY builds, homelab, and self-hosting setups use the same project rule. Keep experiment results with the project; promote only broadly reusable learning to Knowledge/.
- Leave completed projects where they are and mark their state if helpful. Do not automatically archive or move them.
- The current AI creator business model already lives at Business/AI Creator Business/AI Creator Business Model.md. Keep that business-specific strategy there instead of starting a duplicate in Projects/.

## C. AI Systems and Automation

Choose the destination by the role of the information:

- **AI tools, models, agents, and technical behavior:** durable explanations in Knowledge/; source notes and product references in Resources/; brief, known-topic captures can stay in the existing AI Stuff note.
- **Reusable Codex or other agent prompt:** keep a repeatable coding or learning procedure in workflows/; keep a personal planning or vault-maintenance procedure in Planning/. Include its purpose, inputs, constraints, and expected output. Keep project-specific prompts in that project's folder. Do not save every one-off prompt.
- **Agent instruction files:** AGENTS.md belongs inside the relevant code repository: at its root for repository-wide instructions, or within a narrower repository subfolder for local scope. Do not create AGENTS.md in the vault root or anywhere else in the vault without explicit authorization.
- **AI learning workflow:** workflows/ for repeatable learning steps; Knowledge/ for the reusable explanation of a tool or concept; link the notes when both are useful.
- **Automation workflow:** keep a personal or vault-maintenance procedure in Planning/ and project-specific implementation notes in the associated project documentation. Never put secrets in ordinary Markdown.
- **Experiment or AI product research:** record a dated experiment in LOGS/ or inside its project; keep source annotations in Resources/; put durable conclusions in Knowledge/. Do not state a result as general fact until evidence supports it.
- **Vault architecture:** use existing AI Second Brain/ for architecture or audit notes, and root Rules and Structure.md for the authoritative vault-wide rules.

Do not treat tool announcements, marketing, prompts, or model outputs as verified results. Record what was tested, under what conditions, and what remains uncertain.

## D. Resources and Research

Use Resources/ for external material: YouTube tutorials, official documentation, articles, websites, courses, GitHub repositories, and other references. Use existing Resources/Youtube/ for YouTube notes.

For each resource note, retain the original title and URL, why it is useful, relevant sections or timestamps, and your own conclusions or next step. The existing Resource template can be used when it helps, but a short link note may be enough. Do not copy whole articles, course lessons, or repository documentation into the vault.

A research synthesis is your own explanation, not a second copy of the sources. Put durable reusable conclusions in Knowledge/ and link to the source notes. Create a resource-type subfolder only when a growing collection makes it easier to browse; Resources/GitHub/ and Resources/Courses/ are not currently present.

## E. Procedures, Tasks, and Productivity

- **Task:** an action to complete. Use Planning/to do list/; do not hide an actionable checkbox inside a reference note when it should be tracked.
- **Workflow:** repeatable steps for coding or learning, such as the existing [[workflows/Daily Workflow]]; keep execution procedures in workflows/. Use Planning/ for personal weekly schedules, Second Brain reviews, and vault-maintenance procedures.
- **Completion record:** use [[workflows/Daily Task Completion]] to record a daily session and [[workflows/Weekly Completions and Documentation]] for weekly coding review, documentation, and completion.
- **Project:** an outcome requiring multiple related actions and project-specific records. Use Projects/<Project Name>/ once the work is real.
- **Reference note:** information to consult later, not a task or process. Use Knowledge/, Resources/, or Memori/ according to its purpose.

The existing workflows/ notes cover coding and learning execution and completion. Planning/ holds the weekly timetable, Second Brain review checklist, vault-maintenance procedures, and task lists. Keep the two weekly reviews distinct: the Planning checklist reviews the Second Brain; the workflows checklist reviews coding work and project documentation. Keep tasks in the existing task system, and link a task to its project where useful. The sorting guide itself is a procedure and remains at the existing root path Sorting System.md.

## F. Personal Planning and Decisions

Use Memori/ for durable personal context, career plans, job searching, skill roadmaps, long-term goals, and personal decisions. Keep Memory as the existing overview; create a separate, descriptively named note only when the plan is substantial enough to stand on its own. Put concrete next actions in Planning/to do list/ and link to the plan.

Use discretion with financial plans, budgets, job-search records, and other private material. Keep sensitive details to the minimum needed, do not create duplicate copies, and do not store passwords, API keys, financial credentials, recovery codes, or private keys in ordinary notes. A personal routine's reusable steps belong in Planning/; the personal goal or decision behind it belongs in Memori/.

For a decision note, distinguish known facts, assumptions, options, the decision, and a review trigger when one is useful. Do not create a new personal-data folder or copy records from a secure source just to make them searchable.

## G. Databases and Logs

### Protected database area

Databases/ is protected. Do not create, edit, rename, move, reorganize, or delete anything in it—including application data, schemas, views, or records—unless the user explicitly authorizes that specific task. Do not use scripts or bulk tools that may alter it. This guide does not inspect or change database contents.

Keep these information types distinct:

- **Application database and its records:** stay in the protected database/application. Never convert records into Markdown for consistency.
- **Human-written explanation of a specific system:** keep with its project in Projects/ if project-specific.
- **Reusable database concept** (SQL, normalization, SQLite, JSON/CSV handling): Knowledge/.
- **Database troubleshooting:** project folder if system-specific; otherwise LOGS/ for the event and workflows/ for a reusable coding procedure.

### Logs

Use existing LOGS/ for what happened and when: study sessions, coding sessions, standalone error records, investigations, build results, and weekly reviews. Prefer meaningful titles and ISO dates for new dated logs. Keep project-only history with the project when it would not be useful apart from that project. Logs record events; a concept note explains reusable knowledge; a workflow explains repeatable steps.

## H. Temporary Notes and Miscellaneous Information

- **Unsorted or unclear:** root Inbox.md.
- **Quick note with a known area:** the matching existing note in Memori/Q Notes/.
- **Intentionally temporary:** Temporary; review its contents and decide whether to promote, merge, keep, or propose archiving.
- **Idea that may become a project:** capture it in Inbox.md. Create a project folder only after deciding to pursue it.
- **Unclassified source:** capture the URL and enough context in Inbox.md; after review, create or update a resource note in Resources/.
- **Already covered elsewhere:** update the existing note or link to it instead of duplicating.
- **No longer relevant:** mark it for review. Do not automatically delete, archive, or move it. There is no curated Archive/ folder yet; propose one only if there is a real need and obtain approval before moving existing notes.

## Practical Decision Tree

Before saving, search the vault for the same concept, source, project, or procedure. Then choose the first applicable primary home below; a note can link to a second home without duplicating its content.

1. **Is this a task or concrete action?** Put it in the existing Planning/to do list/ task system. If it belongs to a project, add a link to that project.
2. **Is it associated with an active project?** Keep project-specific plans, bugs, decisions, and implementation details in Projects/<Project Name>/ (or in the existing Business/AI Creator Business/ for that business). Do not copy them into general notes.
3. **Is it a learning concept?** Update the existing concept note or create a concise note in Knowledge/.
4. **Is it an external source?** Create or update a note in Resources/, using Resources/Youtube/ for YouTube sources. Preserve the URL and your reason for saving it.
5. **Is it a coding or learning execution procedure?** Use workflows/. For a personal schedule, Second Brain review, or vault-maintenance procedure, use Planning/. Put the task itself in the task list, not in the workflow.
6. **Is it an AI instruction or reusable prompt?** Keep project-specific instructions in the project; save a cross-project repeatable prompt in Planning/ or a short AI quick note in AI Stuff. Place AGENTS.md only inside a code repository and only when authorized; never create it in this vault.
7. **Is it a database file, schema, view, or record?** It belongs to the protected Databases/ system. Do not touch it without task-specific permission. Put only human-written explanations or general concepts in Markdown outside that folder.
8. **Is it a quick, unclassified capture?** Put it in root Inbox.md. If its topic is known and the note is brief, an existing Memori/Q Notes/ note may be more suitable.
9. **Is it already documented?** Update the existing note if the task authorizes editing; otherwise link to it or leave the proposed change for review. Do not create a duplicate.

For mixed items, keep the project-specific or task-specific material in its primary home and link to one general concept or source note. Split one capture only when it contains distinct items that will be useful independently. If none of the routes is clear, leave it in Inbox.md and state what is uncertain.

## Examples

| Example | Destination | Reason |
|---|---|---|
| Python decorator explanation | Knowledge/Python Decorators.md (new note, if no existing note covers it) | Durable Python concept with a concise explanation and working example. |
| DSA merge sort implementation | Knowledge/Merge Sort.md (new note, if needed) | Keep algorithm, complexity, edge cases, and reusable implementation together. Put a project-specific implementation in that project and link to this concept. |
| Java multithreading exam note | Knowledge/Java Multithreading Exam Notes.md (new note, if needed) | Structured study material; dated study-session records go in LOGS/. |
| GitHub repository worth revisiting | Resources/<Repository Name>.md (new resource note) | Save the repository URL, why it is useful, files to inspect, and learning questions. No GitHub-specific resource subfolder exists yet. |
| Bug encountered in a project | Projects/<Project Name>/Bug - <Short Title>.md (create the project folder when needed) | The reproduction, fix, and project context belong with the project. Link a broadly useful fix to Knowledge/. |
| Reusable prompt for Codex to organize Markdown files | Planning/Codex Markdown Sorting Prompt.md (new note, if it will be reused) | It is a repeatable procedure; include scope, file protections, inputs, and expected output. A one-off prompt stays with its task. |
| Workflow for learning a Python library | workflows/Learning a Python Library.md (new note, if needed) | It documents repeatable learning steps. Library concepts go in Knowledge/; official docs and tutorials go in Resources/. |
| YouTube tutorial | Resources/Youtube/<Descriptive Tutorial Name>.md (new note) | Resources/Youtube/ already exists; record the original URL and useful timestamps or lessons. |
| New DIY music player idea | Inbox.md first; if pursued, Projects/DIY Music Player/ (proposed project subfolder, not created) | Keep an unreviewed idea out of a project folder. Create the folder after deciding to pursue the build. |
| Job-search plan | Memori/Job Search Plan.md (new note, if substantial); tasks in Planning/to do list/ | The personal plan belongs with personal memory; dated applications or sessions can be logged only when useful. |
| Temporary idea with unclear category | Inbox.md | Capture it with enough context to decide later; do not invent a folder or delete it. |

All paths marked as new notes or proposed subfolders are examples, not claims that those files exist. The Knowledge/ and Projects/ root folders exist; the subject and project subfolders shown above do not.

## Review and Destructive Changes

Sort one item at a time. When merging, moving, archiving, or deleting would improve organization, first identify the exact source and destination and preserve any unique information. Propose the change and wait for explicit approval before carrying it out. Never automatically delete, archive, or bulk-move content. The Databases/ protection rule is stricter and requires explicit permission for the specific task.
