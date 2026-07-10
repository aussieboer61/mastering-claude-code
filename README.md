# Mastering Claude Code

A practical guide for the curious — friends-of-friends edition.

This is a guide for people who've heard the name Claude Code, maybe tried it once or twice, and want to get more out of it than the box gives you. No prior expertise assumed. The patterns apply regardless of domain — writing, research, consulting, software, ops, or anything else that produces compounding text-based work.

## Read it on the web

The rendered guide, with narrated audio, lives at **https://claude-guide.sauer.com.au** — a landing page plus one page per tier.

## Three reading paths

The same material, three depths. Read in order, or skip straight to the one that matches your appetite.

| Tier | File | Who it's for | Length |
|------|------|--------------|--------|
| **0** | [`tier-0.md`](tier-0.md) — *What Claude Code Actually Is* | Anyone who thinks "Claude Code = for programmers" and would otherwise never try it. No tools, no install, no jargon. Capability tour with non-software vignettes. | ~1,900 words, 8 min |
| **0.5** | [`tier-0.5.md`](tier-0.5.md) — *The Nine Things Worth Building, In Plain English* | Tier 0 readers who got curious. Each pillar as a household analogy (standing letter, locked cabinet, recipe drawer…) plus a "what to build first" adoption order. | ~1,900 words, 8 min |
| **1** | [`published.md`](published.md) / [`narration.md`](narration.md) — *Mastering Claude Code* | People ready to actually set it up. Full nine-pillar treatment with tables, code, file paths, walked example. | ~12,000 words, 50 min |

Tier 0 + 0.5 are the shareables. Tier 1 is what you hand someone after they've decided to do the work.

## The nine pillars

The guide is organised around nine things worth building, in dependency order:

1. **CLAUDE.md** — a standing letter to your assistant: the context and behavioural defaults it arrives knowing.
2. **Memory** — a store of small indexed files, so each session starts at the level of a collaborator who was there from the beginning.
3. **Skills** — named, reusable procedures: "something I explained once" becomes "something we repeat reliably".
4. **Hooks & guardrails** — rules enforced by the harness itself; the ones the model cannot skim, forget, or rationalise past.
5. **Subagents** — briefed-cold specialist workers for parallel or heavy work, keeping the main context clean.
6. **The persistence ladder** — todos, plans, memory, worktrees: state kept at the scope that matches its lifetime.
7. **Async & notifications** — work that runs while you're away, with outbound push, an inbound inbox, and self-healing background runs.
8. **Multi-agent patterns** — critic loops, second opinions, and deterministic workflows for decisions that are expensive to get wrong.
9. **Tool discipline** — the cheapest tool that does the job, batched, with large outputs routed through subagents.

## Tier 1 structure

Tier 1 ships as two files with identical content reshaped for the medium:

- **`published.md`** — written version. Tables, ASCII diagrams, code samples, and an annex prompt at the end for spinning up a fresh AI session that already knows the guide.
- **`narration.md`** — audio version. Prose flow, no tables, no code blocks. This is the text behind the narrated audio on the web version.

Both follow the same nine-pillar structure:

| Part | Chapters | What you'll get |
|------|----------|------------------|
| 1. Getting Started | 0 | What Claude Code is, vocabulary, first session |
| 2. Foundations | 1. CLAUDE.md · 2. Memory · 3. Skills · 4. Hooks · 5. Subagents | Five building blocks of a real setup |
| 3. Composition | 6. Persistence ladder · 7. Async · 8. Multi-agent · 9. Tool discipline | Combining the building blocks into workflows |
| 4. Putting It Together | — | A walked example (Alex's consultancy), adoption order, caveats |

The chapters in Part 2 are independent — read them in any order.

## Weekly updates

The guide is a living document, updated as real sessions teach new lessons. Each round of changes is logged in:

- [`updates/index.md`](updates/index.md) — rolling index of the last ten weeks, newest first.
- `updates/week-NN.md` — one file per week with the actual changes.

If you read this in week 3 and revisit in week 7, open `updates/index.md` and scan the rows between those weeks. Older entries (beyond ten weeks) roll off into a single-line summary at the bottom of the index. [`CHANGELOG.md`](CHANGELOG.md) holds the full lesson-by-lesson history.

## License

This guide is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Share it, adapt it, build on it — including commercially — as long as you give credit. See [`LICENSE`](LICENSE) for the full text.
