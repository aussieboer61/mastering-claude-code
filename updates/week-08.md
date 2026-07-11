# Week 08 — 2026-07-06

## Headline

**A memory store pays rent only when it's consulted at the moment of decision.** This week's biggest lesson is the quietest memory failure of all: everything is recorded — the working pipeline, the component that already does ninety percent of the new request — and the assistant builds a parallel system from scratch anyway, because it never read the index before starting. Chapter 2 gains the failure mode and the fix; Chapters 1, 4, and 9 pick up four smaller lessons from the same fortnight.

## Why

The trigger was a build request whose correct answer was tiny: an existing server already rendered exactly the screen a new device needed, and the only genuinely new part was the transport it arrived over. Instead of a small delta on the recorded, working pipeline, a whole new protocol, app, and firmware got built in parallel — followed by a session of debugging problems the existing system had already solved. Nothing in memory was wrong or stale. It simply wasn't opened. That's a different disease from every memory failure the guide already covered (bloat, staleness, missing provenance), and it needs a different cure: not better writing into the store, but a standing default about *reading* it — at build time, before the first line of anything new.

The smaller lessons came from the same stretch of real work: a latency number reported as fact when geography made it impossible; a scaffold built around a fallback uplink before anyone asked why the primary was out of use; a hardware app "delivered" as a browser page; a credential printed into a transcript by a config check; and a custom-built dashboard confirmed, months on, as something that never became a daily habit.

## What changed in the guide

### Chapter 2 — Memory: new failure mode "A rich store the assistant never opens"

The fix is a standing default worth writing down: at the start of any build task, read the index, list the existing pieces that already solve part of it, and design the change as the smallest delta on those. The moment the assistant is about to author a new service, protocol, or pipeline that parallels one already in the store is the moment to stop and extend instead. *A filing cabinet nobody opens is indistinguishable from an empty one.*

### Chapter 1 — CLAUDE.md: three new behavioural defaults

- **Sanity-check results against known context.** An implausible number — LAN-grade latency to a server on another continent — is a signal to investigate, not a result to report. Companion to "evidence before done": the evidence itself has to be plausible.
- **Ask why the primary path is out — first.** When work is running on a fallback (a backup link, a secondary tool, a workaround config), establish why the designed path isn't in use before engineering around the fallback. One question up front beats a scaffold built carefully around the wrong problem.
- **The target is the deliverable.** Work built *for* a specific device or surface is done when it works there. A stand-in ("it runs in the browser") is at most a temporary aid while the real target is fixed — never the delivered answer unless the downgrade is explicitly accepted.

### Chapter 4 — Hooks: "A pair of hooks for secret hygiene"

"Never print credential values" is the canonical rule that keeps being broken as text. New section with the enforcement pair: a `PreToolUse` hook that denies piping known secret files to printing tools (allow-listing checksums, moves, and `source`), and a `PostToolUse` hook that scans command output for credential shapes and, on a hit, blocks with a treat-as-compromised-and-rotate instruction. Paired with a sanctioned redacting reader so inspection stays legitimate and the hook never becomes an obstacle to route around. Prevention makes the mistake structurally impossible; detection makes the residual failure loud.

### Chapter 9 — Tool discipline: new failure mode "Commissioning a bespoke tool when an adopted one exists"

Tool discipline applies to what you ask the assistant to build, not just what it reaches for in a session. Custom dashboards rot: the hand-maintained list behind them lags reality and they stop being opened. Ask what you would honestly open every day; adopt the maintained tool if one maps; build custom only when nothing adopted covers the need *and* the result derives its data live from an existing source of truth.

All four mirrored into the tier-1 narration.

## Addendum (Friday, same week)

### Chapter 7 — Async: new failure mode "Waiting on a worker that already died"

A delegated agent that stops with "I'll continue when the build completes" has *ended its turn* — if the thing it was waiting on finishes without re-invoking it, or the agent dies partway through its final report, nothing resumes it and no error surfaces. The finished work sits orphaned on disk while the delegating session waits, sometimes for hours, on a worker that will never land.

The discipline: past the expected window with no word, **poll the work state, not the worker** — output files, timestamps, the commit log in the target repository. If the work is done and the worker is gone, take over and finish inline; don't send another messenger after the first one. Mitigations: long-running workers commit early and often (work saved before a death survives it), and keep final reports terse — a long closing summary is a known place for a worker to die with everything undelivered. Closing rule: every delegated deliverable lands somewhere you can *see* — a URL, a rendered file, a screenshot. Work that exists only inside a repository you never open is indistinguishable from work that didn't happen.

Mirrored into the tier-1 narration.

## Addendum 2 (Sunday, same week)

### Chapter 4 — Hooks: new failure mode "A guard that fires once, then goes silent"

The Chapter 4 section on finding your own hooks already recommends a `Stop` guard that refuses an unproven "done" claim. This addendum corrects a subtle way that guard fails in practice: if it blocks only the *first* offence per session and then stays quiet, it stops protecting you exactly when you most need it. The offence it catches is rarely a one-off — a session that claims something finished without proof once tends to repeat it as it lengthens, and those later claims sail through unseen because the guard already "did its job." Read the guard's own log back across several long sessions and the shape is unmistakable: one early block, then a cascade it never stopped. The fix is a per-session counter in the state file — re-arm on the first offence and every Nth after it (first, fifth, tenth) — so the guard keeps its bite through the long sessions where discipline slips the most. A hook that can only interrupt once is a hook that stops working the moment it's needed twice. The existing "unproven claim" bullet now carries a forward-reference to this mode.

### Chapter 1 — CLAUDE.md: new behavioural default "Lead with the answer"

For a direct question — yes/no, who owes whom, how much — the answer belongs in the first sentence, with the supporting breakdown after it. A correct table the reader still has to extract the headline from hasn't answered the question at a glance. Added as a Ch 1 defaults-table row.

Both mirrored into the tier-1 narration.
