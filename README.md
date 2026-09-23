# cache-clear

Safe cache cleaner for Hermes Agent. Clears stale temp data from `~/.hermes/cache` while preserving expensive-to-rebuild JSON caches and active session files.

## Install

```bash
curl -sL https://raw.githubusercontent.com/Aldo-f/cache-clear/main/cache-clear | bash
```

This installs `cache-clear` to `~/.local/bin/` and makes it available on your PATH.

## Usage

```bash
cache-clear              # Interactive (preview, then confirm)
cache-clear --dry-run    # Preview only, delete nothing
cache-clear --force      # Delete without confirmation
cache-clear --uninstall  # Remove the command
cache-clear --help       # Show help
```

## What it clears

- `scratch/` temp files (browser profiles, compile caches, snapshots, PTY sessions)
- `terminal-output/` logs
- `exec/` stdout captures
- `web/` cached page content
- `documents/`, `delegation/`, `browser-use/`, `blocked-scripts/`
- `screenshots/`, `images/`, `videos/`, `audio/`, `vision/`, `spillover/`

## What it preserves

- Root-level JSON caches (`*.json`, `.mcp_schema_cache*`)
- `.browser_use_default_notice`
- `clean.log`
- Active session sockets and PID files
