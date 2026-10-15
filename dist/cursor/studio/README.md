# AI Venture Studio for Cursor

## Setup
1. Create an empty folder for your studio (not inside a product repository) and copy everything in the template folder (`dist/cursor/`, the parent of this `studio/` folder), including the hidden `.cursor/`, into it.
2. Open the folder in Cursor. The rules file applies automatically and the agents appear as `/venture-scout`, `/market-analyst`, `/finance-analyst`.

## Prompts
**1. Studio setup** (once):
```
Set up the studio as defined in .cursor/rules/ai-studio.mdc.
Invoke /venture-scout to run the thesis interview.
Ask me the questions and wait for my answers, then show me studio/THESIS.md.
```

**2. Discover run** (find new ideas):
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
Studio setup (once): thesis interview -> studio/THESIS.md
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

## Cursor notes
- Agents use `model: claude-opus-5[effort=high]`. Change the model ID in `.cursor/agents/*.md` if your Cursor plan lists it differently.
- The agents need Cursor's web search. Make sure web tools are enabled for agents in Cursor settings.
