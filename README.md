# Brain

![Version](https://img.shields.io/badge/version-2.2-blue)

A personal knowledge operating system built on top of [Obsidian](https://obsidian.md/), designed to work alongside AI agents.

The system captures everything — notes, projects, ideas, references, media — processes it into structured knowledge, and connects it into a living wiki that grows over time.

---

## For AI agents

If you are an AI reading this file, follow these steps before doing anything else:

1. **Ask the user for permission** to load the project: _"I found the Brain project README. Would you like me to load `project_brain.md` and the available skills?"_
2. **Only proceed if the user confirms.**
3. Read `project_brain.md` and internalize its structure, philosophy, and commands.
4. Read the `skills/` folder and list all available skill files with a one-line description of each.
5. **Ask the user which skills they want to load** for this session.
6. Load only the skills the user selected and confirm which commands are now active.

Do not execute any command or modify any file until the user explicitly requests it.

---

## Getting started

The file [`project_brain.md`](./project_brain.md) is the core of this project. It contains the full structure, philosophy, and the `/init_brain` command — send it to any AI to automatically create the entire vault folder structure from scratch.

---

## Skills

Reusable AI instructions live in the `skills/` folder. Each skill defines a command that any AI can recognize and execute, either as an automatic skill (in tools like Claude Code or Cowork) or as a pasteable prompt in any chat.

| File | Command | Description |
|---|---|---|
| `project_brain.md` | `/init_brain`, `/brain_status` | Creates and audits the vault structure |
| `skills/project_snapshot.md` | `/project_snapshot` | Exports a structured project note to `B01 Projects/` |

---

## Structure overview

```
Brain/
├── _Assets/            Raw files: PDFs, images, audio, video
├── _Templates/         Note templates
├── A00 Inbox/          Everything enters here
├── A01 Processing/     Triage and routing
├── A02 Anchor Topics/  Navigation hubs (MOCs)
├── A03 Daily Notes/    Daily log
├── B01 Projects/       Active project context notes
├── B02 Ongoing/        Continuous responsibilities
├── B03 Interests/      Topics followed without obligation
├── B04 Archive/        Closed loops and old notes
├── C01 Wiki/           Personal encyclopedia
├── D00 Claude/         AI agent workspace
└── D01 Skills/         Skill files
```

---

## Requirements

- [Obsidian](https://obsidian.md/) — for navigating and editing the vault
- Any AI with file access **or** any chat-based AI (paste the skill file as a prompt)
