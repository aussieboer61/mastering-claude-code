# Week 10 — 2026-07-20

## Headline

**The quiet failures are the ones that report success.** Every lesson this week comes from a system that looked healthy while it was losing something. A guard configuration that rewound itself and told nobody. A nightly backup that collected the day's work, threw it away, and logged "nothing to commit". A cleanup pass that archived a service as dead while its real data sat untouched somewhere else. A browser that opened perfectly — on a screen nobody was looking at. Chapters 2, 4, 5, 6 and 9 each gain a failure mode; Chapter 1 picks up two behavioural defaults about respecting decisions that were already made.

## Why

The week's trigger was a run of incidents that shared one property: nothing errored.

The **hook rollback** was found by accident. A turn ended with a complaint about a hook script that didn't exist — a retired one, pointing at a deleted file. Pulling that thread showed a routine version-control command in the configuration directory had reverted the settings file to its last commit, eight weeks earlier. The resurrected hook was noisy; the nine guard registrations the same command destroyed were completely silent. Every script still sat on disk, intact and never invoked again.

The **backup that discarded its own work** had been reporting success every night for over three weeks. A reconcile-with-the-remote step, added after a genuine incident, sat at the end of the job rather than the start — so each run collected the day's configuration and then reset it away, after which the commit step found nothing to do and exited cleanly. The fix itself failed twice before it landed, because the script was stored inside the directory it reset, and kept overwriting its own patch mid-run.

The **cleanup that deleted a working service** came from a delegated audit. The agent saw a near-empty data directory and a month of no new records, and classified the service as dead. Both signals were misleading: the data lived in a database, not on disk, and the month of silence was the exact fault the service's health check existed to catch — a health check that had itself been failing quietly, which is why nobody had been told. Everything was recovered, because the cleanup moved rather than deleted.

The **browser on the wrong screen** cost two hours in a single sitting. Two tools in the setup can open a browser; one drives a machine in a rack, the other drives the laptop in front of you. The standing instructions named the first as "the" browser, so session after session reached for it and reported success while the person watching their own screen saw nothing happen — repeating the name of their laptop, which was the parameter all along.

And two decisions got re-litigated by an assistant that thought it knew better: a configuration value the user had deliberately chosen days earlier, changed on first-principles reasoning and then defended; and a destructive scope that appeared in a status update and was treated as though mentioning it had been the same as asking.

## What changed in the guide

### Chapter 9 — Tool discipline: new failure mode "Two tools with the same name, pointing at different screens"

When two tools perform the same verb and differ only in *which machine they land on*, a standing instruction that names one of them the default is a coin flip that always lands the same way. Write the discriminator into the rule instead: if the person is watching the result, use the tool attached to their screen; if nobody is watching, use the headless one. And treat a repeated machine name as a parameter, not as emphasis.

### Chapter 4 — Hooks: new failure mode "Hook registrations live in a file, and ordinary file operations can revert them"

Your enforcement layer is a settings file. If it sits in a version-controlled directory, every routine operation there is an operation on your guards — and a file that sessions edit constantly but nobody commits can be months stale at its last commit. Rewinds are asymmetric: a resurrected hook errors visibly, a removed hook makes no sound at all. Treat "hook script not found" at turn end as a rollback symptom, and close the window with a small hook that auto-commits the settings file whenever it drifts — one that refuses to commit an unparseable file, or a change that drops several registrations at once.

### Chapter 6 — Persistence: new failure mode "Reconcile ran after collect, and the gap was the data"

A reconcile step belongs *before* you generate the thing you intend to keep, never after. More generally: a code path that can discard work must never be able to exit successfully with a reassuring message — "nothing to do" and "I destroyed what I was going to do" must not look the same from outside. Includes the self-rewriting-script trap (a job stored inside the directory it resets reverts its own fix mid-run) and a companion note on per-machine settings living in mirrored configuration directories.

### Chapter 5 — Subagents: new failure mode "An agent asked to clean up, deciding what 'dead' means"

"Unused" is not a fact an agent can read anywhere — it has to infer it, from whatever signal is nearest. Broken is not the same as unused, and low recent activity is a symptom, not a verdict. Have a cleanup pass produce a list with a reason per item and keep the decision yourself; require positive evidence of disuse rather than absence of evidence of use; and make cleanup mean *move, with a manifest*, never delete.

### Chapter 2 — Memory: new failure mode "The store as a target the moment anything serves it"

A memory store's threat model is "my own disk" right up until a convenience puts an interface in front of it — and then it is one address returning everything you have ever written down. Require a credential from the reader in the first version, before there's anything worth reading, because the version that ends up exposed is always the one written when the data was "not sensitive yet". And keep credential values out of the store entirely, so "my notes leaked" and "my keys leaked" stay two separate incidents.

### Chapter 1 — CLAUDE.md: two new behavioural defaults

- **A settled decision outranks a fresh derivation.** The reasoning behind a chosen value isn't visible in the configuration, so "this looks wrong for our situation" is not evidence that it is. Check for a prior decision before changing a value; where one exists, it stands until the user moves it.
- **A scope mentioned in a status update is not consent.** Approval attaches to the thing the user actually said yes to. Describing a wider blast radius in passing does not authorise it, and silence about that line is not agreement. For anything destructive, name the specific thing and get an affirmative answer about that thing.
