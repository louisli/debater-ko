# Configuration

Everything that differs from one debate to the next lives in config, not in
[`RULES.md`](../../docs/RULES.md). The rules refer to config keys by their path, for
example `schedule.windows.work.end`.

## Files

| File | What it is |
| --- | --- |
| `src/config/default.json` | The shipped default. Generic names, no accounts, no secrets. |
| `debater.config.json` | Your override, in the repo that runs a debate. Only the keys you change. |

**How they combine:** start from `default.json`, then apply the override.
Objects merge key by key; arrays and plain values replace the default
outright (so an override's `participants` is the whole list).

**Never put secrets in either file.** Logins are public names, not
credentials. Tokens and webhook URLs stay in whatever secret store runs your
participants.

## Keys

### Top level

| Key | Default | Meaning |
| --- | --- | --- |
| `config_version` | `1` | Format version of this file. |
| `name` | `"default"` | A label for the setup, shown in logs. |
| `timezone` | `"America/New_York"` | IANA zone. Every time in the config and the rules is in this zone. |

### `participants`

The AIs (or people) that write proposals and vote. Each entry:

| Key | Meaning |
| --- | --- |
| `id` | Short lowercase name. Used in file names (`breakdown-<id>.md`), labels (`todo:<id>`) and comment tags (`[<id>]`). |
| `login` | Optional. The GitHub login it acts as. Several participants may share one login; they're told apart by `id`. |

The default has three: `bot-a`, `bot-b`, `bot-c`. The cycle works with any
number from 2 up; with 2, each task gets one reviewer.

### `owner`

| Key | Default | Meaning |
| --- | --- | --- |
| `owner.login` | `null` | The GitHub login whose commands the orchestrator executes (docs/RULES.md section 9). `null` means no owner commands are accepted. |

### `schedule`

| Key | Default | Meaning |
| --- | --- | --- |
| `run_days` | `Tue, Thu, Sat, Sun` | Days cycles run. Other days are off. |
| `cycle_hours` | `06, 08, 10, 12` | The hour each cycle starts. Cycles must be at least 1 hour apart. |
| `windows.work` | `0`–`25` | Minutes after the cycle starts when authors write. |
| `windows.sheets.at` | `25` | When the orchestrator builds the review sheets. |
| `windows.review` | `30`–`45` | When reviewers vote. |
| `windows.tally.at` | `47` | When the orchestrator counts votes and preps the next cycle. |
| `participant_wake_minutes` | `0, 15, 30` | When each participant checks for work: the work start, a retry, the review start. |
| `review_wait_until_minute` | `40` | At the review wake-up, how long to keep polling for a review sheet. |
| `orchestrator_minutes` | `25, 47` | When the orchestrator runs in each cycle. |
| `nightly.at` | `"22:30"` | The nightly run: writes tomorrow's day plan. |
| `nightly.prepares_first_cycle` | `true` | The nightly run also preps tomorrow's first cycle. |
| `quiet_hours` | `22:00`–`02:59` | Nothing debate-related starts in these hours, except the nightly run. |

**The window order is fixed:** work ends before sheets, sheets before review
starts, review ends before tally, and tally before the next cycle starts.
A config that breaks this order is invalid.

### `cycle`

| Key | Default | Meaning |
| --- | --- | --- |
| `new_items_per_cycle` | `"one_per_participant"` | How many new items a cycle takes on: one per participant, or a number. |
| `first_author_rotates` | `true` | The participant who gets the first item changes every cycle. |
| `reviewers` | `"all_but_author"` | Who reviews a task: every participant except its author. |

### `proposal`

| Key | Default | Meaning |
| --- | --- | --- |
| `min_leaves` | `3` | Fewer leaves and the proposal counts as missing. |
| `max_leaves` | `null` | `null` = no maximum. |
| `requires_concept` | `true` | A proposal with no `## Concept` counts as missing. |

### `votes`

| Key | Default | Meaning |
| --- | --- | --- |
| `options` | `yes, maybe, no` | The allowed votes. |
| `changes_required_for` | `maybe` | Votes that must say what has to change. |
| `author_counts_as` | `"yes"` | The author's own vote, which isn't asked for. |
| `missing_vote_counts_as` | `"mixed"` | A missing vote makes the result mixed, never a yes or a no. |

### `tally`

An ordered list of rules. The first that matches decides the task's next
state. The default:

| Rule | Outcome |
| --- | --- |
| every reviewer votes `yes` | `approved` |
| every reviewer votes `no` | `rejected` |
| otherwise | `more-review` |

### `limits`

| Key | Default | Meaning |
| --- | --- | --- |
| `reworks_per_task` | `2` | A task still in `more-review` after this many reworks becomes `blocked`. |
| `errors_per_role_per_item` | `3` | Errors or dead locks by one participant on one item before it goes to the owner. |
| `lock_timeout_minutes` | `30` | A lock with no heartbeat for this long is dead. |
| `heartbeat_minutes` | `10` | How often a working participant refreshes its lock. |

### `atomic_test`

The checks every leaf must pass (docs/RULES.md section 8). A list of sentences, so
a debate can make the bar stricter or looser.

### `owner_commands`

Which owner commands are enabled (docs/RULES.md section 9.2). Remove one to turn it
off.

### `audit` and `export`

| Key | Default | Meaning |
| --- | --- | --- |
| `audit.enabled` | `false` | Whether an auditor reviews approved and blocked tasks and exports them. Off: they wait in `approved` or `blocked`. |
| `audit.max_tasks_per_run` | `30` | Cap per auditor run. |
| `export.folder` | `"outbox/"` | Where exported idea notes are written. |

### `trust`

| Key | Default | Meaning |
| --- | --- | --- |
| `trust.verify_authors` | `false` | Also check that each participant file was committed by that participant's `login` (docs/DESIGN.md 5.4). Turn on only when every participant has its own login. |
