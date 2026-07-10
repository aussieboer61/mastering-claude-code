# Week 06 — 2026-06-15

## Headline

**The best source of new hooks is your own transcript history.** This week's lesson isn't a new capability — it's a method. If you want to know which rules your assistant keeps breaking, don't guess: read back over a month of your own sessions (or have the assistant cluster them for you) by *what went wrong*, not by what the task was. The recurring clusters are your hook backlog, ranked by how often they cost you. Chapter 4 gains a section on running that audit, plus two specific hooks that fall straight out of it — neither of which blocks a file path.

## Why

The Hooks chapter taught the mechanism (a rule the harness enforces beats a rule the model merely reads) and the canonical example (block writes to a frozen path). What it didn't say was *how to find the hooks that matter to you specifically*. They're rarely about code correctness. They're behavioural and repetitive — the same correction, twice: it claimed something was done when it wasn't; it did work you didn't ask for; it kept asking permission you'd already given; it trusted a stale note over the live system. Those are exactly the things a hook can catch, and they're sitting in your session logs in plain sight.

The trigger for writing this down was doing the audit in anger: thirty days of transcripts, clustered by failure mode, surfaced a clear number-one — claims of "done" with no verification — and a clear runner-up — stalling or over-stepping on a terse instruction. Both became hooks the same afternoon. That round-trip (mine your history → name the top failure → enforce it) is the reusable part.

## What changed in the guide

### Chapter 4 — Hooks: new "Finding which hooks are worth building"

A section on the audit method, then two worked hooks that aren't path-blockers:

- **A `Stop` guard that refuses an unproven claim.** It reads the assistant's final message; if it asserts *done / fixed / deployed / working* with no evidence in the same message — no command output, no status code, no commit hash, no figure — it blocks once and asks for proof or an honest "I couldn't verify this." "It works" stops being free to say.
- **A `UserPromptSubmit` injector that fires only on heat.** Silent on calm turns; when your message reads as a terse order or a correction (*just do it, I already told you, stop asking*), it prepends your hardest rules to that one turn — the discipline arrives where the record shows it slips.

Two rows were also added to the "What hooks are most useful for" table for these events.

### The framing that ties it together

A rule the model reads can be rationalised past under pressure; a rule the harness enforces cannot. So the third time you add the same line to your standing instructions, treat it as a signal: that's not a documentation gap, it's a hook waiting to be written.

## How to spot it in your own setup

- You've corrected the same behaviour more than twice → stop editing CLAUDE.md and write the hook.
- The assistant says "done" and you've learned to re-check before believing it → that's the Stop-guard hook.
- Your terse, under-pressure instructions are the ones most likely to be mishandled → that's the heat-triggered injector.

## Where to read

Both formats updated. The written version is at the same library URL; the narrated version re-renders from the patched `narration.md`.
