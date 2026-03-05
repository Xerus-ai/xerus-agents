# Xerus Agents

Agent marketplace for the Xerus AI workforce platform. Each agent is a self-contained definition that can be installed into any Xerus workspace.

## Structure

```
{category}/{slug}/agent.md
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
ai_model: gpt-4o | anthropic/claude-sonnet-4.5 | claude-3-5-sonnet-20241022
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

1. Frontmatter is imported into the `agents` + `agent_templates` DB tables
2. Markdown body becomes the `system_prompt` JSONB
3. Backend generates 12 workspace files in `agents/{slug}/`:
   - `config.json` (control surface)
   - `CLAUDE.md` (generated module instructions)
   - `SOUL.md`, `STATUS.md`, `USER.md`, `RELATIONSHIPS.md`, `BOOTSTRAP.md`
   - `system-prompt.md`, `HEARTBEAT.md`, `OPERATING.md`
   - `.memory/agents/{slug}/working.md`, `expertise.md`
4. SDK subagent definition written to `.claude/agents/{slug}.md`

## Adding Agents

1. Create `{category}/{slug}/agent.md`
2. Follow the format above
3. Submit a PR

## Usage in Workspace

This repo is referenced as a git submodule in `xerus-workspace` at `marketplace/agents/`. During workspace scaffold, the contents are available for browsing and installing.

## Related Repos

- [xerus-workspace](https://github.com/xerus-ai/xerus-workspace) - Workspace scaffold template
- [xerus-skills](https://github.com/xerus-ai/xerus-skills) - Skill marketplace
