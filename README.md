# Xerus Agents

Agent marketplace for the Xerus AI workforce platform. Each agent is a self-contained definition that can be installed into any Xerus workspace.

## Structure

```
{category}/{slug}/
  agent.md       # Agent definition (frontmatter + personality/goals/guidelines)
  config.json    # Runtime config (slug, name, model, tools, autonomy)
```

Categories: `research`, `content`, `marketing`, `sales`, `data`, `support`, `multi-agent`

## Agent Format

Each agent is defined in `agent.md` with YAML frontmatter + markdown body:

```yaml
---
name: Agent Name
slug: agent-slug
description: One-line description
personality_type: researcher | creative | analyst | organizer | networker
ai_model: claude-sonnet-4-5-20250929
category: research | content | marketing | sales | data | support | multi-agent
tags: [tag1, tag2]
autonomy_level: supervised | semi_autonomous | autonomous
tools: [tool_app_slug_1, tool_app_slug_2]
skills: [skill1, skill2]
model_config:
  temperature: 0.5
  max_tokens: 4000
permissions:
  can_write_files: false
  can_send_emails: false
  can_create_tasks: false
---

## Identity
## Goals
## Guidelines
## Constraints
## Personality
```

### Required Fields

- **Frontmatter**: `name`, `slug`, `description`, `category`
- **Markdown**: `## Identity`, `## Goals`

### Install Flow

When a user installs an agent from the marketplace:

1. Agent files (`config.json`, `SOUL.md`) are copied to `agents/{slug}/` in the workspace
2. Slug/ID mapping is registered in the `agent_registry` DB table
3. Backend generates workspace files in `agents/{slug}/`:
   - `CLAUDE.md` (generated module instructions)
   - `STATUS.md`, `USER.md`, `RELATIONSHIPS.md`, `BOOTSTRAP.md`
   - `HEARTBEAT.md`, `OPERATING.md`
   - `.memory/agents/{slug}/working.md`, `expertise.md`
4. SDK subagent definition written to `.claude/agents/{slug}.md`

## config.json Format

Each agent also has a `config.json` with runtime configuration read by the backend agent runner:

```json
{
  "slug": "agent-slug",
  "name": "Agent Name",
  "description": "One-line description",
  "role": "researcher | creative | analyst | organizer | networker",
  "model": "claude-sonnet-4.5",
  "autonomy_level": "supervised | semi_autonomous | autonomous",
  "domain": "",
  "primary_channel": "",
  "channels": [],
  "tools": ["tool_app_slug_1", "tool_app_slug_2"],
  "heartbeat_cron": ""
}
```

Fields mapped from `agent.md` frontmatter:
- `slug`, `name`, `description` — direct copy
- `role` — from `personality_type`
- `model` — from `ai_model`
- `autonomy_level`, `tools` — direct copy

Fields set at install time (empty in marketplace):
- `domain`, `primary_channel`, `channels`, `heartbeat_cron`

Fields that stay in `agent.md` only (not in config.json):
- `model_config` (temperature, top_p, max_tokens) — SDK-level config
- `permissions` — derived from autonomy_level at scaffold time
- `tags`, `category` — marketplace metadata
- `skills` — discovered from `.claude/skills/`

## Adding Agents

1. Create `{category}/{slug}/agent.md` and `{category}/{slug}/config.json`
2. Follow the formats above
3. Submit a PR

## Usage in Workspace

This repo is referenced as a git submodule in `xerus-workspace` at `marketplace/agents/`. During workspace scaffold, the contents are available for browsing and installing.

## Related Repos

- [xerus-workspace](https://github.com/xerus-ai/xerus-workspace) - Workspace scaffold template
- [xerus-skills](https://github.com/xerus-ai/xerus-skills) - Skill marketplace
