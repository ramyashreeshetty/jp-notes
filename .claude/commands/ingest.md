---
description: Pull new class notes from notes/inbox into the brain
---

Ingest new notes into the brain.

1. List everything in `notes/inbox/` except `README.md`. If empty, say so and stop.
2. Read each file. Images are fine — read them and transcribe.
3. Read `brain/grammar.md`, `brain/vocab.md`, `brain/kanji.md` first so you know
   what's already recorded.
4. Extract every grammar pattern, word, and kanji. For each one, decide:
   - **Already in the brain** → leave the level alone, but add the new example
     or nuance if the notes teach something the existing row doesn't capture.
   - **New** → add a row at L0, last tested blank, source = the note's date.
5. Write the brain files. Keep them sorted weakest first.
6. Move each ingested file from `notes/inbox/` to `notes/YYYY-MM-DD-<slug>.md`,
   using the class date if the notes state one, otherwise today.
7. Regenerate `STATUS.md`.
8. Update `index.html`, adding the new material to the right *topic* section
   rather than a new dated one.
9. Publish both copies of the site, as described under "The textbook" in
   `CLAUDE.md`: commit and push to `main` for GitHub Pages, and publish the
   stripped copy to the artifact URL.
10. Report: what was added, what was already known, and anything in the notes that
   was ambiguous or that you couldn't parse — ask about those rather than guessing.

If the notes contradict something already in the brain, don't silently overwrite.
Flag the conflict and ask.
