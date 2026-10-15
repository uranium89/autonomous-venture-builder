# AI Venture Studio for Cursor

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/cursor/`, the parent of this `studio/` folder), including the hidden `.cursor/`, into it.
2. Open the folder in Cursor. The rules file applies automatically and the agents appear as `/venture-scout`, `/market-analyst`, `/finance-analyst`.

## Prompts
**1. Kickoff** (once per studio):
```
Kick off the venture studio. [OPTIONAL: what interests you, or an idea you already have, in your own words.]
Act as the orchestrator defined in .cursor/rules/ai-studio.mdc and run Studio Setup, then a first Discover run.
Invoke each agent with its slash command (/venture-scout, /market-analyst, /finance-analyst), one at a time.
Ask me the thesis interview questions and wait for my answers. Then run Discover and show me studio/THESIS.md, the portfolio and the gate briefs.
```

**2. Discover run** (later, to find more ideas):
```
Run Discover as defined in .cursor/rules/ai-studio.mdc.
Invoke each agent with its slash command (/venture-scout, /market-analyst, /finance-analyst), one at a time.
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

## Cursor notes
- Agents use `model: claude-opus-5[effort=high]`. Change the model ID in `.cursor/agents/*.md` if your Cursor plan lists it differently.
- The agents need Cursor's web search. Make sure web tools are enabled for agents in Cursor settings.
