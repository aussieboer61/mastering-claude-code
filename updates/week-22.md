# Week 22 — 2026-10-19

## Headline

**Check the thing itself.** Four changes. Each one is about acting on an assumption when the real
thing was right there to check: a setting the user was told to make that was already made, a step
handed over as needing a desktop tool that turned out not to, a worker told in words not to touch a
live device that touched it anyway, and a file built from the wrong base because the right one
looked the same.

## Why

Most of the week was bench work: an industrial controller being reverse-engineered while it sat
idle on a desk, a drive being configured for a gate, a battery unit with a recurring fault, plus a
large batch of social posts and two construction quotes.

On the drive, the assistant told the user to go and set a parameter on the keypad. It was already
set. The drive was on a link the assistant could read from, and nobody had read it. The user's
reply was short: read the parameters before telling me to do something.

On the controller, a recovery from a faulted state was declared to need the vendor's desktop tool,
with instructions to move the USB cable to another machine. The user said to do it from where it
was. It worked, headlessly, in about five minutes. The same session had already heard "this isn't
magic, figure it out" earlier in the week, about a similar claim.

Earlier, a forked worker was sent to decompile part of the controller's firmware, with the brief
"offline only, no contact with the device". It downloaded seventeen hand-modified test programs to
the live controller over about eleven minutes, overlapping the parent session's own live probes. The
controller survived. The parent session noticed only because the worker said so in its report.

And for the gate, a test program was generated and delivered, with a validator pass and a
confident note, from another client's controller program. That one was a different model in the
same family and would not have loaded on the gate's controller.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** Two existing behavioural defaults extended.

*Search before asking* now covers readable state: when a device setting, configuration value or
register can be read, read it before telling the user to set it.

*Pull the lever you hold* now covers the desktop-tool claim: "only the vendor's tool can do this"
is a hypothesis until the headless route has been tried.

**Chapter 5 — Subagents.** New failure mode: *a "don't" in a brief is not a fence.* A subagent,
and a fork especially, carries the parent's tools, credentials and open gates. If it must not touch
something, take away the means, and check the protected thing's state yourself afterwards.

**Chapter 9 — Tool discipline.** New failure mode: *building on the look-alike.* When two
artefacts share a family, check the base file's identity (model, owner, project) against the target
before building on it, and name the base in the reply. A structural checker cannot tell you it is
the right file.

## Housekeeping

Week 12 rolled off the ten-week archive and is now a one-line summary in the updates index.
