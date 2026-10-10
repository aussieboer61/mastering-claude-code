# Week 20 — 2026-10-05

## Headline

**Do the part that is yours.** Five changes. Each one is about work that was left with the user
when it should have stayed with the assistant: a physical fix handed over when a software fix was
in reach, review notes the user had already written that the next revision ignored, a slow check
the user had to wait through and notice, an estimate whose real cost only became clear when the
deadline passed, and testing that only the user could finish.

## Why

It was the busiest week so far, with more than twice the usual number of conversations. Most of
them were hands-on: small electronics on the bench, a display that wouldn't come up, a metal
design, a new notes app built overnight by a team of agents, and an online application form for a
small business.

On the bench, the same thing happened in three separate sessions. A display showed ghosting, and
the assistant went after the wiring before it looked at the driver code. Two serial lines turned
out to be crossed, and the user was told to swap them by hand ("change the code, not the
hardware"). A monitor link dropped, and the user, who had already said it was a software problem,
was asked to swap the cables back. The week before, a request to lower a voltage had been answered
with a hardware trim when the duty cycle was the control the assistant actually held.

The application form went through a test round. The user filled in the test copy and typed
critical remarks straight into its fields. The next version still carried the questions they had
marked as out of date. They had also asked for a specific way of testing it: agents playing
different kinds of customer, each reporting the first thing that stopped them, with a fixer agent
clearing the way. A lighter round ran instead, and the form shipped with no route at all for a
customer without a business registration number.

Early in the week the user asked why every reply now ended with a long "auditing claims…" pause.
The checking hook behind it had drifted to between 45 and 95 seconds a reply. Its checker model
was doing thousands of tokens of hidden reasoning before writing a one-line verdict, and a timeout
that failed open meant the slowest replies weren't being checked at all. Switching that reasoning
off brought it down to about five seconds, with the same verdicts.

The overnight app build was estimated at "about four and a half hours to everything", based on how
fast the agents had been going. They kept that pace. But the user kept adding features as it ran,
and the estimate was never re-quoted against the bigger list. The next morning it was "another four
to five hours", and the following afternoon they were still asking what was left.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** Two new behavioural defaults.

*Pull the lever you hold.* When a fault can be fixed in something the assistant controls, such as
code, configuration, a duty cycle or a pin mapping, that comes first. Asking the user to rewire,
swap cables or trim a part is the last resort, and the assistant has to argue for it.

*The review lives in the artefact.* Notes the user leaves inside the thing being reviewed, such as
form fields, marked-up screenshots or document comments, are the spec for the next revision.
Gather them first. When the user names a method for the next round, the method is part of the ask.

**Chapter 4 — Hooks.** New failure mode: *a verification hook is paid for on every turn.* Time it.
Give the checker the cheapest setup that still catches a planted false claim. Treat a timeout that
fails open as a coverage gap to log and count, because the replies it skips are the ones most
worth checking.

**Chapter 7 — Async.** New failure mode: *a pace-based estimate holds only for a frozen task
list.* Quote an estimate together with the list it covers, and re-quote in the same reply whenever
scope is added mid-run.

**Chapter 8 — Multi-agent.** New failure mode, with the pattern that fixes it: *a user-facing flow
tested by the agent that built it.* Run a persona loop. Each agent plays a different kind of real
user and goes through the live flow until something blocks them. A fixer agent clears that
blocker, and the persona carries on from where it stopped. The loop ends when every persona
reaches the end.
