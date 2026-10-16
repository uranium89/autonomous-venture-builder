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

## The team

| Agent | Model | Job |
|---|---|---|
| venture-scout | strong | Interviews you about what the studio should look for, finds and screens ideas, writes a one-page thesis and scorecard for each venture, asks you Go / Park / Kill, keeps the portfolio |
| market-analyst | strong | Researches who has the problem, proof that it hurts, competitors and prices, market size, how to reach the first customers, and why the idea could fail, all with sources |
| finance-analyst | strong | Works out price, costs, margins, break-even and the numbers that would prove the idea wrong |
| skeptic | strong | Challenges every thesis before it reaches you: opens the key sources to check them, looks for evidence against the idea, and scores it independently |

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
    market-analyst -> finance-analyst -> venture-scout thesis + scorecard
    -> skeptic challenge (AGREE, or DISPUTE: scout may answer once) -> gate brief
  You: Go / Park / Kill
```

A venture scores 1-5 on Pain, Willingness to pay, Reach, Gap, Buildability, Economics and Fit (35 points in total). The final score of each dimension is the lower of the scout's and the skeptic's. Go needs a final total of 25 or more with no score of 1 and no hard fail. Any score above 3 needs a cited source. Every market report must list at least 3 reasons the idea could fail.

## Caveats

- Discover uses public desk research only. It can show that a problem exists and that people pay for it. It can't prove that people will pay *you*. That is what the Validate stage (planned) is for.
- Agents are told to cite sources and to label guesses as `ASSUMPTION`, but they can still misread a source. Open the sources behind any number that drives your decision.
- Web research is the main cost. One venture uses four or five strong-model agent runs with many searches.
- The skeptic works best on a model from a different vendor than the venture-scout. See the notes for your tool below.
- Write zones and hard limits are instructions to the model, not enforced by the tool.

## Codex notes
- **Web search is required.** Start Codex with live web search, for example `codex --search`, or set `web_search = "live"` in `~/.codex/config.toml`. These option names come from community guides; check the official Codex config reference if they don't work.
- All four agents use `model_reasoning_effort = "high"` and inherit the session's model. Pin one with `model = "..."` in the agent's TOML file. If the venture-scout runs on Claude elsewhere, Codex is a good place to run the skeptic.
- Subagents inherit the parent's sandbox and approval policy. Write zones are enforced only by the instructions.
