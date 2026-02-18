# Claude Settings

Personal Claude Code configuration for Technijian development workflows.

## Structure

```
.claude/
├── settings.json              # Global Claude Code permissions & hooks
├── gsd-file-manifest.json     # GSD file manifest
├── commands/
│   └── gsd/                   # GSD slash commands (52 commands)
├── hooks/
│   ├── gsd-check-update.js    # Auto-update check hook
│   └── gsd-statusline.js      # Status line hook
├── agents/                    # Custom agent definitions (21 agents)
│   ├── gsd-*.md               # GSD workflow agents
│   └── sdlc-*.md              # SDLC pipeline agents
├── scripts/
│   ├── gsd-runner.ps1         # GSD automated phase runner
│   └── gsd-runner-gemini.ps1  # GSD runner (Gemini variant)
├── get-shit-done/
│   ├── VERSION                # GSD version
│   ├── workflows/             # GSD workflow definitions (47 files)
│   ├── references/            # Reference documents
│   ├── templates/             # Templates
│   └── bin/                   # GSD binaries/scripts
└── plugins/
    ├── installed_plugins.json # Installed plugin registry
    ├── known_marketplaces.json
    └── marketplaces/          # Marketplace definitions
```

## What's NOT included

- `.credentials.json` — API keys/tokens
- `history.jsonl` — conversation history
- Runtime directories (`backups/`, `cache/`, `debug/`, `tasks/`, `todos/`, etc.)
- Project-specific state (`projects/`)

## Setup

To use on a new machine, copy the contents to `~/.claude/` after installing Claude Code.
