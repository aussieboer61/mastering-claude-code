# Week 12 — The report nobody drains

**Week of 3 August 2026**

## Headline

Five lessons, and four of them are about *repetition without attention*. A scheduled agent that finds the same fault every morning and writes it up fresh every morning. A one-off request that turned itself into a standing job and quietly filled a drafts folder. A batch of documents regenerated because "the broken ones" was read generously. A second opinion asked of a model that shares every one of the first one's blind spots. In each case nothing errored, nothing looked wrong in any single instance, and the failure existed only in the sequence — which is exactly the thing a system that starts fresh each time cannot see.

The fifth is smaller and sharper: a fact confidently read off a picture too small to contain it.

## Why

A machine on another continent has a backup job for one person's drawings. It has failed every single run since early July — 484 failures out of 488 attempts — and it failed again this morning. That is five weeks of one person's work with no backup at all.

It is not that nobody noticed. It was noticed on more than thirty separate mornings. A scheduled agent checks that system daily and writes a health digest, and the failing job appears in every one of them, correctly described, under a heading like *carried items*. Two other faults on the same machine had the same career: a service restarting in a loop, whose restart count climbed across six consecutive reports — two thousand, then eight thousand, then thirteen thousand, then twenty-four thousand — and a tunnel that had restarted twenty-nine thousand times, ten thousand of them in the preceding day.

Every one of those reports was accurate. Every one was well written. And the aggregate effect of thirty accurate reports was that a person's drawings went unbacked for five weeks, because the section they lived in never changed and therefore stopped being read. An agent that starts cold each morning cannot notice that it said the same thing yesterday, and a reader who has learned a paragraph never changes is a reader who will miss the day it does.

The others came from the same week and rhyme with it. A request to fix the audio on a few documents was resolved as ten — "the broken ones" is a description, not a list. A single instruction to draft a message to a phone company became a recurring job that kept producing drafts nobody asked for, discovered only because the drafts folder filled up. A high-stakes judgement about a legal forum was checked against a second model from a different vendor, which flatly contradicted the first answer and turned out to be right — a check that a second instance of the same model would almost certainly have failed. And a place name, read off a 215-pixel thumbnail, produced a real historic building and a real historic figure, neither of which was the building or the figure on the sign; a delivered folder had already been named after them.

## What changed in the guide

**Chapter 1 (CLAUDE.md) — two new behavioural defaults.**
*End on the measured result* — when the assistant reports something it measured, the report ends there; no pending deal, no unrealised upside, no consolation paragraph. Softening a measured figure with an unrealised one implies the result is less real than it is, and asks the reader to be hopeful on cue.
*Name the set before a batch mutation* — state the exact list before changing a batch of things the user relies on, and act only on that list. "Fix the broken ones" is a description; resolving a description generously is how three become thirty. Naming the set costs a sentence; the user finding the other twenty-seven costs their trust in every batch afterwards.

**Chapter 5 (Subagents) — new failure mode: a scheduled agent's report is a queue, and nobody is draining it.** A recurring agent re-discovers the same finding every run and writes it up fresh, so a real defect becomes wallpaper with a rising number attached. Each report is individually correct, which is why the pattern is invisible; the failure lives only in the sequence. Fix: hand the agent its previous output and ask for a *diff* — new, cleared, unchanged and for how long — and set an escalation rule with teeth, where a finding surviving three consecutive runs must be fixed or escalated once as a named decision. If a report can carry the same item indefinitely without anything changing, it is a to-do list nobody owns.

**Chapter 6 (Persistence) — new failure mode: a one-shot instruction that quietly became a standing job.** A repeatable-looking request is a tempting seed for a recurring task, and automating it reads as initiative. The user finds out from the accumulation, not from a failure. Recurrence is opted into, never inferred; a single imperative buys a single action, and any recurring job announces where it lives and how to stop it. The audit: for every scheduled job, name the moment recurrence was asked for. The tell: artefacts piling up somewhere the user visits rarely.

**Chapter 8 (Multi-agent) — new failure mode: a second opinion from the same model is a mirror.** Two instances of one model share the training, the priors and the blind spots, so the second arrives at the first one's answer by the first one's route. For load-bearing decisions, ask a model from a different vendor and treat cross-vendor agreement as the signal; a split locates where the question is genuinely open and is worth surfacing rather than resolving silently. Mechanics: numbered questions, percentages where you want comparable judgements, explicit instruction on what to be blunt about. Two plumbing traps: a wrapper reading a fixed input path will review the wrong document forever, and a tool that appends piped input to its prompt hangs on an inherited non-interactive stream.

**Chapter 9 (Tool discipline) — new failure mode: reading a fact off a downsampled image.** A thumbnail has had the glyphs destroyed before the model sees it, so what comes back is a reconstruction that fits the surviving shape — and it will be plausible, which is what makes it dangerous. It compounds when the guess becomes a name on a folder or a record. Crop and render the region at full resolution before asserting anything read off an image; if it still won't resolve, say unverified and name the blocker. Thumbnails are for triage, not for text.

**Site fix.** The full-guide page carried a malformed duplicate Chapter 8 heading — a stray horizontal rule fused onto a repeated title — which rendered as a phantom extra chapter. Removed.
