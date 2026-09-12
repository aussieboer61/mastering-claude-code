# Week 16 — 2026-09-07

## Headline

**The fact nobody checked.** Four new changes and three folded-in entries, and the spine
through them is work built confidently on a fact that was assumed rather than checked: who
made a change, where a test was run from, what the user actually owns, how a brief framed
the thing it was asking about — and, from the mid-week entries, whether an empty table
had ever been written to at all.

## Why

The week's evidence came from ordinary work across a handful of sessions.

An unexplained deletion landed inside the window of a long-running media workflow. The
timing made it look like one of the workflow's agents had gone off-script, so the session
restored well over a hundred gigabytes and re-added four library entries. The user had
deleted them himself, on purpose, minutes earlier — and had to ask for the same deletion
a second time.

A security check reported a web service as reachable straight at its public address,
bypassing the CDN in front of it. The test had been run from inside the home network, where
hairpin routing and a local allow-list answer requests aimed at the public address. A
redundant allow-list layer went in before the test was repeated from a genuinely external
machine, which showed the port had been closed to everything but the CDN for months. Earlier
in the same session, told plainly that the page was broken, the assistant had been reading
the healthy APIs behind it rather than loading the page.

Two published reference documents on an electronics build were written around a component
inferred from four characters of a message. The question "which parts do you actually have?"
was asked only after both were published. In the same week, a named visual reference ("like
that app's graph view") was answered first with a tree diagram, then with cards, before
anyone looked at what the reference actually draws.

And a brief sent to two outside models for a second opinion on a personal situation placed
an action the user had explained as an attempt to understand under a heading listing
conduct he "had not denied". Both models, from different vendors, judged it as the adverse
act the heading implied.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** New behavioural default: **ask for the fact the build rests on,
before the build.** When a deliverable depends on something only the user knows and a quick
search does not find it, ask that one question first. An inference from a few characters is
not an inventory. Corollary: a named reference is the spec — look at what it renders before
building the nearest thing you already know how to build.

**Chapter 8 — Multi-agent.** New failure mode: **a second opinion is only as neutral as its
brief.** Raw inputs instead of your conclusion is necessary, not sufficient — whoever writes
the brief is the first agent. Headings, placement and which stated reasons survive all carry
a verdict. Cross-vendor agreement on a slanted brief is agreement about the brief. Keep
headings descriptive, put each stated reason next to the fact it explains, and have someone
read the framing before it goes out.

**Chapter 9 — Tool discipline.** Two new failure modes. **Undoing a change you assumed your
own tooling made** — the mirror of naming an external actor: overlap in time is not
attribution; tie the change to an actor from the application's log or your own tool-call log
before reverting, and ask if you can't, because a revert of someone's deliberate action is a
second destructive change. And **measuring exposure from inside the fence** — a reachability
test run from inside the network measures the network's view of itself; test from outside
before acting, and when the user says the page is broken, load the page.

## Also folded in

Three entries landed as bare commits without a week file since week 15, now carried here:

- **2026-09-01, Ch 1** — *ship everything the ask specified.* When a deliverable has an
  explicit multi-part spec, ship every part or name what is being cut. Quietly deciding an
  item from the source material isn't worth including is a decision that belongs to the
  person paying for the outcome.
- **2026-09-03, Ch 9** — *a wholesale rewrite of a document under revision drops what the
  rewrite didn't remember to keep.* Regenerating a body from your summary of it loses
  deliberately-kept content; and a rejected tool call is not one that never ran. Targeted
  edits against the current file; re-read after any ambiguous tool outcome.
- **2026-09-13, Ch 9** — *an unwired tracking table reads as never-happened, always.* A table
  seeded to record an external event before anything writes to it returns empty forever, and
  empty looks exactly like a true negative. Check whether anything writes to it at all, and
  verify against the primary record it shadows.

Week 06 has rolled off the ten-week archive into the Older summary.
