---
description: Run a Japanese quiz weighted to weak spots and due items
---

Run a test session. Arguments (optional): a focus area, e.g. `/test particles`
or `/test vocab from last week`. With no arguments, cover everything due.

**Build the quiz:**

1. Read `STATUS.md`, all three `brain/` files, and `log/mistakes.md`.
2. Select items: everything **due** (see the level table in `CLAUDE.md`),
   weighted toward L0–L1 and anything in "Active problem areas".
3. If nothing is due, say so and offer a review of the weakest items instead —
   don't invent a test out of nothing.
4. Aim for 10–15 items. Fewer if there isn't enough material yet.

**Run it:**

Ask questions one at a time and wait for each answer. Never show the answer
before they've responded. Mix the formats:

- Recognition: what does this mean?
- Recall: how do you say this in Japanese?
- Production: make a sentence using X
- Correction: here's a sentence with a mistake, find it

**Always end with the sentence exercise:** three sentences to translate into
Japanese, built only from grammar and vocabulary already in the brain, and
targeting the weak spots. This is the part that matters most — prioritise it
even if the rest of the quiz runs short.

**Mark it honestly:**

Wrong is wrong. Say so and explain why. If something is grammatically correct
but not how a Japanese speaker would say it, mark it correct and explain the
natural version — that gap is where real progress lives.

**Write results to disk before showing the summary:**

- Update levels in `brain/` — up one for correct, down to L1 for wrong. Set
  last tested to today for everything tested.
- Append every wrong answer to `log/mistakes.md`, including *why* it went wrong.
- Promote anything wrong 3+ times to "Active problem areas".
- Append a row to `log/sessions.md`.
- Regenerate `STATUS.md`.

Then show the summary: score, what moved up, what dropped, and the one thing to
focus on before the next session.
