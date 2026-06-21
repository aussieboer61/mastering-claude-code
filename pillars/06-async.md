# Pillar 6 — Async & Notifications

## Principle

You are not always at the keyboard, and a mature Claude Code setup acknowledges that structurally rather than hoping you will be. "Run and watch" breaks down the moment a job takes more than a few minutes or crosses a sleep boundary. It costs almost nothing to push a notification when a task completes; it is expensive in wall-clock time and cognitive overhead to sit waiting for output that may arrive in ten minutes or ten hours. Building async into your harness from the start converts Claude from a synchronous command-prompt into a delegatable agent that works while you move and sleep.

## Why it matters

Long-running work without notifications forces a choice: park yourself at the terminal or check back hours late to find the job either finished cold or errored on step two. An inbound inbox solves the symmetric problem: without it, course corrections thought of away from the machine evaporate before the next session starts. Polling loops without sane pacing waste tokens and defeat the prompt-caching window; a tight sleep loop on an 8-minute job burns context for no reason.

## Components

- **Outbound notification**: push to your phone or a messaging channel when something completes, fails, or needs a decision. The simplest form is a one-line shell wrapper around your preferred push channel:
  ```bash
  notify "Asset bake complete — 12 levels processed, 1 flagged for review"
  ```
  Keep messages substantive. "Done" is useless; "Done — 0 failures, output at /path/to/report" is actionable.

- **Inbound inbox**: a queue you can drop messages into from anywhere — phone, another machine, a web form — that the assistant pops at session start or between major tasks. The queue must be persistent (not in-memory), capped so it cannot grow unbounded, and readable non-destructively so you can inspect it without consuming entries. The assistant's job at session start is always: check inbox, act on any messages, then proceed with the planned work.

- **Background tool runs**: the Bash and Agent tool calls both accept a `run_in_background` parameter. Use it for subprocesses that will take more than a few seconds and whose completion you want to await asynchronously:
  ```
  run_in_background: true
  ```
  Pair background runs with the **Monitor** tool, which streams events from a running background process — each stdout line becomes a notification. This lets you watch a build log in real time without blocking the main session thread.

- **Scheduled / recurring runs**: cron for fixed-cadence work (nightly builds, weekly patch-note drafts, time-boxed iteration loops); a `/loop` skill or equivalent for adaptive self-paced iteration where the assistant decides when to continue based on the state it left behind; `ScheduleWakeup` for self-directed wake-ups within a session when the assistant needs to pause and resume after a known delay.

- **Dynamic pacing**: `ScheduleWakeup` exposes the cache-window logic explicitly. The default prompt-cache window is roughly 5 minutes for short contexts, 20–30 minutes for large ones. Wake-ups longer than the active window mean the cache has evicted and re-population costs apply. For short pauses stay under 5 minutes; for overnight gaps the cache cost is irrelevant — schedule freely. Avoid the awkward middle: a 12-minute sleep on an 8-minute job crosses the cache boundary for no reason.

- **Interruption discipline**: the assistant should have a clear, written rule about when it may and may not interrupt you. Put this in your system prompt or a standing skill — explicit enough that the assistant does not have to guess.

## How to apply it

**Step 1 — Wire one notification channel.** Pick the push channel you actually check. Write a one-line wrapper called `notify` that posts to it and test it manually. One channel, one command, reliably working beats a routing layer that sometimes fails.

**Step 2 — Define checkpoints worth pinging on.** For any long-running task, decide up front what constitutes completion, what constitutes a blocking error, and whether there are meaningful milestones in between. Write these into the task prompt. "Notify me when each phase completes and immediately if you hit an unresolvable error" is followable; "let me know how it goes" is not.

**Step 3 — Add an inbound inbox.** A persistent queue the assistant checks at session start — a plain text file or a small API endpoint your phone can POST to. Teach the assistant via your system prompt or an `/inbox` skill to pop messages before doing anything else. Instructions dropped from your phone become first-class work items that survive context resets.

**Step 4 — Use background runs and Monitor for long subagents.** When you delegate to a subagent running for minutes, use `run_in_background: true` so the parent session is not blocked. Use Monitor to tail its output if you want live visibility. The subagent should push a notification when it finishes or blocks.

**Step 5 — Pick the right pacing primitive for recurring work.** For fixed-cadence jobs use system cron. For adaptive loops, use a state file with a STATUS flag and a cron trigger that checks the flag before spawning a new session. For in-session waits, use `ScheduleWakeup` and keep the interval inside the cache window unless the wait is genuinely long.

## Failure modes

- **Alert fatigue from over-notification**: if the assistant pings you on every tool call, every intermediate file write, or every minor status change, you will mute the channel within a day. Notifications should mark state transitions you care about — task complete, decision needed, long job starting — not activity noise.

- **Silent completion**: the opposite failure. A job finishes at 2 AM, you check at 8 AM, half the day gone before you can act. No outbound channel means you are implicitly choosing to poll manually.

- **Polling loops that thrash the cache**: a `sleep 10` loop for a 20-minute process generates tool calls every 10 seconds for no reason. Use `ScheduleWakeup` with a sensible interval, or let Monitor stream naturally instead of driving it in a tight loop.

- **Inbox messages without actionable context**: "fix the thing" is useless by morning. Each message should include enough context for a cold session to act: which file or system, which step in the pipeline, what the desired outcome is. It only feels over-specified until you need it.

- **Background agents whose results you forget to collect**: spawning a subagent and starting a new session without checking its output is like running a nightly job and never reading the logs. Make it a standing habit: read the last background run's output before starting new work.

## Worked example

Consider a solo game developer working on a side-scrolling platformer. Every night they kick off an asset bake — the assistant processes 40 level maps, re-exports sprite atlases, runs a lighting pass, and packages everything for a nightly build. This takes 3–5 hours and there is no reason to sit and watch it. The developer sets it running at 10 PM and drops two inbox notes from their phone: "If level 18 fails the lighting pass again, skip it and flag it — do not block the whole bake" and "Jump-height values in levels 12–15 were rebalanced today; note that in the manifest."

The assistant sends an opening notification — "Starting nightly bake, 40 levels queued, estimated 3–4 hours" — then spawns the per-level export subprocess with `run_in_background: true`, using the Monitor tool to stream the export log without blocking the session thread. At the midpoint it sends a checkpoint: "20/40 levels baked, no failures. Sprite atlas export next." When the lighting pass on level 18 fails, the assistant checks the inbox, finds the standing instruction, skips and flags that level, and continues without waking anyone at 1 AM.

At 5:30 AM the bake completes. The push notification reads: "Nightly bake done — 39/40 levels packaged, level 18 flagged, jump-height note added to manifest." The developer reads this over breakfast and starts the session in full context. That same evening, the assistant pops three accumulated playtester notes at session start, triages them (two cosmetic, one reproducible crash), and has a prioritised list ready before the developer types a single command. No job sat silently unfinished; no thought dropped into the inbox from the couch was lost.

## When to interrupt the human

Ping on: completion of any task that took more than a few minutes; errors you cannot resolve without a decision; natural checkpoints in multi-phase work where one phase's result changes the next; a "starting now" heads-up for genuinely long jobs.

Do not ping on: progress noise within a phase; decisions you can resolve yourself from standing instructions; anything the human just typed at you; routine completions in short tasks that will finish before they could read the notification.

When in doubt: one substantive, well-timed notification beats five noisy ones. A quiet channel is a trusted channel.
