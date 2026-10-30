# debater-ko

A process for AIs to debate ideas in a GitHub repo: they break ideas down,
review each other's work, vote, and rework until the result is buildable.

Everything that differs from one debate to the next (who takes part, when
they run, how votes are counted) is config. The process itself is the same
for everyone.

## How a debate works

1. **An idea comes in.** Someone parks it in `inbox/`. In a live session, the
   owner and an AI turn it into a **topic** with a few **seeds**, one theme
   each.
2. **Each cycle, every participant takes one item.** In the work window it
   writes one proposal as a tree: a concept, its branches, and at least 3
   atomic tasks (leaves).
3. **The others review.** In the review window, every participant votes on
   each task it didn't write: `yes`, `no`, or `maybe` with the changes it
   wants.
4. **A script counts the votes.** Every reviewer says yes → approved. Every
   reviewer says no → rejected. Anything else → back to its author for
   rework, a limited number of times, then blocked.
5. **Approved work is exported** as idea notes, ready for whoever builds it.

The owner can step in at any point with commands like `/approve`, `/reword`
or `/park`.

## What's where

| Folder | Holds |
| --- | --- |
| [`docs/`](docs/) | [`RULES.md`](docs/RULES.md), the process: roles, the cycle, file formats, the tally, runbooks. [`DESIGN.md`](docs/DESIGN.md), how it's built: the tech, Python and evals, the config pattern, boundaries, trust, and how Issues are used. [`CONTRIBUTING.md`](docs/CONTRIBUTING.md), how to propose a change to the process. |
| [`src/`](src/) | [`config/default.json`](src/config/default.json), the default config (three participants, four 2-hour cycles on run days); [`config/README.md`](src/config/README.md), every config key explained; and [`templates/`](src/templates/), templates for a topic README and a seed. The engine's code will go here too. |
| [`local/`](local/) | [`ideas/`](local/ideas/README.md), notes for new work on this repo |

At the root: this README, `CLAUDE.md` and `LICENSE`.

**For AI agents:** start at [`CLAUDE.md`](CLAUDE.md), a short router; the
rules are in [`docs/CLAUDE_debater.md`](docs/CLAUDE_debater.md).

## The default schedule

All times are in the configured time zone (`America/New_York` by default).

| Minutes into each cycle hour | What happens |
| --- | --- |
| :00–:25 | **Work:** each participant writes its proposal or reworks its tasks |
| :25 | Review sheets are built |
| :30–:45 | **Review:** each participant votes |
| :47 | Tally, then prep for the next cycle |

Cycles start at 06:00, 08:00, 10:00 and 12:00 on Tuesday, Thursday, Saturday
and Sunday. A nightly run at 22:30 decides whether tomorrow is on.

## Status

Early. This repo holds the rules and the config format; the orchestrator
script that runs them comes later.

## License

[MIT](LICENSE)
