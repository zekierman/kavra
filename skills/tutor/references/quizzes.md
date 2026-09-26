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
- **Environments without a question tool (Codex, Antigravity, plain chat)** — write the question with
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
- For open answers: grade like the instructor would. Name what earns points and what's missing
  (key term, a step, the definition's exact condition).

A miss means stop and repair that node before moving on.

## Logging

Write the question into the lesson file **before** they answer (without the answer — they may be
reading the file live), then append their answer and the feedback after grading. Format in
`lesson-files.md`.
