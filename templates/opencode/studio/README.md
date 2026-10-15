# AI Venture Studio for OpenCode

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/opencode/`, the parent of this `studio/` folder), including the hidden `.opencode/`, into it.
2. Start OpenCode in the folder; the subagents in `.opencode/agents/` are loaded automatically.

## Prompts
**1. Kickoff** (once per studio):
```
Kick off the venture studio. [OPTIONAL: what interests you, or an idea you already have, in your own words.]
Act as the orchestrator defined in AGENTS.md and run Studio Setup, then a first Discover run.
Invoke each subagent via the Task tool, one at a time.
Ask me the thesis interview questions and wait for my answers. Then run Discover and show me studio/THESIS.md, the portfolio and the gate briefs.
```

**2. Discover run** (later, to find more ideas):
```
Run Discover as defined in AGENTS.md.
Invoke each subagent via the Task tool, one at a time.
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

## OpenCode notes
- Agents use `anthropic/claude-opus-5-5`. Change `model:` in `.opencode/agents/*.md` to use another provider.
- Each agent allows `webfetch` and `websearch`, and only read-only shell commands. Depending on your OpenCode version and provider, `websearch` may need to be enabled separately; check the OpenCode docs if the agents report it missing.
- Permissions use the key-value format. Newer OpenCode versions also accept a list format; convert if yours requires it. Bash rules use last-match-wins.
