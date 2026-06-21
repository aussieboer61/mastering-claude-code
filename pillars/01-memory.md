# Pillar 1 — Memory

## Principle

Claude Code starts each session knowing nothing about you, your project, or your preferences unless you give it a durable place to store and retrieve that knowledge. Memory is a set of plain Markdown files — organized by type, indexed so Claude can navigate them quickly — that travel with your working environment and accumulate real value over months. The investment is small; you write a file once, and every future session starts better than the last.

## Why it matters

Without a memory system, you repeat yourself constantly: re-explaining your naming conventions, re-stating that you prefer one deployment pattern over another, re-locating that credential you dug up last week. With it, a new session can pick up a project mid-stream, avoid past mistakes by consulting a feedback log, and find contextual detail (config locations, API quirks, external standards) without you having to supply it. The compounding effect is real: a memory system that felt marginal at week one feels indispensable at month six.

## Components

- **`MEMORY.md` — the index file.** Lives at `~/.claude/projects/<project-slug>/memory/MEMORY.md`. This is the file Claude reads first. It contains a table mapping each topic file to a one-line description and a set of hashtags. Claude uses the tags to decide which files to open for any given task. Keep descriptions concise; the value is rapid triage, not full prose.

- **Topic files — the actual knowledge.** One file per topic, stored alongside the index. Format: YAML frontmatter followed by Markdown body. The frontmatter carries `name`, `type`, `tags`, and optionally `description`. The body is free-form but structured enough to skim (headings, short bullet lists, code blocks for anything exact like credentials or commands). Each file should be readable in under a minute.

- **Four memory types — the semantic categories.**

  | Type | What belongs here |
  |------|-------------------|
  | `user` | Who you are, your preferences, standing defaults that apply everywhere (communication style, tool preferences, recurring constraints) |
  | `feedback` | Lessons learned from mistakes — what went wrong, why, and the corrective rule. Written after an error, consulted before a similar task. |
  | `project` | Context for a specific ongoing effort: repo location, architecture overview, active work tracker, external integrations, decisions already made. |
  | `reference` | Stable external facts you'd otherwise have to look up: API quirks, vendor-specific gotchas, credential locations, standards excerpts. These change infrequently and save repeated research. |

- **The `~/.claude/projects/` directory.** Claude Code maps project directories to storage buckets here automatically when you use the `--add-dir` flag or open a directory. The `memory/` subdirectory inside each bucket is where topic files live. A cross-project memory store is possible by symlinking — useful when two project directories share the same knowledge base.

- **YAML frontmatter conventions.** A minimal header that makes files machine-readable and human-skimmable:

  ```yaml
  ---
  name: Short human title
  type: feedback          # user | feedback | project | reference
  tags: [relevant, keywords, for, index-matching]
  description: One sentence that goes in the index table.
  ---
  ```

  The index table entry and the file's frontmatter should be kept in sync; they say the same thing in two places, which is intentional — the index is for triage, the file is for depth.

## How to apply it

**Starting from scratch:**

1. Create `~/.claude/projects/<your-project-slug>/memory/` and inside it create `MEMORY.md`. Add a two-column table (File, Description) with a Tags column. Leave it empty for now.

2. Write one `user` file. Call it `me.md` or `user-prefs.md`. Put in it: who you are in one paragraph, your standing preferences (output format, verbosity level, tools you prefer), and anything that applies to every session regardless of project. Link it from the index.

3. The next time a session corrects a mistake or you notice Claude doing something you dislike, write a `feedback` file immediately. The rule: one file per lesson, frontmatter `type: feedback`, a short header explaining what went wrong, and a "How to apply" section that tells Claude what to do instead. Add it to the index.

4. As you settle into a project, write a `project` file covering: what the project is (one paragraph), where the files live, the stack or tools, and a running list of decisions already made. Update it when decisions change. This file pays for itself within the first week.

5. Whenever you find yourself looking up the same external detail twice — a vendor's API endpoint format, a quirk in a tool's config file, a standard you reference regularly — write a `reference` file and stop looking it up manually.

6. Periodically (monthly works) review the index for files you haven't opened in three months. Archive or delete them. A short index that Claude scans quickly beats a long one where relevant files get missed.

**Loading at session start:** Claude Code reads `MEMORY.md` automatically when it's present in the project bucket. If you have cross-project user-level memory, add a `SessionStart` hook that injects it (covered in Pillar 4). You can also instruct Claude explicitly: "read relevant memory before starting" in your `CLAUDE.md` system prompt.

## Failure modes

**Saving derivable facts.** If Claude can reconstruct something in one `git log` or one `grep`, it doesn't belong in memory. Memory files that duplicate what's in the codebase or version history rot instantly — the code moves, the memory doesn't. Save conclusions and decisions, not raw facts that are already tracked elsewhere.

**Duplicate memories drifting apart.** If you write roughly the same information in two files, they will diverge. A rule in `feedback-rules.md` that conflicts with a note in `project-deployment.md` creates confusion rather than clarity. Pick one canonical location for each fact and point from the other if needed. If you merge a standalone feedback file into a master rules file, delete the original.

**Stale memory cited as truth.** A memory file written six months ago about a third-party API, a production credential, or an architecture decision may no longer reflect reality. Consider adding a `last-verified` field to reference files, and treat any memory claim about live system state as a hypothesis to verify, not a fact. "The config lives at X" is a pointer to check; "The config definitely still lives at X" is overconfidence.

**Index bloat.** Every file added to the index increases the cognitive overhead Claude spends on triage. An index with 60 files where 20 are dormant, 10 are duplicates, and 5 are ephemeral notes from old sessions is worse than a 25-file index that's been tended. Do the quarterly cull.

**Dumping session state as memory.** Not every useful thing from a session deserves permanent memory. "We tried approach A and it didn't work for reason B" is often too narrow to generalize; writing it verbatim wastes space. Distil it: "Approach A fails when condition B holds — prefer approach C." The test: will this still be useful in three months, on a different machine, in a different session?

## Worked example

A researcher writing a doctoral thesis is working with Claude Code over eighteen months. Early on she creates a `user-prefs.md` noting that she prefers inline citations over footnotes, values concise prose, and always wants her claims flagged when evidence is thin. She writes a `project` file for the thesis covering her research question, the structure of her argument chapters, the location of her bibliography database, and the statistical analysis decisions she's committed to.

By month four she has three `feedback` files: Claude over-qualifies when asked to "make this more careful" (fix: ask for "tighten the hedges"); a statistical method was questioned by her supervisor (fix: use it only when the dataset meets condition Y); a citation source turned out to be a non-peer-reviewed preprint (fix: always verify source type before including).

She also has a `reference` file for her department's style guide, covering the specific edge cases she keeps looking up: figure caption format, how to cite unpublished conference proceedings, word-limit rules.

When she sits down in month twelve, Claude opens the session knowing her preferred citation style, the argument structure of each chapter, which statistical decisions are settled, and which writing patterns she's already corrected. The session starts at the level of a collaborator who's been alongside the project from the beginning, not a fresh assistant who needs re-onboarding.

## When to use which

**`user`** — when the preference applies regardless of project: communication style, output format, standing policies. One or two files; don't fragment it.

**`feedback`** — immediately after a mistake or pattern of unhelpful behavior, while context is fresh. This type compounds over time and becomes the most valuable category in a long-running setup because it prevents regressions across sessions.

**`project`** — when Claude needs to know where things live, what decisions are settled, and what's in progress. One file per active project; archive it when the project closes.

**`reference`** — when you've had to look up the same external fact more than once: API quirks, vendor-specific behavior, regulatory requirements, style guide rules. Write once, use for months.
