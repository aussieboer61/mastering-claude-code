# Week 01 — 2026-05-11

## Headline

**The guide has been rewritten end-to-end.** This is the new baseline. Everything from this point on builds on this version, not the original 2026-04 draft.

## Why

The original draft was technically accurate but was written for someone already comfortable with Claude Code. It used "pillar" structure but ended up with CLAUDE.md as Pillar 9 even though it's the cheapest, most-foundational piece. The new audience is people who've heard of Claude Code but never used it — friends, peers, the curious — and want a guide they can actually share without prefacing it with "you'll need to skip the first half."

## What changed

### New audience
- Written for someone with zero Claude Code experience.
- Vocabulary primer up front (session, prompt, context, tool, agent, memory, skill, hook, CLAUDE.md) before any chapter expects you to know the terms.
- "What you'll need" + first-session walk-through in Chapter 0 before the foundations begin.

### Reordered pillars
The order now follows dependency: cheapest first, then knowledge, then procedures, then enforcement, then specialists, then the composition patterns.

| New # | Pillar | Old # |
|-------|--------|-------|
| 1 | CLAUDE.md | 9 |
| 2 | Memory | 1 |
| 3 | Skills | 2 |
| 4 | Hooks & guardrails | 4 |
| 5 | Subagents | 3 |
| 6 | Persistence ladder | 5 |
| 7 | Async & notifications | 6 |
| 8 | Multi-agent patterns | 7 |
| 9 | Tool discipline | 8 |

### Two output formats
- **`published.md`** — full markdown with tables, ASCII diagrams, code samples, and an annex prompt at the very end for spinning up a fresh AI session that already knows the guide. This is what gets rendered as HTML at the library URL.
- **`narration.md`** — same content, reshaped for the ear. Tables converted to prose. Code blocks described in words. ASCII diagrams replaced with spoken descriptions. The annex is dropped (it's not useful when heard). This is the file the library's Kokoro TTS narrates, in the British male voice `bm_george`.

### Weekly update model
The guide is now a living document. Each week's changes go into `updates/week-NN.md`. A rolling index at `updates/index.md` lists the last ten weeks. The archive caps at ten weeks — older entries get summarised down to a single line and the full file rolls off. The point is that someone who reads the guide in week 3 and revisits in week 7 only needs to scan the index, then open the two or three week files that look load-bearing for them.

### What stayed
- The worked examples (doctoral thesis, freelance writer, urban planner, etc.) are all still here; they remained the strongest part of the original guide.
- The decision rules in each chapter (when to use CLAUDE.md vs Memory vs Skill vs Hook) are preserved and tightened.
- The closing "build incrementally" framing is unchanged.

## Migration notes for anyone who read the old draft

- The old `pillars/0N-name.md` files are no longer the canonical source. Treat `published.md` as the new single-source-of-truth for the readable version, and `narration.md` for the audio version.
- The old `00-foreword.md` and `10-synthesis.md` are subsumed into Part 1 and Part 4 of `published.md`.
- The `/guide-patch` skill workflow still applies — small targeted edits to the current `published.md`, log into `CHANGELOG.md`, and roll up into the week file each Monday.

## Where to read it

- **Web:** https://claude-guide.sauer.com.au/full-guide/

---

*Next update: 2026-05-18.*
