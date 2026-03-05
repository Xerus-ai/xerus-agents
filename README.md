# Xerus Agent Marketplace

Agent definitions for the Xerus AI workforce platform. Users browse and install agents into their workspace.

## Structure

Agents are organized by category:

```
engineering/        Backend, Frontend, DevOps, AI, Mobile, Code Review, Data Analysis
design/             UI, UX Research, UX Architect, Brand, Visual, Whimsy
marketing/          Content, Growth, Social, Twitter, TikTok, Instagram, Reddit, App Store
product/            Sprint Prioritizer, Trend Researcher, Feedback Synthesizer
project-management/ Studio Producer, Shepherd, Operations, Experiment Tracker, Senior PM
testing/            Evidence Collector, Reality Checker, Performance, API, Tool Evaluator
support/            Support Responder, Analytics, Finance, Infrastructure, Legal, Exec Summary
specialized/        Orchestrator, Data Analytics, LSP, Researcher, Sales Data
spatial-computing/  XR Interface, macOS Metal, visionOS, XR Immersive, Terminal
strategy/           Nexus Strategy
```

## Agent Formats

**Folder agents** have `agent.md` (SDK definition) + `SOUL.md` (personality):
```
engineering/backend-developer/
  agent.md       YAML frontmatter + markdown
  SOUL.md        Personality, values, communication style
```

**Single-file agents** have everything in one markdown file:
```
engineering/engineering-ai-engineer.md    YAML frontmatter + full personality prompt
```

Both formats work. Folder agents are richer (separate SOUL.md for the soul protocol). Single-file agents are simpler to contribute.

## Installation

When a user installs an agent from the marketplace:

1. Copy `agent.md` to workspace `.claude/agents/{slug}.md` (SDK subagent definition)
2. Create `agents/{slug}/` folder in workspace with SOUL.md and config
3. Generate remaining soul files (STATUS.md, USER.md, RELATIONSHIPS.md, BOOTSTRAP.md)
4. Update `agents/index.json`

## Contributing

1. Pick a category (or create a new one)
2. Add your agent as a folder (`{slug}/agent.md` + `SOUL.md`) or single file
3. Include YAML frontmatter: `name`, `description`, and optionally `slug`, `model`, `autonomy_level`, `category`
4. Submit PR

## Credits

Community agents sourced from [The Agency](https://github.com/msitarzewski/agency-agents) by [@msitarzewski](https://github.com/msitarzewski) (MIT licensed).
