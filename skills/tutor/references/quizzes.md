# Quizzes

A quiz has a right answer. An open question ("what do you want to focus on?") doesn't — ask that
normally, never as a quiz. A Socratic "try to discover it" question with a definite answer *is* a
quiz; grading it is how you learn exactly where their model goes wrong.

## Writing options that don't leak the answer

Checking for evenness after the fact doesn't work — the tell is baked in while writing. Build the
options so evenness is automatic:

1. **Every option is a bare claim. No justification in any option.** The #1 giveaway is the correct
   option carrying its own reasoning ("…, because it preserves X") while distractors are bare. All
   reasoning goes in the feedback after they answer.
2. **Write the correct claim first, then mutate it into each distractor.** Take one specific
   misconception or easily confused neighbour and state what someone holding it would claim — same
   skeleton, same length, same register. Each option is "the claim under some belief".
3. **Every distractor is a real error they might make**, so which one they pick is diagnostic — but
   unambiguously wrong on the intended reading. Tempting, not tricky.
4. **No asymmetric emphasis.** Bold nothing, or bold the parallel term in every option.
5. **Randomize where the correct option sits.** Never always B. Never label any option
   "(Recommended)" or similar, even if your tool's conventions suggest it.

Reading the finished set cold, if you can tell which is right without knowing the material,
regenerate — don't patch.

Always offer **"I don't know"** as an option. An honest "don't know" is information; a lucky guess
is noise that hides a gap.

## Asking, per environment

- **Claude Code** — use `AskUserQuestion`. It allows 2–4 options and adds a free-text "Other"
  automatically, so use up to 3 real options + "I don't know". Use `multiSelect: true` only when the
  question says "select all that apply". Put the question stem in `question`, keep `header` short
  (e.g. "Q3"). No option descriptions that hint at correctness.
- **Any other agent with a native question/choice tool** (e.g. Antigravity's `ask_question`) — use it
  the same way: 3 real options + "I don't know", no recommendation tags, correct position randomized.
- **Codex, plain chat, or any choice tool that preselects an option** (a preselected option biases
  the answer) — write the question with
  lettered options (A–C plus D = "I don't know"), then **end your turn and wait**. Never put the
  answer, a hint, or the feedback in the same message.
- **Open-response questions** (explain, trace, write code, calculate) — ask in plain text and wait.
  These are closer to real exam questions; use them at least once per topic.

## Grading

After they answer, in one short block:
- ✓ or ✗, and the correct answer.
- *Why* it's correct, grounded in the nodes already established (and the course source, if any).
- If wrong: what their choice reveals about their model — "B is what you'd say if you thought the
  pointer itself moves; it's the value inside it that changes." This is the valuable part.
- For open answers: grade strictly, like the instructor would — not like a friendly tutor. A vague
  answer that "has the right idea" but misses the formal term, a condition of the definition, or a
  required step loses those points, exactly as it would on the exam. Name what earned points and
  what's missing, and log the miss.

A miss means stop and repair that node before moving on.

## Logging

After grading, append the question, their answer, and the feedback to the lesson file as one block
(format in `lesson-files.md`). One write per question keeps edits simple.
