# AI Venture Studio for Google Antigravity

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/antigravity/`, the parent of this `studio/` folder), including the hidden `.agents/`, into it.
2. Open the folder in Antigravity; the custom agents in `.agents/agents/` are available to the primary agent.

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
Use invoke_subagent for each step, one at a time.
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

## Antigravity notes (experimental)
- **Web tools are not configured yet.** The agents' `tools` list holds the four documented file and command tools only, because the names of Antigravity's web search and page fetch tools could not be verified. Add them to `tools:` in `.agents/agents/*.md` from the Antigravity docs before a Discover run; otherwise the agents stop and report the gap.
- Agents use `model: pro` and run commands in the sandbox.
