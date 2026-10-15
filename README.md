# Autonomous Venture Builder

An AI venture studio that finds startup ideas, researches them against public evidence, and asks you to decide Go, Park or Kill before any money or build effort is spent. Ventures that pass are later built by the [AI Scrum Team](https://github.com/uranium89/ai-scrum-team).

```
DISCOVER -> VALIDATE -> BUILD -> LAUNCH -> MEASURE -> (KILL | PIVOT | SCALE)
```

| Stage | What happens | Status |
|---|---|---|
| Discover | venture-scout sources and screens ideas; market-analyst and finance-analyst research each shortlisted one with cited sources; you get a scorecard and a Go / Park / Kill brief | **Available** |
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

Then open your tool there and follow `studio/README.md`. The Claude Code layout:

```
my-studio/
├── CLAUDE.md / AGENTS.md     rules and orchestration (tool-specific)
├── .claude/agents/ ...       venture-scout, market-analyst, finance-analyst (tool-specific)
└── studio/
    ├── README.md             prompts and how-to
    ├── THESIS.md             what the studio looks for (you own it)
    ├── PORTFOLIO.md          every venture and its status
    ├── ideas/IDEAS.md        sourced ideas and screening results
    ├── decisions/            Go / Park / Kill briefs waiting for you
    └── ventures/V-NNN-slug/  idea.md, market.md, finance.md, thesis.md
```

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
