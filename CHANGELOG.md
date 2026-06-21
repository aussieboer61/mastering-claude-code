# Changelog

Lessons absorbed into the guide, newest first. Each entry: date, one-line summary, affected pillar(s), files touched.

- 2026-04-27 — Route heavy compute to the executor built for it, not the orchestrator host; the orchestrator's job is responsiveness, not throughput — Pillar(s): 8 — Files: pillars/08-tool-discipline.md
- 2026-04-26 — Flat fan-out without a manager agent produces sibling collisions when sub-tasks share design space; use a manager whenever workers might need to coordinate — Pillar(s): 3, 7 — Files: pillars/03-subagents.md, pillars/07-multi-agent.md
