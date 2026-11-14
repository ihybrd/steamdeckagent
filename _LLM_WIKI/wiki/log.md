# Wiki Log

Append-only chronological record. Each entry starts with
`## [YYYY-MM-DD] <operation> | <title>`.

## [2026-11-14] init | Knowledge base initialized

- Created `raw/` for immutable sources and `wiki/` for agent-maintained pages.
- Added `wiki/index.md` and `wiki/log.md`.

## [2026-11-14] refactor | Split device state from shared methodology

- Added `scripts/collect-device-info.sh` (tracked) as the reusable, read-only
  collection method.
- Moved the collected device inventory and its derived pages into the
  gitignored `_LLM_WIKI/device/` directory so local games and modifications are
  not shared.
- Added `.gitignore` entries for `.env` and `_LLM_WIKI/device/`.
- Cleared the tracked wiki index of private device references.
