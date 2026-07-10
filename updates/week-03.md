# Week 03 — 2026-05-25

> Written 2026-06-01 as part of a two-week catch-up (weeks 03 and 04 landed together). The lessons themselves date to this week.

## Headline

**The over-cautious default got rewritten — and a small set of behavioural defaults turned out to matter more than any project fact.** Week 02 diagnosed the *defensive-rule pileup*: feedback rules accumulating until the assistant arrives half-paralysed, asking permission to breathe. This week the prescription was actually applied — the standing default flipped from *read and report; ask before acting* to *act when the work is authorised; ask only when a step is hard to reverse, undecided, or touches shared infrastructure* — and the change took inside a single session. Chapter 1 now names the handful of defaults worth setting; Chapter 2 gains a provenance failure mode.

## Why

Two threads from real sessions.

The first is the follow-through on week 02. Naming the pileup wasn't the fix; rewriting the default was. The interesting part is how *small* the rewrite is — two clauses — against how large the behavioural change is. An assistant that had been pausing at every step to confirm started driving work to completion the moment the resting behaviour changed. That's worth a chapter note, because the lesson is easy to read as "audit your feedback files" when the actual lever is "rewrite the one sentence those files are all carving exceptions from."

The second is that the defaults which earn their keep aren't project facts at all — they're standing instructions about *how* to act. Five recurred often enough to name: act-when-authorised, stay-in-lane (a side-comment is not a new task), search-before-asking (look on disk before asking the human to re-supply), calibrate-confidence (label the unverified, flag risk up front, don't fold when you're right), and evidence-before-"done" (check the symptom is gone before reporting it fixed). Each of these had been a separately-learned correction; collected, they read as the behavioural spine of a good setup.

A third, quieter lesson rode along: **memory needs provenance.** A claim with no source is a claim that can't be audited, and the assistant's plausible guesses, once written down, get treated by every later session as established fact. A fabricated detail doesn't sit still — it propagates through everything derived from it, and it bites hardest in anything written in your own voice.

## What changed in the guide

### Chapter 1 — CLAUDE.md: new "Behavioural defaults worth setting"

A short subsection and a five-row table: act-when-authorised, stay-in-lane, search-before-asking, calibrate-confidence, evidence-before-"done". The framing note matters as much as the list: these are *defaults*, phrased as what *to* do, kept small — because a pile of "never do X" defaults is the very thing Chapter 2 warns about.

### Chapter 2 — Memory: strengthened pileup + new provenance failure mode

The *defensive-rule pileup* bullet now carries the concrete before/after of the rewrite and the "took inside one session" result. A new failure mode, **Memory without provenance**, covers source-tracing, the propagation hazard, and marking inferences as inferred.

### Tier 0.5 — one analogy touch

The filing-cabinet piece now notes that each card should say where its fact came from — so a year later you trust the card instead of half-remembering whether it was ever true.

## How to spot it in your own setup

- You authorised a class of work last week and the assistant still asks before each step → your default is too cautious; rewrite the sentence, don't add another exception.
- A detail in a generated letter or document turns out to be something nobody ever told the assistant → an unsourced inference hardened into fact. Add provenance.

## Where to read

Both formats updated. The written version is at the same library URL; the narrated version re-renders from the patched `narration.md`.
