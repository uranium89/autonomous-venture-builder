# AI Venture Studio for Claude Code

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/claude/`, the parent of this `studio/` folder), including the hidden `.claude/`, into it.
2. Claude Code loads `CLAUDE.md` and the subagents in `.claude/agents/` automatically. Run `/agents` to confirm all three are listed.

## Prompts
**1. Kickoff** (once per studio):
```
Kick off the venture studio. [OPTIONAL: what interests you, or an idea you already have, in your own words.]
Act as the orchestrator defined in CLAUDE.md and run Studio Setup, then a first Discover run.
Invoke each agent as a subagent, one at a time.
Ask me the thesis interview questions and wait for my answers. Then run Discover and show me studio/THESIS.md, the portfolio and the gate briefs.
```

**2. Discover run** (later, to find more ideas):
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

## The team

| Agent | Model | Job |
|---|---|---|
| venture-scout | strong | Interviews you about what the studio should look for, finds and screens ideas, writes a one-page thesis and scorecard for each venture, asks you Go / Park / Kill, keeps the portfolio |
| market-analyst | strong | Researches who has the problem, proof that it hurts, competitors and prices, market size, how to reach the first customers, and why the idea could fail, all with sources |
| finance-analyst | strong | Works out price, costs, margins, break-even and the numbers that would prove the idea wrong |

## What you do as the stakeholder

1. **Answer the thesis interview once**: industries, markets, budget, your time, your advantages. The answers go into `studio/THESIS.md`, which you can edit at any time.
2. **Answer gate briefs** (`studio/decisions/DEC-*.md`) with A (Go), B (Park) or C (Kill). Each brief gives the score, the money and time the next step needs, and the biggest reasons the idea could fail.
3. **Read the portfolio** (`studio/PORTFOLIO.md`) and each venture's `thesis.md`.

## How Discover runs

```
Kickoff (once): thesis interview -> studio/THESIS.md -> first Discover run
Discover run:
  venture-scout: source ideas -> screen -> shortlist
  for each shortlisted venture:
    market-analyst -> finance-analyst -> venture-scout thesis + scorecard -> gate brief
  You: Go / Park / Kill
```

A venture scores 1-5 on Pain, Willingness to pay, Reach, Gap, Buildability, Economics and Fit (35 points in total). Go needs 25 or more with no score of 1 and no hard fail. Any score above 3 needs a cited source. Every market report must list at least 3 reasons the idea could fail.

## Caveats

- Discover uses public desk research only. It can show that a problem exists and that people pay for it. It can't prove that people will pay *you*. That is what the Validate stage (planned) is for.
- Agents are told to cite sources and to label guesses as `ASSUMPTION`, but they can still misread a source. Open the sources behind any number that drives your decision.
- Web research is the main cost. One venture uses three strong-model agent runs with many searches.
- Write zones and hard limits are instructions to the model, not enforced by the tool.

## Claude Code notes
- All three agents use `model: opus`, because research and judgment are the whole job.
- Agents have every tool available. To restrict one, add a `tools:` list to its front matter.
- To run unattended (for example overnight), use a permission mode that skips prompts, inside git so you can undo. Agents never spend money or contact anyone, and gate briefs wait for you.
