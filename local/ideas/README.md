# Local ideas

Drop a rough idea for debater-ko here: one Markdown file per idea, any name
(for example `2026-11-02-tally-ties.md`), in plain words. Say what you want
and, if you know, how to tell it's done.

Jarvis's reviewer, in spec mode, picks each note up (louisli/earth-616-jarvis
`core/agents/reviewer/README.md`, "Spec mode"). This folder is the
`layout.ideasDir` in the `debater` profile there, so Jarvis's `<ideasDir>/`
means here:

- **Small or mid-size** (at most 3 issues, each one engineer run, no API,
  schema, workflow, security or cross-repo change): it writes the specs as
  `status:todo` issues here, with a record each in Jarvis's register, and
  moves the note to `archive/`.
- **Large:** it parks the note in louisli/earth-616-discussion's `inbox/`
  for debate, and moves the note to `archive/`. Lou promotes it there in a
  live session.
- **Unclear:** it moves the note to `needs-info/` with its question on the
  first line. Answer it there, delete that line and move the note back here.

Never edit a note in `archive/`. This README is never picked up.
