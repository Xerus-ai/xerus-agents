# Xerus Agent Marketplace

Agent definitions for the Xerus AI workforce platform. Users browse and install agents into their workspace.

Adding agents is just `git add` + `git push`.

## Structure

Agents organized by category. Each category is a folder:

```
marketing/
  content-writer/                   Folder agent (agent.md + SOUL.md)
  marketing-reddit-community-builder.md   Single-file agent
```

## Agent Formats

**Folder agents** have `agent.md` (SDK definition) + `SOUL.md` (personality):
```
{category}/{slug}/
  agent.md       YAML frontmatter + markdown
  SOUL.md        Personality, values, communication style
```

**Single-file agents** have everything in one markdown file:
```
{category}/{name}.md    YAML frontmatter + full personality prompt
```

## Installation

When a user installs an agent from the marketplace:

1. Copy `agent.md` to workspace `.claude/agents/{slug}.md`
2. Create `agents/{slug}/` folder in workspace with SOUL.md and config
3. Generate remaining soul files (STATUS.md, USER.md, RELATIONSHIPS.md, BOOTSTRAP.md)
4. Update `agents/index.json`

## Contributing

1. Pick a category (or create a new one)
2. Add your agent as a folder or single file
3. Include YAML frontmatter: `name`, `description`
4. Submit PR
