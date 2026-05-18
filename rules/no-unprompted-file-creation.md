# Instruction

Default to outputting content as response text. Do **not** proactively create new files or update existing ones — even when the user asks for content that would naturally fit a file (timelines, plans, notes, summaries, drafts).

## Rules

1. **Output inline by default.** Markdown, tables, code blocks, plans, timelines — render them in the response, not in a `.md` file on disk.
2. **File write/edit requires an explicit verb.** Only create or modify files when the user uses a verb such as: "create file X", "save to X", "write to X", "edit X", "update X", "fix X", "add X to file Y" — where X / Y is a path or a named artifact already under discussion.
3. **Implicit asks ≠ file write.** Phrases like "give me a timeline", "draft a section", "show me a plan", "summarise this", "compare these" all mean **respond inline**, not write to disk.
4. **Active artifacts are the exception.** When the user is iterating on a specific source file (e.g., `main.tex`, `custom.bib`, code under `src/`), edits to *that* file are expected and don't need a verbatim re-confirmation each turn — but creating *adjacent* files (e.g., a `_notes.md` next to it) still needs explicit permission.
5. **Don't re-create deleted files.** If a file was previously created without a clear request and the user removed it (or asked you to stop touching it), do not recreate it.
6. **When unsure, ask.** A one-line question — *"Should I write this to a file or output inline?"* — is preferred to writing a file the user did not want.
7. **Don't delete to compensate.** If a file was created without an explicit request, do not delete it without asking. Leave it; do not write to it again; surface the situation in the next response so the user can decide.

## Failure mode to avoid

- Saving a timeline / plan / summary as `experiment_plan.md`, `notes.md`, `plan.md`, etc. when the user only asked for the content.
- Creating helper / scratch files alongside an artifact the user is iterating on.
- Writing intermediate-state files ("plan.md", "tasks.md", "todo.md") instead of using the runtime task system or just keeping state in conversation.

## Principle

The user owns which files exist in their repo. Treat file creation as a privileged action that requires explicit consent, not a default mode of working.
