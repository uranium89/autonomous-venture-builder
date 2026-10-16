# AI Venture Studio for Codex

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/codex/`, the parent of this `studio/` folder), including the hidden `.codex/`, into it.
2. Start Codex in the folder; the custom agents in `.codex/agents/` are picked up automatically.

## Prompts
**1. Kickoff** (once per studio):
```
Kick off the venture studio. [OPTIONAL: what interests you, or an idea you already have, in your own words.]
Act as the orchestrator defined in AGENTS.md and run Studio Setup, then a first Discover run.
Spawn a subagent for each step, one at a time, and wait for it to finish.
Ask me the thesis interview questions and wait for my answers. Then run Discover and show me studio/THESIS.md, the portfolio and the gate briefs.
```

**2. Discover run** (later, to find more ideas):
```
Run Discover as defined in AGENTS.md.
Spawn a subagent for each step, one at a time, and wait for it to finish.
Stop when every shortlisted venture has a gate brief, then show me the portfolio and the briefs.
```

**3. Check one idea** (you already have an idea):
```
check: [YOUR IDEA, in your own words]
```

**4. Answer a brief**:
```
DEC-NNN: A
```

{{include shared/docs/WORKFLOW.md}}

## Codex notes
- **Web search is required.** Start Codex with live web search, for example `codex --search`, or set `web_search = "live"` in `~/.codex/config.toml`. These option names come from community guides; check the official Codex config reference if they don't work.
- All four agents use `model_reasoning_effort = "high"` and inherit the session's model. Pin one with `model = "..."` in the agent's TOML file. If the venture-scout runs on Claude elsewhere, Codex is a good place to run the skeptic.
- Subagents inherit the parent's sandbox and approval policy. Write zones are enforced only by the instructions.
