# Skill: /consolidate

Audits the vault for fragmented, duplicated, or inconsistent knowledge and proposes consolidation actions.
Execute only when the user types `/consolidate`.

---

## Phase 0 — Vault Snapshot

Before any analysis, take a baseline census:

1. Count total pages in `C01 Wiki/` per subfolder
2. Count pages by content size:
   - **Stub** — fewer than 10 lines of actual content
   - **Short** — 10–30 lines
   - **Full** — 30+ lines
3. Count total internal `[[wikilinks]]` across all Wiki pages
4. Store this snapshot mentally — report it at the end as before/after comparison

Report: "Snapshot taken: X pages across Y subfolders. Z stubs, W short, V full pages."

---

## Phase 1 — Detection

Run all layers. Collect findings — do not act yet.

### Layer 1 — Title Similarity (Fragmentation)
- Scan all page titles in `C01 Wiki/`
- Group titles that share a root term, acronym, or abbreviation
  - Examples: `CAN`, `FDCAN`, `FDCAN1`, `FDCAN2` → candidate group
  - Examples: `I2C`, `I2C Bus`, `I2C Protocol` → candidate group
- Flag groups with 2+ pages as **fragmentation candidates**

### Layer 2 — Stub Orphans
- Find pages with fewer than 10 lines of content AND fewer than 2 incoming backlinks
- These are likely abandoned stubs — candidates for merge or deletion
- Flag as **stub orphans**

### Layer 3 — Co-citation Clusters
- Find sets of pages that are consistently linked together from the same source notes
- If pages A, B, and C are always linked from the same project files, they may describe the same concept
- Flag as **co-citation clusters**

### Layer 4 — Terminology Inconsistency
- Scan all `[[wikilinks]]` across the vault (including projects, inbox, daily notes)
- Find links that reference terms not matching any existing page title exactly
- Examples: link says `[[HAL Driver]]` but page is titled `STM32 HAL` → inconsistency
- Flag as **broken terminology** (different from broken links — the concept exists but the name doesn't match)

### Layer 5 — Conflicting Definitions
- For pages in the same title-similarity group (Layer 1), compare their opening definitions
- If two pages define the same term differently, flag as **definition conflict**
- Note: this requires reading page content — skip if vault is very large (100+ pages)

### Layer 6 — Hierarchy Violations
- Find pages whose title is a numbered or qualified variant of another page
  - Pattern: `[Concept]N`, `[Concept] Type X`, `[Concept] Mode Y`
  - Examples: `FDCAN1`, `FDCAN2` relative to `FDCAN`
  - Examples: `Timer Mode PWM`, `Timer Mode Input Capture` relative to `STM32 Timers`
- Flag as **hierarchy violations** — these are likely subsections living as standalone pages

### Layer 7 — Anchor Topic Drift
- For each subfolder in `C01 Wiki/`, check if a corresponding MOC exists in `A02 Anchor Topics/`
- For existing MOCs, check if they list pages that no longer exist or miss pages that do exist
- Flag as **MOC drift**

---

## Phase 2 — Report

Present findings grouped by severity. Do not execute anything yet.

```
/consolidate report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴 CRITICAL — action strongly recommended
  [list fragmentation candidates and definition conflicts]

🟡 WARNING — review recommended  
  [list stub orphans, co-citation clusters, hierarchy violations]

🔵 INFO — low priority
  [list terminology inconsistencies, MOC drift]

Total: X issues found across Y categories.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For each group, show:
- The pages involved
- Why they were flagged
- Suggested action: **merge** / **restructure** / **link** / **rename** / **delete**

---

## Phase 3 — Owner Decision

Present each flagged group as a numbered decision:

> "Group 1: FDCAN, FDCAN1, FDCAN2, CAN — 4 pages
> Suggestion: merge FDCAN1 and FDCAN2 as sections inside FDCAN; link CAN → FDCAN
> Action? (merge / restructure / link / rename / skip)"

Wait for owner response before proceeding. Accept:
- A number + action: `1 merge`, `2 skip`, `3 link`
- `all merge` / `all skip`
- Individual decisions per group

Do not assume — if unsure, ask.

---

## Phase 4 — Execution

For each approved action:

### Merge
1. Open all pages in the group
2. Designate the most complete page as the **primary** (usually the most linked or most content)
3. Absorb unique content from secondary pages into the primary — add as new sections or expand existing ones
4. Update the Sources section of the primary to include all sources from merged pages
5. In every file across the vault that links to a secondary page, replace the link with the primary page link
6. Move secondary pages to `B04 Archive/` with a header note: `> Merged into [[Primary Page]] on [date]`

### Restructure
1. Open the parent page
2. Create new `##` sections for each sub-concept page
3. Move content from sub-pages into those sections
4. Archive sub-pages with note: `> Restructured as section of [[Parent Page]] on [date]`
5. Update all backlinks vault-wide

### Link
1. Add a `## Related` entry on each page pointing to the others
2. Add a disambiguation note at the top if concepts are often confused:
   `> Not to be confused with [[Related Concept]]`

### Rename
1. Rename the page file to the canonical term
2. Update all backlinks across the vault to use the new name

### Delete (stubs only)
1. Confirm the page has no unique content not covered elsewhere
2. Move to `B04 Archive/` with note: `> Archived (empty stub) on [date]`
3. Remove all links pointing to it

---

## Phase 5 — Post-Consolidation Verification

After all executions:

1. Re-run Layer 1 (title similarity) — confirm groups are resolved
2. Re-run Layer 4 (terminology) — confirm broken terminology reduced
3. Run a broken link scan — confirm no links were left dangling after merges/renames
4. Re-check Anchor Topics in `A02/` — update any MOC that now has outdated links

Report: "Verification complete. X issues resolved. Y links updated. Z pages archived."

---

## Phase 6 — Wrap Up

1. Update `D00 Claude/memory.md`:
   - Log what was consolidated and why
   - Update Wiki page count
   - Note any patterns observed (e.g., "peripheral sub-variants tend to fragment")
2. Update relevant Anchor Topics in `A02 Anchor Topics/` to reflect new structure
3. Present before/after comparison using the Phase 0 snapshot

Report final summary:
> "Consolidation complete.
> Before: X pages | After: Y pages | Archived: Z | Links updated: W
> Patterns noted in memory.md."
