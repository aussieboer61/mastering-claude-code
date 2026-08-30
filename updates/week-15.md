# Week 15 — 2026-08-24

## Headline

**The loop that never told anyone what it was costing.** Six changes, and the spine
running through them is a system that keeps reporting success while the thing you
care about has quietly stopped being true — a schedule that has become a continuous
process, a resume brief that names a position twenty rounds stale, a test log that
looks clean because the run was killed before it could fail, a filter the API never
read, a hook watching a door the work stopped using.

## Why

The week's evidence came from three places.

A long-running unattended review loop, ticking on a fixed thirty-minute timer, turned
out to take one to three hours per tick. Fixed timers do not queue: each tick started
the instant the last one ended, so a "twice an hour" schedule had in fact been a single
continuous process running around the clock. It consumed eighty-two percent of a day's
entire model allowance, and nothing in the system said so — the first measurement of
its cost was the human running out of usage in the middle of the afternoon and asking
why. Two days later he ran out again. Neither the loop nor the harness around it had a
budget, a ceiling or an alarm.

The same loop resumed from a hand-written brief that said "rounds one to sixty-nine are
done, continue at seventy". It had said that since round one hundred and eight. Seven
separate sessions in one week opened by noticing the contradiction, re-deriving the real
position from the report file and the commit log, and writing a paragraph explaining the
correction — every one of them correct, none of them able to fix the file. The recovery
worked and the waste was total.

And a scatter of smaller ones from ordinary work: a test suite killed at two-thirds
whose log contained no failure lines at all, so a `grep FAILED` read it as a pass; an
API whose user filter was silently inert, returning the same four records for a real
user, a different user, and a user that does not exist; a set of files written from a
shell into a directory whose capture hook only watches the file-writing tool, so they
were never captured and a scheduled sync erased them within hours.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** One new behavioural default: **a finding already handled by
a standing process is not an event.** Before surfacing housekeeping — a credential that
looks stale, a file that should have been cleaned up, something that leaked into a log —
check whether anything already owns it on a schedule. If it does, raising it manufactures
a decision the user has already made and buries what they actually asked about.

**Chapter 4 — Hooks.** New failure mode: **a tool-event hook has a shell-shaped blind
spot.** Nearly everything a file-write hook watches for can also be done from a shell,
and only the tool call is visible to it. The guard fires on the path it was written for
and misses everything else, which is worse than no guard because it looks like coverage.
Sharpest when the environment steers toward the shell. Scope by effect as well as by
tool, and verify from the far side for anything whose loss would be silent.

**Chapter 6 — Persistence.** New failure mode: **the brief that resumes the loop is not
the state of the loop.** A position baked into a launch prompt is true exactly once.
Position is task state and belongs in an artefact the work itself writes — the report,
the commit log, the tree. A resume prompt regenerates its position from that artefact,
or names none at all. With a short-timescale companion: a figure measured early in a
long turn goes stale before the turn ends, so anything volatile gets re-read at compose
time or goes out with its timestamp.

**Chapter 7 — Async.** New failure mode: **a schedule shorter than the job is not a
schedule.** The tell is in the timestamps — consecutive runs whose start time equals the
previous run's end time rather than the next tick. Measure one real run and make the
interval exceed it with room to spare, or use a self-paced loop that re-arms on
completion. And give anything unattended that calls a model in a loop a daily budget it
reports against, so the cost is visible before it is felt. Closing note: when you find
such a loop running away, that is a decision, not a status update — the offer to kill it
belongs in the first two sentences.

**Chapter 9 — Tool discipline.** Two new failure modes. **A killed run leaves a clean
log** — a suite terminated partway never reaches its failures and never prints its
summary, so searching the log for failure markers returns nothing and reads as a pass;
gate on the exit code and treat the log as evidence about *what* failed, never that
nothing did. Companion cause: starting a second heavy job alongside a running one on a
box with room for either but not both produces exactly this signature. And **a filter
the system silently ignores** — prove a filter works by asking it for something that
must return nothing, and never use a relevance-ranked search to establish a negative;
enumerate and count instead.

## Also folded in

Two entries that landed mid-week as bare commits without a week file, now carried here:

- **2026-08-27, Ch 4** — *a discovered credential with more privilege than the task needs
  is not permission to use it.* A design that keeps a permission away from the assistant
  is a control, not a technicality; finding a more-privileged credential lying around is
  a discovery to report, not a lever to pull. Companion finding from the same incident:
  verify what a live-fire attempt actually did before writing the postmortem, or two
  separate failures collapse into one wrong story.
- **2026-08-29, Ch 9** — *reaching for discovery before the source that already has a
  name.* When a specific documented live source exists for a question, that source is the
  first tool call. One session ran forty-three tool calls of memory search, transcript
  grep, network probes and web scraping on a question with one obvious documented owner,
  and produced no answer until the user broke in.
