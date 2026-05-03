# Skill: /extract

Extracts reusable knowledge entities from a project note and proposes Wiki pages.
Execute only when the user types `/extract [filename]` or `/extract` (scans all projects).

---

## Steps

1. Read the specified file from `B01 Projects/` (or all files if no filename given)
2. Identify entities that could become standalone Wiki pages:
   - Technologies, components, protocols, tools (e.g., STM32-Timers, I2C, DMA, ADC)
   - Concepts, methods, patterns
   - Do NOT include: project-specific decisions, temporary context, failed attempts
3. For each candidate, check if a page already exists in `C01 Wiki/`
4. Present the owner with a numbered list:
   > "Found X concepts not yet in the Wiki:
   > 1. [[Concept A]] — [one-line description]
   > 2. [[Concept B]] — [one-line description]
   > Which would you like to create? (reply with numbers, 'all', or 'none')"
5. Wait for owner approval — do not create anything without confirmation
6. For approved items: create stub pages in the correct `C01 Wiki/` subfolder using the Wiki Page Format in `CLAUDE.md`
7. Update relevant Anchor Topics in `A02 Anchor Topics/`
8. Update `memory.md` with what was extracted and approved
