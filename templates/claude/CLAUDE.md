# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

{{include shared/RULES.md}}

## Orchestration (Claude Code)
- The roles are subagents in `.claude/agents/*.md`: `venture-scout`, `market-analyst`, `finance-analyst`.
- The main session is the orchestrator. Invoke the agents with the Agent tool, following the Orchestrator rules above.
- Agents need web search and page fetch. If a permission prompt blocks them, allow `WebSearch` and `WebFetch` for this project.
- Agent front matter uses the alias `model: opus`, which resolves to the current model in that family.
