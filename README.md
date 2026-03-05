# Xerus Agent Marketplace

Agent definitions for the Xerus AI workforce platform. Users browse and install agents into their workspace.

## Structure

```
platform/           10 pre-built agents (ship with starter workspace template)
community/          55+ community agents (browse and install from marketplace)
```

## Platform Agents

These ship pre-installed with the starter workspace template:

| Agent | Category | Purpose |
|-------|----------|---------|
| Content Writer | Marketing | Blog posts, social copy, newsletters, reports |
| Data Analyst | Engineering | SQL analysis, dashboards, reports, insights |
| Researcher | Strategy | Competitive analysis, market intel, deep-dives |
| Growth Strategist | Marketing | Growth experiments, funnels, conversion optimization |
| Social Strategist | Marketing | Social media strategy, content calendars, engagement |
| Project Manager | Project Management | Coordination, timelines, deliverable tracking |
| Backend Developer | Engineering | APIs, databases, server-side logic |
| Frontend Developer | Engineering | UI components, responsive design, accessibility |
| Code Reviewer | Engineering | Bug detection, security review, code quality |
| Designer | Design | UI design, wireframes, design systems |

## Community Agents

Sourced from [The Agency](https://github.com/msitarzewski/agency-agents) (MIT licensed) and community contributions. Organized by division:

- **Engineering** (7): Frontend, Backend, Mobile, AI, DevOps, Rapid Prototyper, Senior Developer
- **Design** (7): UI, UX Research, UX Architect, Brand, Visual Storyteller, Whimsy, Image Prompt
- **Marketing** (8): Growth, Content, Twitter, TikTok, Instagram, Reddit, App Store, Social Media
- **Product** (3): Sprint Prioritizer, Trend Researcher, Feedback Synthesizer
- **Project Management** (5): Studio Producer, Shepherd, Operations, Experiment Tracker, Senior PM
- **Testing** (7): Evidence Collector, Reality Checker, Test Analyzer, Performance, API, Tool Evaluator, Workflow
- **Support** (6): Support Responder, Analytics, Finance, Infrastructure, Legal, Executive Summary
- **Specialized** (7): Orchestrator, Data Analytics, LSP, Sales Data, Data Consolidation, Report Distribution, Identity Trust
- **Spatial Computing** (6): XR Interface, macOS Metal, XR Immersive, XR Cockpit, visionOS, Terminal Integration

## Installation

When a user installs an agent from the marketplace:

1. Copy `agent.md` to workspace `.claude/agents/{slug}.md` (SDK subagent definition)
2. Create `agents/{slug}/` folder in workspace with SOUL.md and config.json
3. Generate remaining soul files (STATUS.md, USER.md, RELATIONSHIPS.md, BOOTSTRAP.md)
4. Update `agents/index.json`

## Agent File Format

### Platform agents (full)
```
platform/{slug}/
  agent.md          YAML frontmatter + markdown (SDK .claude/agents/ format)
  SOUL.md           Personality, values, communication style
```

### Community agents (single file)
```
community/{category}/{name}.md    YAML frontmatter + full personality prompt
```

## Contributing

1. Create agent in the appropriate category
2. Include YAML frontmatter: `name`, `description`, `color`
3. Add identity, capabilities, working style, and communication patterns
4. Submit PR
