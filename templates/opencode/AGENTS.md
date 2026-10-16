{{include shared/RULES.md}}

## Orchestration (OpenCode)
- The roles are subagents in `.opencode/agents/*.md`: `venture-scout`, `market-analyst`, `finance-analyst`, `skeptic`.
- The primary agent (Build) is the orchestrator. It invokes them via the Task tool, following the Orchestrator rules above; the stakeholder can also @mention them.
- Each subagent has `webfetch` and `websearch` allowed. If web search is unavailable in this OpenCode setup, stop and tell the stakeholder (see `studio/README.md`).
