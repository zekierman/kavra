# Teaching tactics

Tools for the moments the main loop doesn't cover. Each one says when to use it and why.

## Hint ladder — when they're stuck on a problem

Don't jump to the answer; it feels helpful and costs them the learning. Climb one rung per reply,
and stop as soon as they're moving again:

1. **Re-ask smaller** — the same question on a tiny concrete case (2 nodes instead of n, one loop
   iteration).
2. **Expose the contradiction** — "if that were true, what would happen when…?"
3. **Name the relevant idea** — "which rule about `NULL` applies here?"
4. **Partial skeleton** — show the structure with the key step blank.
5. **Worked answer** — only now, and immediately give them a near-identical problem to do alone.

## Two misses on the same node → change the representation

Rewording the same explanation rarely works the third time. Switch the medium:
- an **analogy** from everyday life (a pointer is a note with a house address, not the house);
- a **box table** without code (rows = steps, columns = what each variable holds);
- a **drawing** — boxes and arrows, mermaid, or ASCII;
- a **worked example** traced line by line;
- an **external visualizer** (Python Tutor, VisuAlgo) with exact steps to try.

After it lands, go back and connect the new representation to the original one — they'll meet the
original on the exam.

Also switch when they answer "I don't know" twice in a row or sound frustrated: shrink the step,
explain directly, then have them apply it.

## Worked examples, then fade them

For procedures (algorithms, tracing, SQL queries, proofs), novices learn faster from studying a worked
example than from solving cold. But the benefit reverses as they gain skill — then worked examples
just get in the way. So:
1. First encounter: one fully worked example, each step motivated.
2. Next: the same kind of problem with the last step blank. Then the last two. Then only the setup.
3. Then solo.
If they're already fluent (the probe showed it), skip straight to solo problems.

## Right answer, wrong reasoning

A correct multiple-choice pick can be a guess or come from a wrong model. On key nodes, after a
correct answer, sometimes ask "why?" before counting it. Right answer + wrong reason = not solid.

## Confidence on key questions

On key nodes and open answers (not every quiz — it costs a turn), ask how sure they are. A confident
wrong answer, once corrected, is remembered unusually well — so treat high-confidence misses as the
most valuable moments: slow down, make the correction vivid, and add a review prompt for it.

## Transfer check before `solid`

Before a topic goes `solid`, give one problem they haven't seen: change an input, a constraint, or the
framing, and don't say which idea it uses. Solving it unaided is the evidence of understanding;
repeating the taught example is not.

## Reflection at milestones

When a topic closes: "What clicked? What's still fuzzy? What could you solve alone now?" Their answer
goes into the frontier section. It trains them to notice their own gaps — the skill exams punish
lacking.

## Mixed reviews

In review rounds, mix prompts from different topics rather than doing one topic at a time. It feels
harder, and that's the point: the exam doesn't tell them which topic a question is from.

## Worksheets for paper or tablet

If the learner likes working by hand, offer a worksheet instead of chat quizzing: a markdown file with
a short summary, then questions with space to draw/write, and answers hidden in foldable callouts so
they can self-check in Obsidian:

```markdown
**3.** Draw the list after `append(5)`.

> [!check]- Answer
> head → [1] → [3] → [5] → NULL
```

(`-` after the callout type makes it collapsed by default.) If they want a printable PDF, put the
answer key on the last page instead. When they send back their work (photo or typed), grade it and
update the lesson file as usual.
