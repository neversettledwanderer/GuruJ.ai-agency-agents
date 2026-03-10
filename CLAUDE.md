# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A collection of markdown-based AI agent definitions ("specialists") that can be installed into various AI coding tools (Claude Code, GitHub Copilot, Cursor, Gemini CLI, Aider, Windsurf, etc.). There is no application code — the "product" is the agent `.md` files themselves.

## Common Commands

```bash
# Validate agent files (runs frontmatter + structure checks)
bash scripts/lint-agents.sh path/to/agent.md
# or validate all agents in a category
bash scripts/lint-agents.sh design/*.md

# Convert agents to all supported tool formats (outputs to integrations/)
bash scripts/convert.sh

# Install agents to local tool configs (interactive)
bash scripts/install.sh
```

CI runs `lint-agents.sh` on changed agent files for every PR (`.github/workflows/lint-agents.yml`).

## Agent File Structure

Every agent lives in a category directory (e.g. `engineering/`, `design/`, `game-development/unity/`) and must follow this exact format:

```markdown
---
name: Agent Name
description: One-line description of specialty
color: colorname or "#hexcode"
---

# Agent Name

## 🧠 Your Identity & Memory
## 🎯 Your Core Mission
## 🚨 Critical Rules You Must Follow
## 📋 Your Technical Deliverables
## 🔄 Your Workflow Process
## 💭 Your Communication Style
## 🔄 Learning & Memory
## 🎯 Your Success Metrics
## 🚀 Advanced Capabilities
```

Frontmatter (`name`, `description`, `color`) is required — `lint-agents.sh` will fail without it. The section headers are recommended but only produce warnings if missing.

Files are named `{category}-{slug}.md` (e.g., `engineering-frontend-developer.md`). Subdirectories are allowed (e.g., `game-development/unity/unity-architect.md`).

## Agent Categories

| Directory | Focus |
|---|---|
| `design/` | UI/UX, visual design systems |
| `engineering/` | Software development specialists |
| `game-development/` | Game engine specialists (Unity, Unreal, Godot, Roblox) |
| `marketing/` | Growth and marketing |
| `product/` | Product management |
| `project-management/` | PM and coordination |
| `testing/` | QA and testing |
| `support/` | Operations and support |
| `spatial-computing/` | AR/VR/XR |
| `specialized/` | Unique specialists |
| `strategy/` | Strategic specialists |

## Integration Architecture

`scripts/convert.sh` reads all agent `.md` files and outputs tool-specific formats into `integrations/`:

- **Claude Code / GitHub Copilot**: `.md` files copied as-is
- **Cursor**: `.mdc` rule files in `.cursor/rules/`
- **Antigravity / Gemini CLI**: `SKILL.md` + manifest in skill subdirectory
- **OpenCode**: `.md` files in `.opencode/agent/`
- **Aider**: single `CONVENTIONS.md` concatenating all agents
- **Windsurf**: single `.windsurfrules` file

## Contribution Guidelines

From `CONTRIBUTING.md`:

- Each agent must have strong personality, clear deliverables, measurable success metrics, proven workflows, and concrete examples (code, templates, documents) — not generic advice.
- The `description` frontmatter field is used as the agent's trigger phrase in Claude Code's `--agent` selection. Make it specific and action-oriented.
- Use the PR template (`.github/PULL_REQUEST_TEMPLATE.md`) when submitting new agents.
- Run `lint-agents.sh` locally before opening a PR.
