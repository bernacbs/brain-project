# project_snapshot

![Version](https://img.shields.io/badge/version-2.6.0-blue)

## What is this file
Defines the command `/project_snapshot`.  
**Script-like instruction.** Only execute when user types `/project_snapshot`.

Generates a **linked knowledge snapshot** with explicit wikilinks, relationships, and a **stability mechanism** that asks the user for missing information before creating the final output. No guessing, no `TBD` without explicit user permission.

---

## Configuration

```yaml
LANGUAGE: en
```

---

## Command trigger

Execute **only** on exact message: `/project_snapshot`

---

## Phase 0: Context check

Does the conversation contain **any project-related context**? (at least a mention of a project name or goal)  
If **no**: reply: *"I don't see any project in this conversation. Please tell me the project name and what it's about. Then type `/project_snapshot` again."*  
If **yes**: proceed to **stability loop**.

---

## Phase 1: Stability loop – identify and resolve gaps

**Step 1 – Assess completeness**

From the conversation, determine which of the following essential fields are **missing or unclear** (lack explicit, actionable information):

- **Project name** (clear, unique identifier)
- **Objective** (what problem it solves, in one or two sentences)
- **Status** (active, paused, completed – if mentioned)
- **Stack / Tools** (specific languages, frameworks, hardware, services)
- **Architecture & key decisions** (any design choices and why)
- **Problems & solutions** (issues encountered, how resolved)
- **Next steps** (concrete actions planned)
- **People / researchers involved** (if any)
- **References / links** (any URLs or document mentions)
- **Relationships** (how this project relates to other projects, concepts, or MOCs)

**Step 2 – Generate a structured question list**

If any gaps exist, create a **numbered list of questions** asking the user to provide **specific missing information**. Never ask yes/no questions when an open answer is needed. Examples:

> *"Before I generate the snapshot, could you please provide:*
> 1. *The main objective of [Project Name]?*
> 2. *Which programming languages or tools are being used?*
> 3. *What were the main technical decisions and why?*
> 4. *Any known problems you encountered and how you solved (or plan to solve) them?*
> 5. *What are the next concrete steps?*
> 6. *Are there any relevant links (repository, documentation, article)?*"

**Step 3 – Output questions and wait**

- Output the questions in a clear, **non‑repetitive** message.
- Do **not** guess answers. Do **not** generate a partial snapshot.
- Wait for the user to answer. The user may answer all at once, or one by one.

**Step 4 – Iterate if needed**

If after the user's answers there are still gaps (e.g., they skipped some questions or gave incomplete info), ask **only for the remaining missing items** in a follow‑up.

**Step 5 – Complete**

Once all essential fields are filled (or the user explicitly says "proceed with what you have"), proceed to Phase 2.

---

## Phase 2: Structured thinking (internal chain of thought)

**Perform these reasoning steps internally, before writing the snapshot.** Do not output the thinking unless the user asks.

```
[INTERNAL THINKING]
1. Central topic / project name: ...
2. Extract entities (with frequency if available):
   - Technologies, tools, frameworks
   - People, researchers, developers
   - Methods, concepts, patterns
   - Organizations, repositories
3. For each entity, detect variations → choose canonical name (e.g., "Claude AI" → [[Claude]]).
4. Identify relationships (subject - predicate - object):
   - [[Project]] uses [[Tool]]
   - [[Person]] proposed [[Idea]]
   - [[Problem]] solved by [[Solution]]
5. Which are the high‑value entities? (appear >=2 times or are domain‑specific)
6. Suggested tags (lowercase, no spaces) based on entities and project domain.
7. Suggested Anchor Topics (MOCs) from `A02 Anchor Topics/` that would index this project (or propose new MOC names).
8. Note ambiguities (e.g., "Apple" as company vs fruit) and decide on disambiguated name: [[Apple (company)]].
```

---

## Phase 3: Generate the snapshot

Produce the snapshot in markdown format with frontmatter and sections, using **wikilinks** throughout.

### Output format

```markdown
---
status: active | paused | completed
tags: [tag1, tag2, project, inferred-tags...]
updated: YYYY-MM-DD
---

# [Project Name]

## Objective
[Description with wikilinks]

## Status
[ ] Active  [ ] Paused  [ ] Completed

## Stack / Tools
- [[Tool1]]
- [[Tool2]]

## Architecture & Decisions
[Text with wikilinks; include relationship phrasing e.g., "[[Component A]] calls [[Component B]] via [[API]]"]

## Problems & Solutions
[Issues and resolutions, linking to entities.]

## Next Steps
[Concrete actions, linking to MOCs or related projects.]

## References

### Knowledge base
> Confirmed references — already processed or manually curated.
- [Title](URL) — [[Related Entity]]

### Sources queue
> Links and files listed here will be fetched and processed into `D00 Claude/sources/` by the agent on the next `/ingest` run.
> Agent reads this section, fetches each item, saves raw content to sources/, then clears the checkbox.
- [ ] <!-- paste URL or file path here -->

### Local files
> Files already in `_Assets/` or accessible locally that relate to this project.
- <!-- [[_Assets/filename.pdf]] -->

## Keywords / Links
**Technologies & Tools:** [[A]], [[B]]  
**People:** [[C]], [[D]]  
**Concepts & Methods:** [[E]], [[F]]  
**Projects:** [[G]]

## Relationships (explicit key links)
- [[Project]] → uses → [[Tech]]
- [[Person]] → wrote → [[Paper]]

## Suggested Anchor Topics (MOCs)
Consider adding this project to: [[Suggested MOC1]]  
Or create a new MOC: [[New Topic MOC]]
```

If, after the stability loop, the user explicitly allows `TBD` for some fields, use `TBD` as a placeholder – but never invent details.

---

## Output behavior

### With filesystem access
- Save/update directly to `B01 Projects/Project-Name.md`
- Output: `Snapshot saved to B01 Projects/Project-Name.md`

### Without filesystem access (chat-only)
- Output: `[FIRST SNAPSHOT]` or `[UPDATED SNAPSHOT]`
- Then the snapshot markdown (as above)
- Then on a new line: `Copy this and save as B01 Projects/Project-Name.md`

---

## Memory across calls

Remember if `/project_snapshot` was already called in this conversation. If yes, and the snapshot was already generated, update the existing snapshot (same file name) with new conversation context, **but first re‑run the stability loop** – because new information may have been added since the last generation.

---

## Rules

- **Never guess or hallucinate information.** If data is missing, use the stability loop to ask.
- **Only generate the snapshot after all essential gaps are filled** (or user explicitly waives).
- **Use English for technical terms** even when `LANGUAGE` is pt-BR, unless a clear Portuguese equivalent is standard.
- **Update the `updated` field** on every snapshot.
- **No sensitive data** (keys, passwords) anywhere.