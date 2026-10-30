# docs/CLAUDE_debater.md

Rules for working in louisli/debater-ko. The root `CLAUDE.md` routes here;
read this first and follow links only when the task needs them. This file is
the profile's `layout.rulesFile` in Jarvis.

## Start here
- **Which file to read for your task:** the routes table in `CLAUDE.md`.
- **The engineer, the reviewer and how tickets work** live in Jarvis
  (louisli/earth-616-jarvis): `docs/CHARTER.md`, `core/agents/`,
  `core/standard/`. This repo is the profile `debater` there
  (`profiles/debater/profile.json`). Jarvis's rules win for that work.
- **What's where:** the folders set by Jarvis's `core/standard/layout.md` and
  this profile's `layout` block (`README.md`, "What's where"):
  - `docs/`: the process (`RULES.md`), how it's built (`DESIGN.md`), how to
    change it (`CONTRIBUTING.md`) and this file;
  - `src/`: the default config and its key reference (`config/`), the
    templates (`templates/`) and, later, the engine;
  - `local/`: `ideas/` (`layout.ideasDir`).

## Checks before any push
- `src/config/default.json` parses as JSON (this repo's `checks` in its
  Jarvis profile).

## Rules
- Keep it config-driven (`docs/DESIGN.md` section 3): a value that could
  differ between debates is a key in `src/config/default.json`, with a row in
  `src/config/README.md`.
- Keep it generic: no real logins, repo names, chat channels or secrets
  (`docs/CONTRIBUTING.md`).
- A change that's asked for directly still gets a ticket first: an issue
  here, with its record in Jarvis (`core/standard/README.md`, "Changes Louis
  asks for directly").
- Changes go through a PR that says `Closes #<n>`. Changes to `CLAUDE.md`
  and this file are merged by Louis by hand.
- New ideas for this repo go in `local/ideas/`; large ones go to the debate in
  louisli/earth-616-discussion. Bot-to-bot notes go there too, under
  `bot-conversation/<from>_<to>/`.
- No secrets in files, commits or PR text; say where a secret is kept.
