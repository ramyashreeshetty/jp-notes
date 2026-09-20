# Japanese learning system

This folder is Ramya's Japanese study record. It is not a codebase — treat every
file here as knowledge state, not source code.

## Read this first, every session

At the start of any session in this folder, read:

1. `STATUS.md` — the dashboard: current level, counts, weak spots
2. `brain/grammar.md`, `brain/vocab.md`, `brain/kanji.md` — everything known so far
3. `log/mistakes.md` — active problem areas

`index.html` is the compiled reference — read the brain files, not this, when
preparing a test. It is output, not state.

Do not ask "what do you know?" — it's written down. Read it.

## The core rule

**State lives in files, never in conversation.** Every session starts blank, so
anything learned, tested, or corrected must be written to disk *at the moment it
happens* — not saved up for the end of the session. Sessions get closed abruptly.

After a test: write results before showing the summary.
After ingesting notes: write the brain updates before reporting what was added.

## Confidence levels

Every item in `brain/` carries a level and a last-tested date.

| Level | Meaning | Review interval |
|-------|---------|-----------------|
| L0 | New, never tested | next session |
| L1 | Got it wrong recently | next session |
| L2 | Shaky | 3 days |
| L3 | Getting there | 1 week |
| L4 | Comfortable | 3 weeks |
| L5 | Solid | 2 months |

An item is **due** when `last tested + interval <= today`. Correct answer moves
it up one level. Wrong answer drops it to L1 and adds a line to `log/mistakes.md`.

Never skip a level on a single correct answer. Levels are earned slowly.

## Commands

- `/ingest` — pull new notes from `notes/inbox/` into the brain
- `/test` — run a quiz session
- `/status` — show progress
- `/wrap` — catch-all: write down anything learned conversationally this session

## Learner profile — important

Ramya has been in class since **2 Dec 2025**, four classes a month, one-to-one.
The class is **conversational** — speaking and listening, not reading.

**She cannot read or write kana or kanji yet.** All her notes are in romaji.
This is deliberate for now; reading and writing are a target for the coming
months, not today.

What this means in practice:

- **Test in romaji + English only.** Never show a question in kana or kanji and
  expect an answer. Doing so tests reading, which she hasn't learned, and turns
  a grammar question into a wall.
- **Still record kana and kanji in the brain files.** The textbook slides and
  the verb sheet already carry them. Store them now, hidden from testing — when
  the reading phase starts the material is already in place and she'll be
  learning to read words she can already say. That's a big head start, so don't
  throw the script away.
- `brain/kanji.md` is therefore a **parked reference**, not an active deck.
  Nothing in it gets tested until she says the reading phase has started.

**Romaji standard:** Hepburn, with particles spelled as they are *pronounced* —
`wa`, `o`, `e` (not `ha`, `wo`, `he`). Her teacher's notes are inconsistent
(`ha`/`wa`, `syoyu`/`shouyu`, `tusugi`/`tsugi`); normalise when ingesting, and
note the written form in parentheses on the particle entries, since that's the
bridge to reading later. Long vowels: `ou`/`uu` as the notes do (`koohii`,
`shuumatsu`).

## Curriculum

The class follows **みんなの日本語 初級1 (Minna no Nihongo Elementary 1)**, but
loosely — the teacher covers conversational grammar ahead of the book's order.
Use the book's lesson numbers for grouping vocabulary, not for pacing.

## Writing style for the brain files

Keep the tables sorted by level ascending (weakest first) — the stuff that needs
work should be at the top of the file where it's visible.

Use plain markdown tables. No code fences around them. They get edited constantly,
so keep rows on one line and don't pretty-align columns — alignment breaks on
every edit and creates noisy diffs.

Romaji is the primary form in every table. Kana and kanji go in their own
columns where known, for later.

## Tone during tests

Be a real teacher, not a cheerleader. If an answer is wrong, say it's wrong and
explain why. If an answer is technically correct but unnatural, say so — that
distinction matters more than the score. Don't pad results with praise.

## The site

Two pages, both hers to read:

- `index.html` is every class note rearranged by topic instead of by date.
- `diary.html` is the koe nikki: one entry a day, newest month on a calendar.

### Every change ships, every time

**No change to either page is finished until it is live on the web.** This is not
an `/ingest` step; it applies to every edit, however small, and to both pages.
The sequence is always: edit, commit, push, publish the artifact, then *verify
the live URL with `curl` before saying it is done*. GitHub Pages takes a minute
or two to rebuild, so poll until the change actually appears rather than
assuming the push was enough. Never report a change as live on the strength of
a successful push.

It is served from two places, and both need updating:

1. **GitHub Pages, the canonical one.** https://ramyashreeshetty.github.io/jp-notes/
   Commit and push to `main` and the site rebuilds in a couple of minutes.
2. **A Claude artifact mirror.** https://claude.ai/artifact/LrN9xnZ5KvASCDaVqyWhV9
   Always pass that URL as `url` when publishing, so the link stays stable.

The two need slightly different files. `index.html` is a complete document with
its own doctype, charset and viewport, because Pages serves it raw. The artifact
publisher supplies its own head, so publish a stripped copy to the artifact:
take everything from `<title>` to just before `</head>`, then the contents of
`<body>`, write that to a scratch file and publish that path with the URL above.

`diary.html` rides along on the artifact as a published file, complete document
and all, so the Diary link in the top bar works there too. So do the recordings
in `audio/`. Pass them in `files` on the same publish, or the artifact copy ends
up with a dead link while Pages is fine.

Never drop the charset from `index.html`. Without it every kana and kanji on the
page renders as mojibake.

### The diary page

One `<section>` per day, carrying `data-date="YYYY-MM-DD"`. The calendar builds
itself from those attributes, so a new entry needs nothing else to appear on it.

Keep an entry to four things and no more: the date heading, the player, the
whole entry in Japanese, the whole thing in English. No per-sentence pairing, no
corrections table, no vocabulary grid, no counts, no section intro. Corrections
belong in `log/mistakes.md`, which is where `/test` reads them from. She stripped
all of that out once; do not put it back.

Recordings go in `audio/YYYY-MM-DD.mp3` with `preload="none"` on the player. The
repo is public, so the audio is public: she chose that knowingly on 20 Sep 2026.

Conventions inside the textbook:

- Romaji is primary. Kana and kanji live in `<div class="jp-s">` elements which
  are hidden until the reader flips the script toggle. Always fill them in when
  you know them, even now — that's the head start for the reading phase.
- Sentences she built herself in class get `class="mine"`, which renders them in
  vermilion. Teacher examples stay plain. Keep that distinction honest; it is
  the clearest record of what she can actually produce.
- Correct the teacher's romaji inconsistencies silently, but when the notes
  contain an outright error (a wrong word, not a spelling), fix it and add a
  `.call.warn` box naming the correction.

### House style for the textbook

These are corrections Ramya made directly. Hold to them.

- **No em dashes anywhere.** Use a colon, a comma, a full stop or brackets.
- **No narration.** Do not write "from your 24 June class", "your teacher's
  example", "this was the best thing in", or anything else that talks about the
  lessons instead of the language. The book is a reference, not a diary.
- **No instructions to the reader** scattered through the page. No "tap this",
  no "worth memorising", no "say these aloud until". State the rule and stop.
- Section intros are one or two factual sentences about the grammar, or absent.
- Callouts are for a rule, a trap or an exception. If a callout does not teach
  something, delete it rather than rewrite it.
- Sections are numbered and separated by a rule. Keep the numbering matching the
  contents list.

### The repository

The folder is a git repo pushed to https://github.com/ramyashreeshetty/jp-notes,
which is **public**. Ramya chose that knowingly, including the raw class notes
and the personal details in the example sentences, so do not quietly strip them.

Commits use a GitHub noreply address rather than her work email, since every
commit is publicly visible. Pushing needs the `ramyashreeshetty` account:
`gh auth switch --user ramyashreeshetty`, push, then switch back to
`ramyashreeradix`, which is the account she normally works under.

## Theme

Set once, do not drift from it when regenerating.

**Type.** Both faces are real Japanese families from Google Fonts, so the Latin
was drawn to sit beside kana.

- Headings, the masthead, section numbers, Japanese script: **Shippori Mincho**
- Body, romaji sentences, tables, UI: **Zen Kaku Gothic New**

Because headings and the kana/kanji share one family, flipping the script toggle
reads as the same book rather than a second typeface arriving.

**Colour.** Named traditional Japanese colours, used as tokens:

| Token | Colour | Role |
|---|---|---|
| `--washi` | kinari, undyed cloth | page ground |
| `--sumi` | sumi, ink | text |
| `--ai` | ai, indigo | headings, links, Japanese script, callouts |
| `--shu` | shu, vermilion seal | the masthead hanko only |
| `--mine-bg` | faint warm tint | the sentences she wrote herself |

Her own sentences get a barely-there warm tint and a 2px edge at about 30%
vermilion, with the word "yours" in muted italic. Full-strength vermilion was
too distracting across a hundred lines, so it now appears exactly once, on the
masthead seal. Do not reintroduce it to the lines.

**Ornament.** Three Japanese elements, and no more than three:

- A **seigaiha** wave band between every section, with about 58px of air each
  side. This is what separates sections, so keep the spacing generous.
- The section number as a **hanko**, a bordered square holding a kanji numeral
  (`counter(sec, cjk-ideographic)`). The contents list keeps arabic numerals for
  scanning; the kanji in the sections doubles as passive number practice.
- One **vermilion seal** reading 学 in the masthead.

**Other.** Body 17px at 1.62 line height. Square corners, not rounded. A faint
SVG paper grain on the body background at 3.5% opacity. Every colour is defined
on bare `:root` first, then redefined for dark mode, so the toggle works in both
directions.
