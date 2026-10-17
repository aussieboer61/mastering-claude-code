# Week 21 — 2026-10-12

## Headline

**Say only what actually happened.** Five changes. Each one is about a gap between what the
assistant said, or assumed, and what was really true or really done: product facts stated from
memory when the manual was a download away, reference material treated as the finished product, a
promised notification that nothing was set up to send, a form filed when it was meant to wait, and
a cleanup that deleted far more than the assistant had made.

## Why

It was a quieter week than the last, about half the conversations, but most of them were hands-on
again: an old audio amplifier being stripped down and rebuilt, a gate controller designed around an
industrial drive, a battery backup unit that kept reporting a fault, a metal skateboard deck being
stress-tested and then shown off in a social post, and a notes app growing new sections almost
daily.

On the gate design, the assistant described what an industrial drive could and couldn't do from
memory, labelled some of it "unverified", and was wrong. The user's answer was blunt: pull the
manual, and stop guessing. The same week the assistant had proposed buying a logic analyser to work
out how a display was driven, when the next page of the service manual already had the full map,
and it had given a confident diagnosis of the battery unit that it hadn't checked. The user turned
it into a standing rule: official source first, third parties next, a sibling product as a
labelled baseline last, and file what you fetch.

For the social post, the assistant used the user's own workshop photos of the deck as the post's
images. Those photos had been taken to show dimensions and parts. The user had expected a rendered
3D model with a proper background, and said so.

During the deck's stress tests, the assistant tried to wait for four simulation runs with a
sleep-and-check command. A hook refused it. The reply still said "the background waiter will
notify me when the runs finish". The runs finished on time, in about the ten minutes quoted, and
nobody heard about them for well over an hour, until the user came back and asked.

On the battery unit, the user asked for a vendor support ticket to be filled in and held for
review. The assistant pressed Enter to confirm a date field, and the form submitted. The first
report of what had gone out was written from the draft and said every field was right. Reading the
live ticket showed that the part that actually asked the vendor for something was missing.

While testing a new version of the notes app, the assistant cleaned up a throwaway database
container with a host-wide volume prune. It deleted seventy-six unrelated volumes on a shared
server. The running services were fine. The orphaned volumes could not be recovered, and nobody
could say what had been in them.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** Two new behavioural defaults.

*Fetch the published document.* When a maker publishes a fact about their product, get the
document and read it before stating the fact. "Unverified" is what you write after the search has
come back empty, not instead of searching. Go to the maker first, then labelled third-party copies,
then a sibling product as a labelled baseline. Cite the page.

*Inputs are not outputs.* Reference photos, rough sketches, sample wording and templates the user
hands over are information about the deliverable, not part of it. If it is unclear which one
something is, treat it as input.

**Chapter 7 — Async.** New failure mode: *a refused wait leaves nothing armed.* Any sentence
promising a future event, such as "I'll be notified", must point at a mechanism that a tool call in
this turn actually started without error. If the wait was refused, start one the harness accepts,
or say plainly that nothing is watching the job.

**Chapter 9 — Tool discipline.** Two new failure modes.

*Filling a form you were told not to send.* Enter in a form field usually submits the form. Set
values with fill and click actions, and describe anything that went out by reading the live record
back, not from the draft.

*A cleanup command's scope is the host, not your mess.* Prune and clean-all commands act on
everything unused on the machine. Record what you create, remove exactly that by name, and leave a
host-wide prune to whoever owns the host.
