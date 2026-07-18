# Updates — rolling index

A weekly log of changes to *Mastering Claude Code*. Newest first. The guide itself stays current; this file (and the per-week files alongside it) exists so anyone who already read the guide can catch up on just the diff since they last looked.

Each entry lists what changed, why, and which chapter(s) were touched. Open the linked week file for the full diff and any worked examples.

**How to use this:** if you last read the guide in week N and you're back in week M, scan the entries between those weeks here. If anything sounds load-bearing for how you've set things up, open that week's file.

The archive holds the last ten weeks. Older entries are summarised at the bottom of this file and the full week files are removed.

---

## Current archive (rolling, last 10 weeks)

| Week | Date (Mon) | Headline | Chapters touched | File |
|------|-----------|----------|------------------|------|
| 09 | 2026-07-13 | **Concurrency and defaults fail in disguise.** New Ch 8 failure mode: **parallel sessions colliding in another failure's clothes** — a sibling session's test teardown reads as OOM, a fail-open coordination registry hides lane conflicts, and a conflict-free merge silently drops a branch's additions after a wholesale refactor (per-run namespaces, worktree per session, "check for a sibling" before debugging, grep the merged tree for your key symbols). New Ch 6 failure mode: **two retention windows, the shorter one upstream** — a built-in thirty-day purge starves a ninety-day archive sweep forever, silently; make the upstream window outlast the sweep. Two Ch 1 behavioural defaults: **finish the slice** (no "want me to continue?" mid-plan; follow-on steps you hold the keys for are part of the work) and **the question outranks the instruction** (answer first, background the delegation). | 1 (CLAUDE.md), 6 (Persistence), 8 (Multi-agent) | [week-09.md](week-09.md) |
| 08 | 2026-07-06 | **A rich store the assistant never opens** — the quietest memory failure: everything is recorded and a parallel system gets built from scratch anyway, because the index was never read before starting. New Ch 2 failure mode + standing default: read the index at build-start, design the smallest delta on what exists. Plus: **secret hygiene as a hook pair** (PreToolUse deny on printing secret files + PostToolUse output scan for credential shapes, with a sanctioned redacting reader) in Ch 4; three Ch 1 behavioural defaults (**sanity-check results against known context**, **ask why the primary path is out first**, **the target is the deliverable**); a Ch 9 failure mode: **adopt a maintained tool over commissioning a bespoke dashboard** — bespoke status surfaces rot; and (Friday addendum) a Ch 7 failure mode: **waiting on a worker that already died** — poll the *work state* (files, mtimes, commits), not the worker; take over inline once results exist; and (Sunday addendum) a Ch 4 failure mode: **a guard that fires once then goes silent** — re-arm a `Stop`/detection hook on a per-session counter (1st + every Nth) so it keeps its bite through long sessions, plus a Ch 1 default **lead with the answer** (put the yes/no/how-much in the first sentence, breakdown after). | 1 (CLAUDE.md), 2 (Memory), 4 (Hooks), 7 (Async), 9 (Tool discipline) | [week-08.md](week-08.md) |
| 07 | 2026-06-29 | **Self-healing background runs** — a background task can *guard* a risky live change, not just report it. Pair a cutover (DNS flip, deploy, repoint) with a watcher that polls for success and **auto-reverts** if it doesn't hold within a deadline. Two disciplines: a *consistent* success signal (two good readings, not one lucky one), and a *complete* rollback (unwind every side-effect, not just the DNS record). New Ch 7 section. | 7 (Async) | [week-07.md](week-07.md) |
| 06 | 2026-06-15 | **Find your hooks by auditing your own transcripts** — cluster the moments you corrected or repeated yourself by *what went wrong*; the top clusters are your hook backlog. New Ch 4 section + two worked, non-path-blocking hooks: a **Stop guard** that refuses a "done" claim with no proof, and a **heat-triggered `UserPromptSubmit` injector** that re-states your hardest rules only on terse orders/corrections. | 4 (Hooks) | [week-06.md](week-06.md) |
| 04 | 2026-06-01 | Guide caught up with two capabilities it predated: deterministic **workflows** (pipeline / barrier / loop-until-dry / adversarial-verify / judge-panel) and **exhaustive mode** in Ch 8, and **process skills** (the fire-before-you-act, plugin-pack kind) in Ch 3. Plus a hooks failure mode: shared state must be scoped per session. | 3 (Skills), 4 (Hooks), 8 (Multi-agent) | [week-04.md](week-04.md) |
| 03 | 2026-05-25 | The over-cautious default got **rewritten** (read/report → act-when-authorised) — week-02's prescription applied. New Ch 1 section: the behavioural defaults worth setting (act-when-authorised, stay-in-lane, search-before-asking, calibrate-confidence, evidence-before-done). New Ch 2 failure mode: **memory without provenance**. | 1 (CLAUDE.md), 2 (Memory) | [week-03.md](week-03.md) |
| 02 | 2026-05-18 | New chapter-2 failure mode: defensive-rule pileup → spoon-feeding default. Watch for the carve-out signal — when new feedback rules contradict your default, rewrite the default rather than stacking another exception. | 2 (Memory) | [week-02.md](week-02.md) |
| 01 | 2026-05-11 | Guide rewritten end-to-end. New audience (curious non-experts), new pillar order (CLAUDE.md → Memory → Skills → Hooks → Subagents → Persistence → Async → Multi-agent → Tool discipline), two output formats (published + narrated), weekly-update model. | All — full rewrite | [week-01.md](week-01.md) |

---

## Older summary (pre-archive)

*Nothing here yet — guide was rewritten in week 01.*

---

## How updates work

- **Each Monday**, a new `week-NN.md` is added with the week's changes.
- **The index** (this file) gets a new row at the top.
- **Older entries roll off** once the archive exceeds ten weeks. The week file is deleted; a one-line summary lands in *Older summary* above.
- Changes are sourced from the `CHANGELOG.md` at the repo root, but the week file is human-pitched — written to be useful at-a-glance, not just a commit log.

If you want the bare commit log, see `CHANGELOG.md`.
