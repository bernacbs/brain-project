# Skill: /ingest

Processes all pending content in `D00 Claude/sources/` into `C01 Wiki/`.
Execute only when the user types `/ingest`.

---

## Step 0 — Resolve Sources Queue in project files

1. Scan `A00 Inbox/sources-queue.md` and all files in `B01 Projects/` for unchecked items (`- [ ]`) under `### Sources queue`
2. For each unchecked item:
   - If URL: fetch page content and save as `.md` file in `D00 Claude/sources/`
   - If local file path: confirm file exists and reference it in `sources/`
   - If fetch fails: leave unchecked, add comment `<!-- fetch failed: [reason] -->`
   - If successful: mark as `- [x]`
3. After processing `A00 Inbox/sources-queue.md`: remove all `- [x]` lines from the file. Never delete the file — preserve the header and the empty `### Sources queue` section.
4. Scan all files in `A03 Daily Notes/` for unchecked items (`- [ ]`) under any `### Sources queue` section:
   - Process each item the same way as above
   - **Never modify Daily Notes files** — do not mark `[x]`, do not remove lines, do not add comments
   - If an item from Daily Notes was already processed (same URL found in `sources/processed/`), skip silently
5. Report: "Found X queued items across Y sources. Processing..."

---

## Step 1 — Detect content type and read

| Type | Extensions | Strategy |
|------|-----------|----------|
| Text | `.txt`, `.md` | Read directly |
| PDF | `.pdf` | Extract text if capable; if not: "Cannot read [file] — please export as .txt or .md" |
| Image | `.png`, `.jpg`, `.jpeg`, `.webp`, `.svg` | Describe and extract visible content (diagrams, schematics, text) |
| Web page | `.html`, URLs as text | Extract main content, strip navigation/ads |
| Document | `.docx`, `.odt` | Extract text if capable; otherwise notify owner |
| Spreadsheet | `.xlsx`, `.csv` | Extract data as table; summarize structure and key values |
| Code | `.c`, `.h`, `.py`, `.v`, `.vhd`, etc. | Read as technical reference; extract purpose, key functions, dependencies |
| Audio / Video | `.mp3`, `.mp4`, `.wav` | Cannot process — "Please provide a transcript or summary for [file]" |
| Unknown | any other | Attempt to read as plain text; if unreadable, notify owner |

---

## Step 2 — Synthesize into Wiki

1. Identify the knowledge domain → map to correct `C01 Wiki/` subfolder
2. Check if a page already exists for this concept
3. If yes: update and expand, note the source
4. If no: create a new page using the Wiki Page Format in `CLAUDE.md`
5. Add internal links to related existing pages
6. Update relevant Anchor Topic in `A02 Anchor Topics/`
7. Move processed source to `sources/processed/`
8. Update `memory.md`

**Link preservation rule (mandatory):** Every Wiki page created or updated by `/ingest` must include the original source URL in its `## Sources` section. The link must never be omitted, summarized, or replaced — even if the content was already known. Format:
```
## Sources
- [Page title or description](original URL) — date ingested
```
If the source was a local file, record its path. A Wiki page with no source entry is considered incomplete.
