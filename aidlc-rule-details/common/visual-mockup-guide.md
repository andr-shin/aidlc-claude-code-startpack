# Visual Mockup Guide (시각적 목업 가이드)

Adapted for AIDLC from the brainstorming "visual companion" method: show a picture when a
picture beats words. AIDLC runs inside the user's coding tool, so instead of a live server we
generate a self-contained HTML mockup file the user opens in a browser, and they answer with
the existing `[Answer]:` mechanism.

## Where this applies (ANY stage — not just one)
This is a cross-cutting rule (loaded via `common/nondev-question-style.md`), so it applies to
EVERY stage that asks a question, whenever the trigger below is met. It is NOT limited to User
Stories. The most common places a visual decision arises:
- **Requirements Analysis** — user-facing scope (e.g., "does it have a docs portal / dashboard?").
- **User Stories** — user journeys, screen flows, navigation between screens.
- **Application Design** — page/screen composition, component placement, information hierarchy.
- **Construction (functional / UI design, frontend code generation)** — concrete screen/component
  layout before writing UI code.

Save the mockup next to the stage that asked it: `aidlc-docs/inception/mockups/<topic>.html` for
inception stages, or `aidlc-docs/construction/<unit>/mockups/<topic>.html` for construction. The
trigger and the option-letter ↔ `[Answer]:` bridge are identical in every stage.

## When to use a mockup
Use a mockup in EITHER case below.

**Case A — UI/layout decision (ALL three must hold):**
1. The decision is about UI/screen layout, navigation structure, or visual hierarchy.
2. There are 2+ meaningfully different visual directions to choose between.
3. A text description would be ambiguous — the user would understand it better by seeing it.

**Case B — functionally-critical decision (even if NOT a pure UI-layout choice):**
When a decision is critical to how the product fundamentally works — a core feature, a key user
flow, a state machine, an important data/interaction flow — AND a picture would help a
non-developer confirm it far better than text, produce a visual. It may be a screen mockup OR a
simple flow / sequence / state diagram (still a self-contained HTML file with A/B/C options when
there is a choice, or a single explanatory diagram when you just need confirmation). Use this
sparingly — only for genuinely critical decisions, not every feature.

Still SKIP purely textual/conceptual/scope questions and trivial data-modeling choices where the
answer is words, not something worth seeing.

## ALWAYS: inception wrap-up mockup
Regardless of whether any trigger above fired, at the END of the INCEPTION phase (after the last
inception stage is approved, just before moving to CONSTRUCTION) you MUST produce at least one
wrap-up mockup that summarizes everything understood so far: the product's main screen(s) and/or
its primary user flow. Save it to `aidlc-docs/inception/mockups/inception-summary.html`, tell the
user in Korean to open it in a browser, and ask whether it matches their expectation before
construction begins. This guarantees the user sees the product visually at least once even if no
earlier trigger fired.

## How to build the mockup
1. Write a self-contained HTML file to `aidlc-docs/inception/mockups/<topic>.html`:
   - No external/network dependencies; inline CSS only. Must open by double-click.
   - Present 2–4 options on one page, labeled A / B / C (/ D), each in its own labeled box.
   - Wireframe fidelity: focus on layout and structure, not pixel-perfect polish.
   - Use realistic placeholder content so the layout reads clearly.
   - All visible text in Korean (per `common/language-korean.md`).
2. Create the matching question in the normal question file, using option letters that match the
   mockup boxes, following `common/nondev-question-style.md` (plain framing + a ⭐추천).
3. Tell the user, in Korean: which file to open in a browser, what they are comparing, and to put
   their chosen letter after `[Answer]:` in the question file.

## After the user answers
- Read the `[Answer]:` letter as usual. If the user revised their choice in chat, honor the latest.
- If feedback asks to change the mockup, write a NEW file `<topic>-v2.html` (never reuse a
  filename) and ask again. Advance only when the choice is settled.

## Minimal HTML skeleton (copy and fill)
```html
<!doctype html><html lang="ko"><meta charset="utf-8"><title>화면 시안 비교</title>
<style>
 body{font-family:system-ui,sans-serif;margin:24px;background:#f6f7f9}
 h1{font-size:18px} .opts{display:flex;gap:16px;flex-wrap:wrap}
 .opt{background:#fff;border:1px solid #d0d4da;border-radius:10px;padding:16px;width:320px}
 .tag{display:inline-block;font-weight:700;background:#111;color:#fff;border-radius:6px;padding:2px 8px}
 .wire{border:1px dashed #9aa0a6;border-radius:6px;padding:10px;margin-top:10px;min-height:120px}
 .bar{background:#e9edf2;border-radius:4px;height:14px;margin:6px 0}
</style>
<h1>아래 시안을 보고, 질문 파일의 [Answer]: 에 A/B/C 를 적어주세요</h1>
<div class="opts">
 <div class="opt"><span class="tag">A</span> 상단 메뉴형
   <div class="wire"><div class="bar" style="width:100%"></div><div class="bar" style="width:60%"></div><div class="bar" style="width:80%"></div></div></div>
 <div class="opt"><span class="tag">B</span> 좌측 사이드바형
   <div class="wire"><div style="display:flex;gap:8px"><div style="width:80px"><div class="bar"></div><div class="bar"></div></div><div style="flex:1"><div class="bar" style="width:90%"></div><div class="bar" style="width:70%"></div></div></div></div></div>
</div>
</html>
```
