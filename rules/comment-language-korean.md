# Instruction

When writing or editing **code comments and docstrings**, default to **Korean**. When touching nearby code in any file, convert pre-existing English comments to Korean opportunistically.

## Rules

1. **All new code comments and docstrings → Korean.** Module docstrings, function docstrings, inline `#` comments, class docstrings. Default language is Korean.
2. **Existing English comments → convert when touching that file.** "가능한 한 한글로" — if you're already editing a file, convert nearby English comments in the same pass. Don't convert files you aren't otherwise touching just for translation.
3. **Keep English for searchable tokens.** `TODO:`/`FIXME:`/`NOTE:`/`HACK:` prefixes, `[bug]`/`[assumption]`/`[hack]` tags, API symbol references, exact error strings, RFC numbers, ISO standards — leave English so grep/IDE search still works.
4. **Markdown docs and prose responses are separate.** This rule applies to **code comments**. `docs/*.md` and user-facing response text follow the language of the conversation. New doc sections added when the user is speaking Korean should be Korean; existing English docs aren't translated proactively.
5. **License headers and generated boilerplate.** Don't rewrite. They're not really "comments" — they're metadata.
6. **Auto-generated docstring sections (Args / Returns / Raises) work in Korean.** It's OK to write "반환: ..." or "Args: ..." with Korean body text.

## Failure modes to avoid

- Mixing English explanation and Korean within one comment block — pick one language per comment.
- Translating identifiers or string literals (which would change behavior) instead of just the surrounding prose.
- Leaving English comments untouched in a file you just substantially edited.

## Principle

Korean by default because the user thinks in Korean for this project. English stays only where it's load-bearing for tools (keywords, search) or external (licenses, generated content).

