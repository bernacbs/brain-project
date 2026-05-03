# Brain

![Version](https://img.shields.io/badge/version-2.1.0-blue)

A personal knowledge operating system built on top of [Obsidian](https://obsidian.md/), designed to work alongside AI agents — from cloud LLMs to local models.

The system captures everything — notes, projects, ideas, references, media — processes it into structured knowledge, and connects it into a living wiki.

---

## How it works (LLM + Obsidian)

Brain uses markdown files (`.md`) as its database. Obsidian provides the visual interface and linking. AI agents help you create, organize, and retrieve content.

**Two modes of operation:**

| Mode | AI capabilities | What the AI does |
|------|----------------|------------------|
| **Full access** | Can create folders, read/write files (e.g., Claude Code, local LLM with filesystem permissions) | Executes commands directly: creates vault structure, saves snapshots to `B01 Projects/` |
| **Manual / Chat-only** | No filesystem access, no internet fetch (typical web chat) | Outputs markdown + scripts for the user to copy, paste, and execute manually |

Brain is designed to work well in **both modes** — no feature is locked behind capabilities that most AIs don't have.

---

## Getting started

1. Open the file [`activate.md`](./activate.md) from this repository.
2. Copy its entire content.
3. Paste it as the **first message** in a conversation with any AI (Claude, ChatGPT, local LLM, etc.).
4. Follow the AI's instructions.

> The activation block contains all the logic. The AI will guide you through setup or snapshots based on your choices.

---

## Repository files

| File | Purpose |
|------|---------|
| `activate.md` | **Activation block** – copy and paste this into any AI chat to start |
| `project_brain.md` | Vault structure, commands (`/init_brain`, `/brain_status`), configuration, philosophy |
| `skills/project_snapshot.md` | Command `/project_snapshot` – exports project notes |

---

## Vault structure (created by `/init_brain`)

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
└── D00 Claude/         AI agent workspace
    ├── CLAUDE.md       Agent instructions
    ├── memory.md       Persistent context
    ├── sources/        Raw sources to process
    │   └── processed/
    └── Skills/         Skill logic files (ingest, extract, lint, memory, consolidate)
```

---

## Requirements

- [Obsidian](https://obsidian.md/) – for navigating and editing the vault
- Any AI chat (web or local) – paste the content of `activate.md` as the first message