# Week 09 — 2026-07-13

## Headline

**Concurrency and defaults fail in disguise.** This week's two big lessons share a shape: the real cause never appears in the error. Two assistant sessions working the same codebase collide — and the collision surfaces as an out-of-memory kill, a silent lane conflict, or a merge that looks clean while dropping code. And a harness's default retention setting quietly deletes material two months before the archive job downstream would have collected it — no error, ever, just an archive that stays empty. Chapter 8 gains the collision failure mode, Chapter 6 the retention one; Chapter 1 picks up two behavioural defaults about momentum and attention.

## Why

The trigger for the collision lesson was a week of genuinely parallel work: two sessions running test suites on one machine killed each other's containers (the exit code looked exactly like out-of-memory — nothing in the system logs said "your sibling did this"); a lane-claim registry was unreachable from one machine and failed open, so neither session could see the other's claim; and a feature branch merged "cleanly" against a mainline whole-file refactor, with auto-resolution silently taking the refactor and discarding most of the branch's additions — only two orphaned tests even hinted at it.

The retention lesson came from an archive-everything pipeline discovered to be archiving nothing: the harness's built-in transcript cleanup (thirty days, hard delete, on by default) ran upstream of a ninety-day archive sweeper. The giveaway, once looked for, was almost comic: the oldest surviving file was exactly thirty days old.

The two behavioural defaults came from the same stretch. An assistant that finished each build increment by asking "want me to continue?" — when the phase plan was already agreed — and that offered the final infrastructure step (DNS, certificate, service registration, credentials in hand) as an optional "say the word" extra instead of just finishing the slice. And a turn that carried both an instruction and a question, where the right shape was: answer the question now, run the instruction in the background.

## What changed in the guide

### Chapter 8 — Multi-agent: new failure mode "Parallel sessions colliding in another failure's clothes"

Two sessions on one machine rarely fail with "another session interfered" — they fail as something else. The disciplines: give each concurrent run its own namespace (test project names, ports, a worktree per session — never a shared checkout); treat an unexplained kill signal as "check for a sibling" before debugging the code; and after any merge where the other side heavily refactored shared files, search the merged tree for your branch's key symbols. *A conflict-free merge is not a content-preserving merge.*

### Chapter 6 — Persistence: new failure mode "Two retention windows, and the shorter one runs upstream"

When you build anything archival, enumerate every cleanup already acting on the source — the harness's own retention setting first — and make the upstream window outlast the downstream sweep, or disable it. The audit is one check: if the oldest surviving item is exactly as old as some tool's default retention period, that tool is winning.

### Chapter 1 — CLAUDE.md: two new behavioural defaults

- **Finish the slice.** When the plan is agreed and work remains, work through to done — no "want me to continue?" at each increment. A standard follow-on step the assistant already holds the keys for is part of the work, not an optional extra to offer back. Ship the whole vertical slice, not the eighty percent that leaves the user wiring the last mile.
- **The question outranks the instruction.** When one message carries both, the answer comes first — the question blocks the user's next thought; the instruction is delegation that can start in the background and report when it lands.
