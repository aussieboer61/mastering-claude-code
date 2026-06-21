# Mastering Claude Code — A Project-Agnostic Practitioner's Guide

This guide is for intermediate users who have moved past first contact with Claude Code and want to build something more durable: a working environment that accumulates knowledge over time, enforces the rules that matter, runs work in the background, and does not make you re-explain yourself at the start of every session. The patterns apply regardless of domain — software, research, writing, consulting, operations, or anything else that produces compounding text-based work.

## Reading order

Start with the Foreword for the three-paragraph meta-stance and a map of the guide. Then read Pillars 1–4 plus Pillar 9 in any order — these five are the foundational layers, each independent enough to implement before the others are in place. Pillars 5–8 describe how to compose the building blocks into workflows; read these after you have a feel for the foundations. The Synthesis chapter (`10-synthesis.md`) walks a single practitioner through all nine pillars as one integrated system — read it first if you want the tour before the detail, or last if you prefer to build as you go.

## Contents

| # | Chapter | What it covers |
|---|---------|----------------|
| — | [Foreword](00-foreword.md) | What the guide is, who it is for, and the three claims that run through it |
| 1 | [Memory](pillars/01-memory.md) | Four-type persistent knowledge store — how to make each session start at the level of a collaborator who was there from the beginning |
| 2 | [Skills](pillars/02-skills.md) | Named, reusable slash-command procedures — converting "something I explained once" into "something we repeat reliably" |
| 3 | [Subagents](pillars/03-subagents.md) | Briefed-cold specialist workers — parallel execution, context isolation, and the brief template that makes delegation work |
| 4 | [Hooks & Guardrails](pillars/04-hooks.md) | Deterministic lifecycle enforcement — rules that run as shell commands and cannot be misread, forgotten, or overridden |
| 5 | [The Persistence Ladder](pillars/05-persistence.md) | State at four scopes — matching todos, plans, memory, and worktrees to the lifetime of the work they carry |
| 6 | [Async & Notifications](pillars/06-async.md) | Operating away from the terminal — outbound push, inbound inbox, background runs, and pacing that respects the cache window |
| 7 | [Multi-agent Patterns](pillars/07-multi-agent.md) | Independent perspective through critic loops, planner/executor splits, and second-opinion calls on high-stakes decisions |
| 8 | [Tool Discipline](pillars/08-tool-discipline.md) | Precise, fast execution — dedicated tools over shell equivalents, parallel batching, and routing large outputs through subagents |
| 9 | [CLAUDE.md & Standing Instructions](pillars/09-claude-md.md) | The always-on, manually authored project- and user-scope instructions file — the interpretive frame the assistant arrives knowing |
| 10 | [Synthesis](10-synthesis.md) | All nine pillars as one system, walked through a concrete practitioner's setup from week one to year one |

## Conventions used in this guide

The guide is project-agnostic by design: no assumption that your work is software, no single domain treated as the default. Each pillar chapter uses a worked example from outside software to anchor the principle — academic research, long-form non-fiction writing, consulting report work, legal review, home renovation, indie game development, event planning, archival history, and a small bookkeeping practice. The Synthesis chapter uses a different domain again (one-person IT consultancy) as its concrete through-line. When you read the examples, map the roles and artefacts to your own work: the pattern is always more portable than the example that carries it.

## License

This guide is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Share it, adapt it, build on it — including commercially — as long as you give credit. See [`LICENSE`](LICENSE) for the full text.
