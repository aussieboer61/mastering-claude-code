# Week 07 — 2026-06-29

## Headline

**A background run doesn't have to just report — it can guard.** The Async chapter already covered background jobs that notify you on completion. This week adds the pattern that makes them safe for *outward-facing* work: pair a risky live change — a DNS flip, a deploy cutover, repointing a live service — with a background watcher that verifies the desired outcome and reverts automatically if it doesn't materialise within a deadline. Chapter 7 gains a "Self-healing background runs" section.

## Why

The gap was between "I can run this in the background" and "I can trust this change to the live system without babysitting it." A cutover you'd normally sit and watch — because the failure mode is a customer-facing service left down — is exactly the kind of thing you *want* to hand off, but only if failure can't be silent. The self-healing watcher closes that gap: it polls for the success signal, and if the deadline passes without it, the watcher runs the rollback itself and tells you what it did. You get informed either way — "live on the new host" or "reverted, here's why" — without standing watch.

The trigger for writing it down was a run of live cutovers where the first attempt flipped a production hostname before the new host was ready, took the site down, and a panicked manual rollback left a stale binding that kept it down. The fix wasn't "be more careful" — it was to encode the caution: stage on a preview URL, verify, cut over, and let a watcher own the revert. Every cutover after that was fire-and-forget with a floor under it.

## What changed in the guide

### Chapter 7 — Async: new "Self-healing background runs"

A short section, after "Background runs," with the shape (apply change → poll for a held success signal → auto-rollback on deadline) and the two disciplines that make it trustworthy:

- **A consistent success signal.** Require two consecutive good readings, not a single lucky one near the deadline — a transient blip shouldn't declare false victory.
- **A complete rollback.** Restoring the DNS record isn't enough if the cutover also registered the hostname somewhere that now blackholes it. The rollback has to unwind every side-effect, or the "safe" path is still broken.

Mirrored into the tier-1 narration. No other chapters touched.
