# Autonomous Venture Builder

An AI venture studio that finds startup ideas, researches them against public evidence, and asks you to decide Go, Park or Kill before any money or build effort is spent. Ventures that pass are later built by the [AI Scrum Team](https://github.com/uranium89/ai-scrum-team).

```
DISCOVER -> VALIDATE -> BUILD -> LAUNCH -> MEASURE -> (KILL | PIVOT | SCALE)
```

| Stage | What happens | Status |
|---|---|---|
| Discover | venture-scout sources and screens ideas; market-analyst and finance-analyst research each shortlisted one with cited sources; skeptic checks the sources and re-scores it; you get a scorecard and a Go / Park / Kill brief | **Available** |
| Validate | Cheap experiments with real people against kill thresholds set in advance | Planned |
| Build | A validated venture gets its own repository with the AI Scrum Team | Planned |
| Launch, Measure | Release, channels, metrics, Kill / Pivot / Scale decisions | Planned |

## Use the template

Pick your tool, then copy the contents of its `dist/` folder, including hidden folders, into an empty studio folder (keep it separate from product repositories). Each one has its own `studio/README.md` with the setup, Discover, check and answer prompts.

| Tool | Copy from | Rules file | Agents | Web research |
|---|---|---|---|---|
| Claude Code | `dist/claude/` | `CLAUDE.md` | `.claude/agents/*.md` | built in |
| OpenAI Codex | `dist/codex/` | `AGENTS.md` | `.codex/agents/*.toml` | start with live web search on (see its README) |
| Cursor | `dist/cursor/` | `.cursor/rules/ai-studio.mdc` | `.cursor/agents/*.md` | built in |
| OpenCode | `dist/opencode/` | `AGENTS.md` | `.opencode/agents/*.md` | `webfetch` and `websearch` allowed per agent |
| Google Antigravity | `dist/antigravity/` | `AGENTS.md` | `.agents/agents/*.md` | experimental: web tool names to add yourself |

```sh
mkdir ~/my-studio && cp -R dist/claude/. ~/my-studio/ && cd ~/my-studio && git init
```

Then open your tool there and run the Kickoff prompt below. The Claude Code layout:

```
my-studio/
├── CLAUDE.md / AGENTS.md     rules and orchestration (tool-specific)
├── .claude/agents/ ...       venture-scout, market-analyst, finance-analyst, skeptic (tool-specific)
└── studio/
    ├── README.md             prompts and how-to
    ├── THESIS.md             what the studio looks for (you own it)
    ├── PORTFOLIO.md          every venture and its status
    ├── ideas/IDEAS.md        sourced ideas and screening results
    ├── decisions/            Go / Park / Kill briefs waiting for you
    └── ventures/V-NNN-slug/  idea.md, market.md, finance.md, thesis.md
```

## Quick start

After copying, open your tool in the studio folder and paste the prompts below. The examples are for Claude Code; for other tools, swap the rules file and the "invoke" line using the table. Full instructions per tool: [Claude Code](dist/claude/studio/README.md), [Codex](dist/codex/studio/README.md), [Cursor](dist/cursor/studio/README.md), [OpenCode](dist/opencode/studio/README.md), [Antigravity](dist/antigravity/studio/README.md).

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

**3. Check one idea**:
```
check: [YOUR IDEA, in your own words]
```

**4. Answer a brief**:
```
DEC-NNN: A
```

| Tool | Rules file | Invoke line |
|---|---|---|
| Claude Code | `CLAUDE.md` | Invoke each agent as a subagent, one at a time. |
| OpenAI Codex | `AGENTS.md` | Spawn a subagent for each step, one at a time, and wait for it to finish. |
| Cursor | `.cursor/rules/ai-studio.mdc` | Invoke each agent with its slash command (/venture-scout, /market-analyst, /finance-analyst, /skeptic), one at a time. |
| OpenCode | `AGENTS.md` | Invoke each subagent via the Task tool, one at a time. |
| Google Antigravity | `AGENTS.md` | Use invoke_subagent for each step, one at a time. |

As the stakeholder, you only answer the thesis interview, choose Go / Park / Kill in gate briefs (`studio/decisions/`), and read the portfolio and each venture's `thesis.md`.

## Repository layout

```
shared/       content common to every tool (edit here first)
  RULES.md      lifecycle, roles, hard limits, Discover workflow, scorecard, gate rule, file formats
  agents/       agent prompts (description + body)
  docs/         README sections included in every tool's README
  studio/       the studio/ skeleton
templates/    tool-specific parts only (front matter, rules-file wrapper, README)
dist/         generated, ready-to-copy templates (do not edit by hand)
scripts/build.py
```

## Edit a template

1. Change shared content in `shared/`, and tool-specific content in `templates/<tool>/`.
2. Run `python3 scripts/build.py` to regenerate `dist/`.
3. Run `python3 scripts/build.py --check` to confirm `dist/` is up to date.

Templates use the same directives as ai-scrum-team: `{{include PATH}}`, `{{body PATH}}`, `{{description PATH}}`. To add a role, add `shared/agents/<role>.md`, a wrapper in every `templates/<tool>/` agents folder, and the role to `shared/RULES.md` and `shared/docs/WORKFLOW.md`.
