# CLAUDE.md: louisli/debater-ko

A process for AIs to debate ideas in a GitHub repo: the rules and the config
format, with the engine to come. Its tickets are GitHub issues here, worked by
the engineer and reviewer from **louisli/earth-616-jarvis** (Jarvis), where
this repo is the profile `debater`.

## General rules (same in every repo)
1. Read the rules file below before you start work; a route may send you to
   just one part of it. If it and this file disagree, stop and ask Lou (in an
   unattended run: report it and stop).
2. Name the repo, branch and file path in everything you report.
3. No secrets in files, commits, PRs or posts. Say where a secret is kept.
4. Lasting instructions live in the repo. When Lou gives a lasting rule in a
   chat, write it into the rules file.
5. If no route below matches your task, ask Lou (in an unattended run: report
   it and stop). Don't guess.
6. Run git and gh as one command per call. No && or ;, and don't start with
   cd. Use git -C <dir> ... instead.

## Rules file
Read `docs/CLAUDE_debater.md` first (the profile's `layout.rulesFile` in
Jarvis).

## Routes: read only the file that matches your task
| If your task is… | Read |
| --- | --- |
| an engineer or reviewer run (scheduled or by hand) | louisli/earth-616-jarvis `CLAUDE.md`, with the profile `debater` |
| creating or changing tickets (GitHub issues) | louisli/earth-616-jarvis `core/standard/README.md` |
| a new idea for this repo | `local/ideas/README.md` |
| the debate process itself | `docs/RULES.md` |
| how it's built, or the config pattern | `docs/DESIGN.md`, then `src/config/README.md` |
| a change to the process | `docs/CONTRIBUTING.md` |
| anything else | ask Lou |
