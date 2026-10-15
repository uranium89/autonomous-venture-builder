# AI Venture Studio for Claude Code

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/claude/`, the parent of this `studio/` folder), including the hidden `.claude/`, into it.
2. Claude Code loads `CLAUDE.md` and the subagents in `.claude/agents/` automatically. Run `/agents` to confirm all three are listed.

## Prompts
**1. Studio setup** (once):
```
Set up the studio as defined in CLAUDE.md.
Invoke the venture-scout as a subagent to run the thesis interview.
Ask me the questions and wait for my answers, then show me studio/THESIS.md.
```

**2. Discover run** (find new ideas):
```
Run Discover as defined in CLAUDE.md.
Invoke each agent as a subagent, one at a time.
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

## Claude Code notes
- All three agents use `model: opus`, because research and judgment are the whole job.
- Agents have every tool available. To restrict one, add a `tools:` list to its front matter.
- To run unattended (for example overnight), use a permission mode that skips prompts, inside git so you can undo. Agents never spend money or contact anyone, and gate briefs wait for you.
