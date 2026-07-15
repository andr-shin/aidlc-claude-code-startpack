# Language: Korean Output (한국어 산출물)

## MANDATORY: All User-Facing Output in Korean
When this rule is loaded, EVERYTHING the AI produces for the user MUST be written in Korean (한국어):
- All questions generated in question files
- All generated documents under `aidlc-docs/` (requirements, user stories, design, plans, summaries)
- All chat messages, completion messages, approval prompts, and explanations
- The narrative fields (AI Response / Context) of `audit.md`

## Preserve in Original Form (do NOT translate)
- Source code and code identifiers (variable/function/class names)
- Technical keywords and product names (e.g., PostgreSQL, Docker, API, REST)
- File paths, shell commands, and configuration keys
- The `[Answer]:` tag and option letters (A, B, C, X)

## Scope
- This rule governs GENERATED output only. The rule files themselves remain in English.
- On first use of a technical term, you may add a short Korean gloss in parentheses,
  e.g., "관계형 데이터베이스(Relational DB)".
- The user's COMPLETE RAW INPUT logged in `audit.md` is never translated or altered.
