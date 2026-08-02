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

---

## Addendum — 2 August 2026

Four more, added later in the same week. Where the main round was about trusting a *description* of the system, these are about trusting a *sample* of it: one status line, one cheap probe, one glance at a page, one closing checklist. Each one is a small true observation being asked to stand in for something much larger.

### Why

The first came out of a five-day audit of a debugging run. A turn closed with a tidy status checklist — done, not done, deferred — and every item was accurately labelled. The problem was that one of them read *"fixes: none applied, deliberately"* while the same message correctly forecast that the fault would recur. It did, for another eight hours, until the user demanded the fix that had already been written down. Nothing in the checklist was false. "Deferred" is a formally valid closing state, so a turn that identifies the fix and declines to apply it still grades itself compliant. The same audit found the rule set carried roughly fourteen "never do X" prohibitions for every one "always do X" affirmative — a ratio that makes stillness the safest-scoring move.

The second is a memory problem that no amount of memory fixes. A store had grown to a hundred and fifty-odd rule files, all of them accurate. Only the index loads automatically, and the index holds one line per topic — a title and a link. So at the moment of an ordinary request, the assistant knew a rule about this existed somewhere and had no procedure to follow, and did what anyone does with a hint and no instructions: explored, guessed, reached for the wrong tool, or asked a question already answered. It reads as amnesia. The reflex is to write another rule file, which is exactly how the store got to a hundred and fifty.

The third and fourth both came from a single day of automation work. A job needed to create an issue through an API. The credential was checked first — a read against the same service, which succeeded — and the create call then failed on a missing write scope, after the plan had been committed and several steps had run. Later the same day, a browser script was pointed at a profile to find something to navigate to, so it enumerated the page's links. The profile had become logged in since it was last observed, and on a logged-in messaging application the navigation *is* the content: the script returned the conversation list with message previews, and the user's private messages landed in a transcript that persists and syncs.

### What changed in the guide

**Chapter 1 — CLAUDE.md.** New failure mode: *a self-graded status checklist can make doing nothing count as compliance.* Define "deferred" narrowly — blocked by something genuinely outside your control, never "found the fix, asking anyway" — and watch the prohibition-to-affirmative ratio in your own standing rules. *(Added 31 July; recorded here for completeness.)*

**Chapter 2 — Memory.** New failure mode: *the index carries a pointer, not the procedure.* Knowing a rule exists is not the same as being able to act on it. The fix is retrieval rather than authorship — a prompt-submit hook that injects the actual call sequence, verbatim, before reasoning starts — with two cautions: inject it as an order rather than prose, and measure the fire rate against real prompts before trusting it.

**Chapter 9 — Tool discipline.** Two new failure modes. *A probe that succeeds is not the call you are about to make* — scopes and network paths both differ between the cheap check and the real operation, so probe with the operation you intend, using the same credential, from the same place. *Driving a browser reads whatever the page is holding* — enumerating a page on an authenticated application pulls its content into the transcript, and being logged in is a moving target, so narrow the selector and re-check the sign-in state immediately before acting.
