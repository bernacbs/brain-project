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