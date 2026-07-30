# Week 11 — The map is not the territory

**Week of 27 July 2026**

## Headline

Six lessons, and they all rhyme. Every one of them is a case of trusting a *description* of the system over the system itself — a procedure file, a status field, a documentation table, a line in an instructions file. The descriptions were all confident, all plausible, and all wrong in ways that cost hours.

## Why

A routine job: publish a long document to a personal reading-and-listening setup, and get it narrated.

It took four hours, and almost none of that was the job.

The one-command procedure for publishing named the wrong engine, on the wrong machine, with timings off by a factor of about sixty, and gave a default option that no longer existed. It had been written months earlier and never re-checked. Meanwhile the general project instructions were entirely correct — but the purpose-built file reads as more authoritative, so it won. Every estimate given to the user came out wrong in the same direction.

Then the narration kept failing. Three attempts, three completely different errors: a refused connection, a name-resolution failure, a service rejecting the request. Three faults, obviously. So: check the network, check for memory pressure, check the dependency's configuration. All plausible, all wrong. The service was being redeployed while the jobs ran — one event, wearing three costumes, and the timestamp of its process start said so in two seconds.

Then the status field. It said "missing" while the job sat in a queue. It said "error" while the job was healthy and waiting. It kept a stale error after a successful retry. It said "ready" before the output existed. A polling loop trusted it and gave up on a job that was fine.

Then the workaround. The document was stuck behind a hundred others, and the procedure file's list of operations showed no way to reprioritise. So the plan became: temporarily modify forty-one other documents to clear a path. The user, reasonably, asked what was going on — and reading the actual source took two minutes and found a documented parameter that does exactly "render this next". One query parameter, versus eighty-two mutations to someone else's data.

And underneath all of it, a line in the instructions describing a sync that ran every ten minutes to a particular machine. It had never existed. The equivalent jobs for three other destinations did exist, which is exactly why nobody had ever questioned the fourth. That machine had been drifting silently for as long as anyone had been reading the sentence.

The one that stings least but generalises best: one document was checked, found to have its audio intact, and reported as "they all have audio". Fifteen of the seventeen did not.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** New behavioural default: *One sample is not the set.* Check more than one before characterising a group, because the wrong claim then justifies an action sized for a situation that doesn't exist.

**Chapter 3 — Skills.** New failure mode: a skill that asserts facts, written once and never re-checked. Skills carry claims about the world, not just procedures — and claims age fast. Covers the authority inversion against the project instructions file, wrongness-by-omission when an endpoint list predates a feature, and the two habits that contain it: date your factual claims, and read skill-vs-project-file disagreement as the skill being behind.

**Chapter 6 — Persistence.** New failure mode: an instruction that describes automation nobody built. Why it hides so well, why sibling jobs make it look real, and the check that catches it.

**Chapter 7 — Async.** New failure mode: the ground moving under a long-running job. Repeated failures with *different* messages from one dependency in a short window mean one upstream event, not several faults — check when the dependency's process actually started.

**Chapter 9 — Tool discipline.** Two new failure modes. *Trusting a status field over the artifact* — decide completion on real size, real duration, bytes returned. *Absence from the documented surface is not absence from the system* — the obligation to read the real interface scales with the blast radius of your workaround.
