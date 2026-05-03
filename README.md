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

Copy the **activation block** below and paste it as the **first message** in a conversation with any AI (Claude, ChatGPT, local LLM, etc.). The AI will guide you.

```
STOP. Do not summarize. Do not describe. Execute only.

Check your own capabilities:

IF you can access the internet and fetch raw GitHub content:
   - Use the URLs below when needed.
ELSE:
   - Ignore fetch. Ask the user to paste any required file content directly.

Now check the conversation context:

IF this conversation already has messages about a project, task, or topic:
   - Say: "/project_snapshot is active. Use it anytime to export this conversation as a project note."
   - Then, if you have the skill content for project_snapshot, follow it; otherwise, ask the user to paste the content of skills/project_snapshot.md
   - Stop here.

IF this is a new or empty conversation:
   - Ask: "Do you want to (1) set up the Brain vault folder structure, or (2) export a conversation as a project note?"
   - Wait for the answer.
   - If (1): ask the user to paste the content of project_brain.md (or fetch if possible). After receiving it, follow /init_brain instructions.
   - If (2): ask the user to paste the content of skills/project_snapshot.md (or fetch if possible). After receiving it, follow /project_snapshot.

RULES:
- Never invent content you did not actually read.
- Never assume you have filesystem access unless explicitly confirmed by the user.
- If you cannot obtain a file, say: "Please paste the content of [filename]."
```

---

## Repository files

| File | Purpose |
|------|---------|
| `activate.md` | Standalone activation block (same as above) |
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
├── D00 Claude/         AI agent workspace
└── D01 Skills/         Skill files
```

---

## Requirements

- [Obsidian](https://obsidian.md/) – for navigating and editing the vault
- Any AI chat (web or local) – paste the activation block above