# Skill: /lint

Audits the vault health and reports issues without modifying anything.
Execute only when the user types `/lint`.

---

## Steps

1. **Orphan pages** — find Wiki pages with no incoming links from other notes
2. **Broken links** — find `[[wikilinks]]` that point to non-existent pages
3. **Empty folders** — list folders with no files inside
4. **Missing Anchor Topics** — find Wiki subfolders with no corresponding MOC in `A02 Anchor Topics/`
5. **Sources queue backlog** — count unchecked `- [ ]` items across all `B01 Projects/` files
6. **Stale projects** — list projects in `B01 Projects/` with `status: active` not updated in over 30 days

Report findings grouped by category. Do not auto-fix anything — owner reviews and decides.

At the end, suggest: "Run `/ingest` to process [X] pending sources queue items."
