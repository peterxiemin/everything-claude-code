# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Everything Claude Code is a plugin ecosystem for Claude Code (Anthropic's CLI). It provides agents, skills, commands, rules, hooks, and MCP server configurations that extend Claude Code's capabilities. All scripts are written in Node.js for cross-platform compatibility (macOS, Linux, Windows).

## Commands

### Testing

```bash
node tests/run-all.js
```

Set `CLAUDE_CODE_PACKAGE_MANAGER` env var to test with a specific package manager (npm, pnpm, yarn, bun).

### Linting

```bash
# JavaScript
npx eslint scripts/**/*.js tests/**/*.js

# Markdown
npx markdownlint "agents/**/*.md" "skills/**/*.md" "commands/**/*.md" "rules/**/*.md"
```

### Validation

Each component type has a dedicated validator:

```bash
node scripts/ci/validate-agents.js
node scripts/ci/validate-hooks.js
node scripts/ci/validate-commands.js
node scripts/ci/validate-skills.js
node scripts/ci/validate-rules.js
```

### Install Dependencies

```bash
npm ci
```

## Architecture

### Component Types

The project is organized around six component types, each in its own top-level directory:

- **`agents/`** - Specialized subagents (markdown files with YAML frontmatter defining `name`, `description`, `tools`, and `model`)
- **`skills/`** - Workflow definitions and domain knowledge (single `.md` files or directories with multiple files)
- **`commands/`** - Slash commands (markdown files with `description` frontmatter)
- **`rules/`** - Always-follow guidelines loaded automatically
- **`hooks/`** - Automation triggers defined in `hooks.json` (PreToolUse, PostToolUse, PreCompact, SessionStart, SessionEnd, Stop)
- **`mcp-configs/`** - MCP server configurations in `mcp-servers.json`

### Supporting Directories

- **`scripts/lib/`** - Shared utilities (`utils.js` for file/path/system helpers, `package-manager.js` for PM detection)
- **`scripts/hooks/`** - Hook handler scripts (session lifecycle, compaction, evaluation)
- **`scripts/ci/`** - CI validation scripts for each component type
- **`contexts/`** - Dynamic system prompts for different modes (dev, review, research)
- **`schemas/`** - JSON schemas for plugin, hooks, and package-manager config validation
- **`.claude-plugin/`** - Plugin manifest (`plugin.json`) and marketplace metadata

### Package Manager Detection

Priority chain: `CLAUDE_PACKAGE_MANAGER` env var > project `.claude/package-manager.json` > `package.json` `packageManager` field > lock file detection > global `~/.claude/package-manager.json` > first available.

### Continuous Learning v2

An instinct-based learning system: hooks capture session activity, an observer agent detects patterns, creates atomic instincts with confidence scoring, and `/evolve` clusters instincts into reusable skills.

## Contributing New Components

- Place files in the appropriate directory (`agents/`, `skills/`, `commands/`, `rules/`, `hooks/`, `mcp-configs/`)
- Agents require YAML frontmatter: `name`, `description`, `tools`, `model`
- Commands require YAML frontmatter: `description`
- Use lowercase-with-hyphens filenames: `python-reviewer.md`, `tdd-workflow.md`
- Run the relevant validator script before submitting
- Don't manually add a `hooks` field to `.claude-plugin/plugin.json` -- hooks are auto-loaded by convention (requires Claude Code CLI v2.1.0+)

## CI

GitHub Actions CI runs on push/PR to main with a matrix of OS (ubuntu, windows, macos) x Node (18, 20, 22) x package manager (npm, pnpm, yarn, bun). Pipeline stages: test, validate components, security audit, lint (ESLint + markdownlint).
