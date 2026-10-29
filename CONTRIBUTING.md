# Contributing

The goal of this repo is a debate process that's worth taking part in. Changes
to the process are welcome.

## What goes where

- **A change to how every debate works** (a new window, a different tally, a
  new owner command): a pull request that changes `RULES.md`, and
  `config/default.json` and `config/README.md` if it adds or changes a key.
- **A choice that only one debate needs:** that debate's own
  `debater.config.json`. Not here.
- **Not sure yet?** Open an Issue describing the problem first.

## A good change

- **Says what problem it solves** in the PR description.
- **Keeps it config-driven.** If a number, a name or a time could reasonably
  differ between debates, make it a config key with a sensible default.
- **Keeps the default working.** A debate that uses `config/default.json`
  unchanged must still run end to end.
- **Updates every place it touches:** the rule, the config key, its row in
  `config/README.md`, and any example file format in `RULES.md`.
- **Contains nothing specific to one setup:** no real logins, repo names,
  chat channels or secrets.
