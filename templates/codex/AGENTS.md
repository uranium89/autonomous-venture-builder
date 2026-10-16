{{include shared/RULES.md}}

## Orchestration (Codex)
- The roles are custom agents in `.codex/agents/*.toml`: `venture-scout`, `market-analyst`, `finance-analyst`, `skeptic`.
- The main thread is the orchestrator. Spawn ONE subagent per step, following the Orchestrator rules above.
- Subagents inherit the parent's sandbox, approval policy and web search setting. Discover needs live web search; if it is off, stop and tell the stakeholder how to turn it on (see `studio/README.md`).
