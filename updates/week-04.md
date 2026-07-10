# Week 04 — 2026-06-01

## Headline

**The guide caught up with two capabilities it predated.** It was written in mid-May, before deterministic multi-agent *workflows* and before the *process-skill* plugin model were everyday tools. This week both went in: Chapter 8 gains a section on handing the control flow to a workflow (and on "exhaustive mode"); Chapter 3 gains the second kind of skill — the ones that fire *before* the work. Chapter 4 also picks up a hook failure mode that only shows up once you run more than one session at a time.

## Why

The multi-agent chapter described five patterns you drive *by hand* — spawn, read, decide, spawn again. That's still the right starting point, but it stops describing reality once the shape of a job is known. At that point you don't want to babysit the fan-out; you want to write the loop, the fan-out, and the verify-each-finding step down as a script and let it run. The vocabulary that comes with that — pipeline, barrier, loop-until-dry, adversarial verify, judge panel — is small, and worth naming because each term encodes a real decision (when to wait for the whole set, how to size an unknown search, how to stop a confident-wrong result reaching you).

Skills had the same gap in the other direction. The chapter covered *procedure* skills — a deploy, a style pass — but not the class that has grown up since: skills that encode *how to approach* a kind of work and fire before you start it. Brainstorm-before-build, test-first, debug-before-fix. These ship as installable plugin packs now, not as files you hand-write, and the discipline that makes them work — consult them *before* you charge in — is the part most people get wrong.

The hooks lesson came from a real cross-session collision: a hook wrote a bypass flag under a fixed name, a second concurrent session saw the flag, and a guard that should have fired didn't. The fix is boring and general — put the session ID in the filename — but the failure is invisible until two sessions overlap, so it's worth writing down.

## What changed in the guide

### Chapter 8 — Multi-agent: new "When the shape is known: workflows"

A new section after the five patterns: what a workflow is, the five-term vocabulary in plain language, when to orchestrate vs when to scout first, and a named posture — **exhaustive mode** — for spending tokens to buy confidence on decisions that are expensive to get wrong. Two failure modes added: *orchestrating before you know the shape*, and *silent caps*.

### Chapter 3 — Skills: new "A second kind: process skills"

Procedure skills you invoke vs **process skills** that fire before the work. Examples (brainstorm/test-first/debug), the consult-before-you-start discipline, and the plugin-pack distribution model.

### Chapter 4 — Hooks: new failure mode

**Shared hook state that leaks across sessions** — locks, bypass flags and dedupe markers must be scoped per session or they collide.

### Tier 0.5 — one analogy touch

The "colleague who reads your draft" piece now notes that once you trust a review routine, you can write the routine *itself* down so the reader and the foreman run themselves across a stack of work.

### Annex

The condensed system-prompt payload at the end of Tier 1 was updated to match — process skills, session-scoped hook state, workflows/exhaustive mode, and two recurring patterns (provenance, behavioural defaults).

### Housekeeping — display font

Unrelated to content: the site's display heading typeface was swapped from a serif (Fraunces) to the same sans-serif (Inter) used everywhere else on the site, for consistency. Nothing in the guide text changed.

## How to spot it in your own setup

- You find yourself manually spawning the same fan-out-then-verify shape for the third time → write it as a workflow.
- A guard or a "once only" action misfires only when you have two terminals open → a hook is sharing state across sessions. Add the session ID to the state filename.

## Where to read

Both formats updated. The written version is at the same library URL; the narrated version re-renders from the patched `narration.md`.
