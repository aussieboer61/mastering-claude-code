# Week 02 — 2026-05-18

## Headline

**Defensive feedback rules can quietly become a spoon-feeding default.** Added a fifth memory-chapter failure mode covering the pattern, and a process for catching it: when new feedback files start reading as *carve-outs* from a default that's grown too cautious, rewrite the default rather than stacking another carve-out.

## Why

Played out in a real session this week. Across six months, the memory store had accumulated forty-five `feedback` files — each individually reasonable, almost all phrased negatively (never do X, stop doing Y, verify Z before reporting done). On top of them, the standing default was *report / read only — only write/create/delete when explicitly asked.*

The cumulative effect was a session that, on every turn, was checking forty-five fences before acting. Carve-outs had started appearing — feedback files explicitly saying for project X, commit without asking — which is the signal: the default itself had become the bug. Each carve-out is a half-admission that the default is too cautious, but the default keeps shipping because no one rewrites it; they just add another exception.

The fix, applied in the same session: rewrite the default. From *report / read only* to *solve the problem when authorised, ask only on destructive / undecided / shared-infra.* Then archive the four most stale or duplicated feedback files. The behavioural change was immediate and noticeable inside one turn.

## What changed in the guide

### Chapter 2 — Memory: new failure mode

Added a fifth bullet to the *Failure modes* list, titled **Defensive-rule pileup.** Names the pattern, gives the symptom to watch for (the carve-out signal), and prescribes the response (rewrite the default; audit quarterly; retire obvious rules; merge near-duplicates).

The existing four failure modes — saving things the codebase already knows, stale current-state memory, index bloat, two files saying nearly the same thing — are about storing the *wrong* things. This new one is about storing the *right* things in a way that compounds badly. Both `published.md` and `narration.md` updated.

### Nothing else moved

This is a single-chapter addition. The pillar order, the audience, the two-format split, the weekly-update model — all unchanged. If you read the guide last week, you only need to read the new bullet under chapter two's failure modes.

## How to spot it in your own setup

Three signals, any one of which warrants an audit:

1. **You're writing feedback files faster than you're retiring them.** The store grows monotonically. Healthy stores prune.
2. **New feedback files contradict the standing default.** For X, do Y without asking is the carve-out shape — it's saying the default is wrong for X. If three or four files do that, the default is wrong for more than X.
3. **The assistant asks before acting on things you've already authorised.** That's the user-facing symptom. The cause is in the feedback dir.

When two or three of these light up, sit down with the memory store for an hour, retire what's stale, merge what overlaps, and rewrite the default itself.

## Where to read

The chapter-2 update lands in both formats. The written version is at the same library URL; the narrated version re-renders automatically (Kokoro picks up the patched `narration.md` on next regeneration).
