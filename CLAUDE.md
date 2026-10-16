# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Templates for an AI venture studio (venture-scout, market-analyst, finance-analyst, skeptic) working for a non-technical stakeholder. Only the Discover stage is implemented; Validate, Build, Launch and Measure are planned, and Build will hand ventures to https://github.com/uranium89/ai-scrum-team. The workflow rules live in `shared/RULES.md`; this file is about maintaining the templates, not running the studio.

## Commands

- `python3 scripts/build.py`: regenerate `dist/` from `shared/` + `templates/`.
- `python3 scripts/build.py --check`: exit 1 if `dist/` is stale. Run it after every change.

## Architecture

Same layout as ai-scrum-team: `shared/` (rules, agent prompts, README sections, the `studio/` skeleton) is expanded into `templates/<tool>/` by `scripts/build.py`, producing `dist/<tool>/`. Never edit `dist/` by hand.

## Conventions

- All documentation, prompts, templates and studio documents are written in English.
- A role's write zone, model tier and duties must agree across `shared/RULES.md`, `shared/docs/WORKFLOW.md`, the agent prompt and every tool's agent wrapper.
- To add a stage: add its roles to `shared/agents/`, its workflow and file formats to `shared/RULES.md`, flip its row in the lifecycle table to Implemented, and update `shared/docs/WORKFLOW.md` and the README.
- Every tool's agents need web search and page fetch. Tool config formats (front matter, model IDs, tool and permission names) change often; check the tool's official docs before editing them. Unverified: Codex `--search` / `web_search = "live"`, OpenCode `websearch` permission, and Antigravity web tool names (not yet in its `tools` list).
- The stakeholder is non-technical. Briefs and summaries stay in business terms: money, time, risk, reversibility.
- Agents never spend money, contact real people or invent evidence. Keep those hard limits in every new stage until a stage explicitly needs an exception, and then gate it with a decision brief.
