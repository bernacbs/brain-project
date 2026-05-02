# Brain

A personal knowledge operating system built on top of [Obsidian](https://obsidian.md/), designed to work alongside AI agents.

The system captures everything — notes, projects, ideas, references, media — processes it into structured knowledge, and connects it into a living wiki that grows over time.

---

## Getting started

The file [`project_brain.md`](./D01%20Skills/project_brain.md) is the core of this project. It contains the full structure, philosophy, and the `/init_brain` command — send it to any AI to automatically create the entire vault folder structure from scratch.

---

## Skills

Reusable AI instructions live in the `D01 Skills/` folder. Each skill defines a command that any AI can recognize and execute, either as an automatic skill (in tools like Claude Code or Cowork) or as a pasteable prompt in any chat.

| File | Command | Description |
|---|---|---|
| `project_brain.md` | `/init_brain`, `/brain_status` | Creates and audits the vault structure |
| `project_snapshot.md` | `/project_snapshot` | Exports a structured project note to `B01 Projects/` |

---

## Structure overview
