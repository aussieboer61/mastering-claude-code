# Week 18 — 2026-09-21

## Headline

**The model of the thing, not the thing.** Four new changes and two folded-in entries. The
thread through all of them is an assistant working from its own picture of something when the
real thing was available: a memory's summary of a rule instead of the rule, a search's view of
a store instead of the store, a quiet process read as a busy one, background offered in place
of an answer, datasheet numbers instead of the labels on the board, and the layer the tools
could reach instead of the one the user named.

## Why

The week's evidence came from ordinary work across a handful of sessions.

A payment arrived on a debt that had been written off months earlier, and the assistant booked
it the way its memory said to. The memory was a summary, in the assistant's own words, of a
rule the user had designed carefully in their own accounting software — and the summary had the
tax treatment backwards. It had been applied that way twice before. The user caught it on the
third, asked why it was being done that way again, and pointed at the design document. The
memory had not failed to fire; it fired exactly as written, and was wrong.

An application on a desktop machine refused to start because some of its settings still
pointed at a folder that had been renamed. Two days earlier a search of the machine's
configuration store for that old path had come back with zero matches. The settings had been
there the whole time, stored as encoded binary — and the search tool only matched text values.

An unattended job that renders audio from an external service sat for ten minutes having done
three items out of hundreds, with no error and no CPU use. It looked slow. It was stuck: the
local resolver was handing out an address the network could not route, and every connection
attempt waited forever. Over the other address family the same request answered in two
seconds.

In a conversation about a moral question, the user asked twice whether something was worth its
cost, and twice got background on how people come to be in that situation. They read the
background as excusing the outcome, and said so.

And two entries landed in the guide mid-week, both from a long run of hands-on hardware work:
a wiring table given in datasheet pin numbers to someone holding a board printed with different
labels, and seven hours spent re-checking a sensor the user had twice said was fine, when they
had asked for a firmware test.

## What changed in the guide

**Chapter 2 — Memory.** One new failure mode.

*A paraphrase that outranks its source.* The quieter variant of memory without provenance: the
fact had a source, but memory holds the assistant's summary of it instead of a pointer, and the
summary is what loads every session. For anything with money, law or safety attached, a memory
entry should point at the governing document and say the document wins, and the assistant
should reopen that document before acting. When memory and source disagree, the source is right
and the memory is a bug.

**Chapter 7 — Async.** One new failure mode.

*A wait with no CPU is not a slow job.* A background job at zero CPU, making no progress and
printing no error, is blocked, not slow — most often on a network connection that will never
complete. Check the process's CPU time and its open connections before deciding to wait longer;
both belong in any watch on a job nobody is looking at.

**Chapter 9 — Tool discipline.** One new failure mode.

*A search that cannot see the encoding returns a clean nothing.* A search tool only searches
the representations it can read, and returns zero, with no warning, over values stored any
other way. The mirror of *a filter the system silently ignores*: there you prove the filter by
asking for something that must return nothing; here you prove the search by asking for
something that must return something. Run it for one known positive before reporting "no
matches".

**Chapter 1 — CLAUDE.md.** One new behavioural default.

*Context is not a verdict.* A direct evaluative question gets its verdict in the first
sentence, with reasoning underneath. Background on how a situation arises is mechanism, not an
answer; offered instead of one, it reads as excusing the outcome. Having to ask the same
question twice is the tell.

**Folded in from mid-week commits.** Two entries had landed in the guide during the week
without a week file or an index row. Both had also skipped the narrated edition; this round
adds their narration.

- **Chapter 1 — *Pin numbers are not the reference frame the user has*** (24 Sep). When someone
  is working on a physical board alongside you, the identifier that matters is the label
  printed on the part in front of them, not the pin number from the datasheet. Translate into
  their frame before handing anything over.
- **Chapter 1 — *Instrumenting the layer the user already cleared*** (21 Sep). When the user
  names the layer to work on and clears another from their own inspection, that clearance is a
  scope decision, not a hypothesis to re-test. The cleared layer is usually the one the tools
  reach, which is why re-checking it looks like diligence while making no progress.

## Archive housekeeping

Week 08 rolled off the ten-week archive into the *Older summary* in the index;
`updates/week-08.md` removed.
