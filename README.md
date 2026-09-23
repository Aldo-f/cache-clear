# cache-clear

Safe cache cleaner for any Linux system.

## Goal

Clear stale temporary data from common cache locations without breaking
active sessions or expensive-to-rebuild caches. Works on Raspberry Pi,
desktop, and server — no sudo required for normal operation.

## Features

- **Safe by default**: previews before deleting, asks for confirmation
- **Preserves important data**: keeps active JSON caches, session files
- **Swap dance**: automatically manages swap on low-memory systems to prevent OOM
- **Cross-platform**: works on Debian, Ubuntu, Arch, Raspberry Pi OS
- **Easy install**: one-line installer via curl pipe

## Install

```bash
curl -sL https://cdn.jsdelivr.net/gh/Aldo-f/cache-clear@main/cache-clear | bash
```

Or via GitHub raw:

```bash
curl -sL https://raw.githubusercontent.com/Aldo-f/cache-clear/main/cache-clear | bash
```

## Usage

```bash
# Preview what would be deleted
cache-clear --dry-run

# Delete without confirmation
cache-clear --force

# Remove the command
cache-clear --uninstall

# Show help
cache-clear --help
```

## What gets cleared

| Category | Locations |
|----------|-----------|
| Hermes Agent | `~/.hermes/cache/scratch/*` |
| Node.js | `~/.npm`, `~/.cache/yarn` |
| Python | `~/.cache/pip`, `~/.cache/uv` |
| Browsers | Chromium, Firefox caches |
| APT (sudo) | `/var/cache/apt/archives/*` |
| Journal (sudo) | `/var/log/journal/*` |

## What's preserved

- Root-level JSON files (`.mcp_schema_cache*`, config files)
- Active session files
- `clean.log` (this script's own log)

## Safe mode

When reclaiming >1 GB and the system has zram swap, cache-clear runs
a **swap dance**:

1. Creates a 4 GB temp swap file in `/tmp`
2. Swaps in the temp file
3. Swaps out zram0
4. Swaps in zram0 again
5. Removes the temp file

This prevents OOM when large caches are purged on memory-constrained
systems like the Raspberry Pi.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT
