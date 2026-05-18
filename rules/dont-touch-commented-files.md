# Instruction (ALWAYS-ON, all future sessions included)

Do **not** modify `*.commented.py` (or any `*.commented.*`) annotated-reference files unless the **current user message** explicitly names that exact file. This rule applies in every session — past, present, and future — without re-confirmation from the user. Treat it as effectively a hard guardrail, not a soft preference.

## Rules

1. **Treat `*.commented.*` as read-only by default.** They are the user's curated annotated copies of the live code — manually maintained for human reading, not for the runtime.
2. **Live edits go to the live file only.** When changing a function's behavior or refactoring, edit the live source (e.g. `preprocess.py`) and leave `preprocess.commented.py` untouched.
3. **Explicit verb required.** Only modify a `*.commented.*` file when the user says something specific like "update `preprocess.commented.py`", "sync the commented file", "annotate this in the commented copy". Generic "update the docs/comments" does NOT include the commented file.
4. **Don't re-sync proactively.** If the live file drifts ahead of the commented file, leave the drift. The user will reconcile when they want to. Don't "fix" it on your own.
5. **Don't grep / read them as authoritative.** When verifying behavior or learning code, prefer the live file over the commented copy — the commented copy may be stale.

## Failure modes to avoid

- Updating `preprocess.commented.py` whenever you update `preprocess.py` "to keep them in sync" — that's the user's call.
- Including the commented file in a broader sweep ("Korean comments default" or similar) without explicit instruction.
- Treating the commented file as the source of truth when its content disagrees with the live file.

## Principle

`*.commented.*` files exist because the user wants a stable, hand-curated reading copy decoupled from the live code's churn. Auto-syncing destroys that decoupling.
