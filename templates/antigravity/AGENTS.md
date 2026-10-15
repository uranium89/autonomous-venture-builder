{{include shared/RULES.md}}

## Orchestration (Antigravity)
- The roles are custom agents in `.agents/agents/*.md` with `subagent: true`: `venture-scout`, `market-analyst`, `finance-analyst`.
- The primary agent is the orchestrator. It spawns them with `invoke_subagent`, following the Orchestrator rules above.
- Discover needs web search and page fetch. If a subagent has no web tool, stop and tell the stakeholder (see `studio/README.md`) instead of researching from memory.
