# AI Guidelines — Multi-Category AI Prompt & Instruction Repository

A collection of reusable, portable instruction packs for AI agents. Each top-level directory is a self-contained **category** — a complete set of prompts and procedures for a specific domain.

## Categories

| Category | Description | Docs |
|----------|-------------|------|
| `it-support/` | Role-based instructions for AI coding agents, with local task context management | [docs/it-support.md](docs/it-support.md) |

## Quick Start

```bash
git clone {REPO_URL} && ./ai-guidelines/bin/install.sh it-support ./.ai
```

## Install

The install script copies a category's contents into your target directory:

```bash
bin/install.sh <category> <target>
```

**Arguments:**
- `category` — name of the category directory (e.g., `it-support`)
- `target` — destination directory (created if it doesn't exist)

**Examples:**
```bash
bin/install.sh it-support ./.ai              # conventional .ai/ dir
bin/install.sh it-support ./prompts          # custom directory name
bin/install.sh it-support ../my-project/.ai  # relative path to another project
```

The script copies the category's subdirectories directly into the target. Running it again upgrades the files while preserving your `prd/prd.md` and local `wiki/tasks/` context entries.

## Task Wiki and Context Management

The `it-support` category includes a local-only task wiki for agent context exchange:

- `wiki/tasks/{PROJECT_KEY}-{N}/summary.md` — compact task state
- `wiki/tasks/{PROJECT_KEY}-{N}/handoff.md` — role-to-role handoff notes
- `wiki/tasks/{PROJECT_KEY}-{N}/observations.md` — important task events
- `wiki/tasks/{PROJECT_KEY}-{N}/reflection.md` — compressed conclusions
- `wiki/tasks/{PROJECT_KEY}-{N}/heartbeat.md` — current checkpoint, blockers, and next action

Task wiki entries are operational memory and should stay local. The init instructions add `.ai/wiki/tasks/` to `.gitignore`, and the installer preserves existing task context during upgrades.

Commit reusable procedure and templates to GitHub. Keep session memory, heartbeat, observations, handoffs, task status, and deployment-specific details local-only.

Before ending any task, agents must perform a local context dump even if the user does not explicitly ask for it. The dump updates `wiki/tasks/{TASK_KEY}/summary.md`, `heartbeat.md`, `handoff.md`, and `observations.md`; it also updates `reflection.md` when a meaningful phase completes or context needs compression. If no task key is known, agents create or reuse a local key such as `wiki/tasks/{PROJECT_KEY}-context-snapshot/`.

## Repository Structure

```
ai-guidelines/
├── it-support/          # Category: AI coding agent instructions
├── docs/                # Category documentation
├── bin/
│   └── install.sh       # Category installer
├── CHANGELOG.md
└── README.md
```

## Attribution

This repository is a fork of the original project created by Jurand Antoś:
https://github.com/jurand-antos/ai-guidelines

The original work is licensed under the MIT License. Copyright and license
notices are preserved in the LICENSE file.

Modifications in this fork are maintained by Piotr Matysek / matysxx.

## License

MIT License — see LICENSE file for details.
