# AI Venture Studio for Codex

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/codex/`, the parent of this `studio/` folder), including the hidden `.codex/`, into it.
2. Start Codex in the folder; the custom agents in `.codex/agents/` are picked up automatically.

## Prompts
**1. Studio setup** (once):
```
Set up the studio as defined in AGENTS.md.
Invoke the venture-scout as a subagent to run the thesis interview.
Ask me the questions and wait for my answers, then show me studio/THESIS.md.
```

**2. Discover run** (find new ideas):
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
- All three agents use `model_reasoning_effort = "high"` and inherit the session's model. Pin one with `model = "..."` in the agent's TOML file.
- Subagents inherit the parent's sandbox and approval policy. Write zones are enforced only by the instructions.
