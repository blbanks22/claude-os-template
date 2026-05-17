# Custom agents

Subagent definitions. Two generic agents are included to start: `pr-author` and `researcher`. Add more as workflows generate friction.

Each agent lives in its own `.md` file with YAML frontmatter:

```yaml
---
name: agent-name
description: When to use this agent (specific triggers, in third person)
tools: Bash, Read, Grep   # optional tool allowlist
model: sonnet              # optional model override
---

Agent system prompt body here.
```

See [Anthropic docs](https://docs.claude.com/en/docs/claude-code/sub-agents) for the full schema.
