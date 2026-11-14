# AGENTS.md

Guidance for AI agents working in this repository.

## Project

SteamDeck Agent is an open-source tool that automates common Steam Deck
operations. The project is in early development, so keep the repository
public-ready at all times and prefer simple, reviewable changes.

## Repository rules

- Never commit secrets: API keys, tokens, passwords, SSH keys, cookies, or
  personal data.
- Keep local configuration in `.env`; `.env` must stay gitignored.
- Do not commit virtual environments, build output, caches, logs, or downloaded
  assets.
- Keep changes focused. Do not reformat or refactor unrelated code.
- Do not add a dependency without a clear need.
- Do not commit or push unless the user explicitly asks.
- Update `README.md` when user-facing behavior or setup changes.
- Write code, comments, commit messages, and documentation in English.
- Use small, focused commits with imperative messages, for example
  `Add battery status command`.
- When the tech stack is chosen, record its build, lint, and test commands in
  this file.

## Steam Deck safety

- Default to non-destructive operations.
- Destructive or system-modifying actions (writing outside the project,
  installing packages, restarting services, changing filesystems) must require
  explicit user confirmation.
- Explain what a command will do before running it on a device.

## Steam Deck device documentation

- Inspecting the device must be read-only: no `sudo`, no installs, no writes
  outside the repository, no service changes unless the user explicitly asks.
- Collect device state with the tracked method
  `scripts/collect-device-info.sh`, which writes a snapshot to the gitignored
  `_LLM_WIKI/device/` directory.
- Device state (installed games, plugins, modifications) is private and must
  never be committed. Keep the collection *method* tracked, the *results* local.
- When adding a new kind of device data, update the script and re-run it rather
  than hand-writing local snapshots.
- Distinguish system services from user services (`systemctl` vs
  `systemctl --user`) when reporting status.
- Re-collect and refresh the local device files when the device changes.

## Knowledge base

This repository follows Karpathy's LLM Wiki pattern. Read
`karpathy_llm_wiki.md` before doing knowledge-base work. The goal is to
accumulate durable project knowledge instead of re-deriving it in chat.

Layout:

```text
_LLM_WIKI/
  raw/       immutable source material; agents read but never modify
    assets/  locally stored images referenced by sources
  wiki/      agent-maintained markdown knowledge base
  device/    gitignored; private device state from the collection script
```

- `_LLM_WIKI/wiki/index.md` catalogs every wiki page with a link and a one-line
  summary.
- `_LLM_WIKI/wiki/log.md` is append-only. Each entry starts with
  `## [YYYY-MM-DD] <operation> | <title>`.

Rules:

- Never edit files in `_LLM_WIKI/raw/`. Add new sources there instead.
- The agent owns `_LLM_WIKI/wiki/`; humans read it.
- Ingest one source at a time unless asked to batch.
- After an ingest, update the index, all affected pages, and the log.
- File useful query answers back into the wiki as new pages.
- Run a lint pass on request: contradictions, stale claims, orphan pages,
  missing pages, and missing cross-references.
- Keep wiki pages connected with relative markdown links.

## Before finishing work

- Run available linters and tests, or state that none are configured.
- Check `git status` to confirm only intended files changed.
- Report what changed and what was verified.
