# Non-Developer Question Style (비개발자 친화 질문 형식)

## Purpose
This rule EXTENDS `common/question-format-guide.md`. The base format (multiple choice, "Other"
as the last option, `[Answer]:` tags, contradiction/ambiguity detection) STILL applies. This rule
adds requirements that make every question answerable by a non-technical participant.

## MANDATORY additions to EVERY question you generate
1. **Plain-language framing** — directly under the question title, one line starting with
   `> 💡 쉽게:` that explains, in everyday language (analogy if helpful), what this question
   decides and why it matters. No undefined jargon.
2. **Per-option plain explanation** — under each meaningful option (A, B, C…), one line
   `비개발자 설명:` describing what choosing it means in everyday terms. If a technical term is
   unavoidable, gloss it.
3. **A recommended default** — mark exactly ONE option with `⭐ 추천` and add a line `왜:` giving
   a one-sentence reason it is the safe, common-case choice. Pick the most broadly suitable,
   lowest-risk, best-supported default for a typical project.
   - The recommendation is a SUGGESTED DEFAULT, never a requirement. If the user picks another
     option (including "Other"), honor it without pushback.
   - **Recommendation bias — non-developer running LOCALLY, no deployment yet.** Assume the audience
     is a non-developer who will build and SEE the result on their own machine first; there is no
     production deployment for now. So the ⭐ default should favor the option that:
     - runs locally with the least setup — prefer local/file/SQLite over managed cloud DBs, local
       dev server over cloud deploy, no external accounts / API keys / payment / production infra;
     - gets them to a working, visible result on their own computer fastest.
     Only recommend a cloud/deployment/managed option as the ⭐ default if the requirements clearly
     demand it; otherwise mention it as a non-default option ("이럴 때: 나중에 실제 배포할 때").
   - If genuinely no option is a safe default (truly context-dependent), replace `⭐ 추천` with a
     line `> 판단 필요:` naming the one fact that would decide it, and ask for that fact.

## Format template (extends the base format)
```markdown
## Question [N] — [질문 제목]
> 💡 쉽게: [이 질문이 무엇을 정하는지 일상어로]

A) [option]
   비개발자 설명: [일상어 설명]
   ⭐ 추천 — 왜: [한 문장 사유]

B) [option]
   비개발자 설명: [일상어 설명]
   이럴 때: [이 옵션이 맞는 상황]

X) Other (please describe after [Answer]: tag below)

[Answer]:
```

## Visual decisions (any stage)
When a question is about UI/screen layout, navigation, or visual hierarchy AND the choice is hard
to judge from text alone, ALSO follow `common/visual-mockup-guide.md` to present mockups
together with the text question. This applies in EVERY stage that asks such a question
(Requirements Analysis, User Stories, Application Design, and Construction) — not only User Stories.

## Interaction with overconfidence-prevention
This rule does NOT reduce how many questions you ask. Keep asking whenever there is ambiguity
(see `common/overconfidence-prevention.md`). The recommendation only helps the user answer faster;
it never lets you skip a needed question or assume an answer.
