# Pillar 9 — CLAUDE.md & Standing Instructions

## Principle

`CLAUDE.md` is the always-on, system-level instruction file for a project or user scope. Claude Code reads it at session start and treats its contents as standing context — things the assistant should always know when operating in this directory. Use it for everything that would otherwise need re-explaining at the top of every session: how this project is laid out, which commands to run, conventions the codebase enforces, domain-specific terminology, important gotchas, and pointers to the rest of your working environment (memory store, skills directory, hook notes). It is written by you, not by the assistant. It is scoped — either to a single project or to your user globally — not to all projects everywhere.

## Why it matters

Without a `CLAUDE.md`, every new session starts at zero for your project. You explain the same directory layout, the same deployment pattern, the same "never do X" rule — repeatedly, session after session, often halfway through a task when you realise the assistant has gone off in the wrong direction. With it, the assistant arrives already knowing how your project works. A five-minute investment in a tight `CLAUDE.md` saves you that re-onboarding cost every single session and eliminates a whole class of "but I told it last time" frustrations.

## Components

### File locations and cascade order

Claude Code reads `CLAUDE.md` files in a defined order and concatenates their contents into the session context:

1. **Enterprise policy** — injected by your organisation's Claude Code deployment, if applicable. You cannot override this.
2. **User scope** — `~/.claude/CLAUDE.md`. Applies to every session you open, regardless of project. Use it for preferences and conventions that are truly global to you: your communication style, your default tool preferences, things that should hold across all projects.
3. **Project root** — `CLAUDE.md` at the root of the directory you open with Claude Code. Applies only when you are working in that directory tree. This is where project-specific standing instructions live.
4. **Subdirectory files** — any `CLAUDE.md` files in subdirectories within the project are also read when Claude Code is working in that subtree. Use these sparingly; they add complexity and are easy to forget about.

All files in the cascade are merged additively. Later files extend the context; they do not silently replace it. If instructions conflict, the later (more specific) file takes precedence, but conflicting instructions are a sign your system needs rationalising, not adding to.

### What gets injected and when

The entire content of every `CLAUDE.md` in the active cascade is injected at session start, as a system-level prompt. It is present for the whole session. It is not selectively retrieved — it all goes in every time. This is the key constraint that shapes everything else about what belongs here: if you write five thousand words, five thousand words get loaded into every session.

### Contents that earn their place

A well-maintained `CLAUDE.md` covers:

- **Project structure summary.** Two to five lines describing what this project is, where the main working directories are, and any non-obvious layout decisions. Not a full directory listing — a mental map.
- **Common commands.** The exact commands used to run, build, test, lint, or deploy. Commands you otherwise look up or re-type from memory every session.
- **Conventions and house style.** Naming patterns, file organisation rules, anything that generates a PR comment when violated. One or two sentences per rule; a list, not an essay.
- **Domain glossary.** Terms that have specific meaning in this project and would be misunderstood by a general assistant. A three-column table (term, meaning, notes) works well.
- **Important gotchas.** Things that have caused problems before and are not obvious from the codebase alone: "never restart service X without stopping Y first", "this config file is auto-generated — edit the template, not the output", "the staging environment uses a different auth provider than production."
- **Pointers to the rest of the system.** A short section that tells the assistant where memory lives, where skills are, and what hooks are active. Not the content of those systems — just the pointers. "Memory files are at `~/.claude/projects/this-project/memory/` — read `MEMORY.md` for the index." "Skills are at `.claude/skills/` — run `/deploy` to deploy."

### Contents that do NOT belong

- **Secrets and credentials.** Your project `CLAUDE.md` is almost certainly committed to version control. If it is not, it is still a plaintext file on disk. Neither is the right place for API keys, passwords, or tokens. Those belong in a secrets manager or environment variable store that the assistant accesses via a skill or hook.
- **Ephemeral session state.** "We are currently on step 3 of 7" is not a standing instruction. Current task state belongs in a plan file (Pillar 5), not baked into `CLAUDE.md` where it will be stale by tomorrow.
- **Cross-project knowledge.** Your preferred commit message style, your general debugging workflow, your communication preferences — these apply to all your projects. Put them in `~/.claude/CLAUDE.md` (user scope) or in user-type memory files. Duplicating them into every project's `CLAUDE.md` means you update them in one place and forget the other nine.
- **Enforcement rules that must not be skippable.** If a rule matters enough that being skipped once is a real problem — "never write to the production database in this script", "this path is frozen", "always get user confirmation before deleting" — that belongs in a hook, not here. The assistant can in principle misread or deprioritise a `CLAUDE.md` instruction when context is crowded. It cannot ignore a non-zero exit code. If the consequence of skipping matters, use a hook (Pillar 4).
- **Invocable procedures.** If it is a sequence of steps the user invokes on demand — deploy this, generate that report, run the migration — it belongs in a skill file (Pillar 2), not in `CLAUDE.md`. Skills are called when needed; `CLAUDE.md` loads every session whether or not today's task requires it.

### Length and readability discipline

Every word in `CLAUDE.md` costs you tokens on every session. A bloated file does three bad things: it eats into the context budget for actual work; it dilutes the signal so the assistant weights important instructions less; and it makes the file hard for you to maintain, which means it drifts out of date. Target 50–150 lines. If you are over 200 lines, start cutting. Move stable factual content to memory topic files and replace it with a pointer. Move procedures to skill files. Move enforcement to hooks.

## How to apply it

**Start minimal.** When setting up a new project, write a `CLAUDE.md` with only the five things you are certain you would have to explain in the first ten minutes of any session. Ten lines is a fine starting size.

```markdown
# Project: [Name]

## What this is
[One or two sentences describing the project and its purpose.]

## Structure
- `src/` — [main working directory]
- `tests/` — [test files]
- `docs/` — [documentation]

## Common commands
- Build: `[build command]`
- Test: `[test command]`
- Deploy: run `/deploy` (see `.claude/skills/deploy/SKILL.md`)

## Important
- [One gotcha that will cause a problem if the assistant doesn't know it]

## System pointers
- Memory: `~/.claude/projects/[slug]/memory/MEMORY.md`
- Skills: `.claude/skills/`
```

**Grow it by noticing re-explanations.** The next time you find yourself typing the same contextual paragraph at the start of a session — a glossary term, a structural note, a constraint — add it to `CLAUDE.md`. Not everything deserves a permanent place; only things you expect to need again next week and the week after.

**Reference, do not duplicate.** When a memory file already covers a topic, point to it from `CLAUDE.md` rather than copying the content. "Deployment details: see `[[deploy-workflow]]` in memory." This keeps the single source of truth in one place and keeps `CLAUDE.md` lean.

**Trim quarterly.** Every three months, read the file end to end and ask: has this instruction been relevant in the last month? Is this still accurate? Is this in the right place (here vs memory vs hook vs skill)? Archive or delete content that hasn't been relevant. A 60-line file that is current beats a 300-line file where 40% is stale.

**Separate user-global from project-specific.** If a convention applies to all your projects, it goes in `~/.claude/CLAUDE.md`. If it applies only to this one, it goes in the project root. Mixing them means one file does two jobs and neither particularly well.

## Failure modes

**The 5,000-word `CLAUDE.md`.** The file started at 20 lines and grew over eighteen months into a full reference manual. Now it loads into every session whether or not the task needs it, burns hundreds of tokens on rarely-used sections, and the assistant has learned to effectively skim it because there is too much. The fix is a quarterly trim and a rule: if a section is useful only for one type of task, move it to a skill or a memory topic file and replace it with a pointer.

**Instructions that should have been hooks.** You wrote "never modify files in `output/` directly — they are generated" in `CLAUDE.md`. Three sessions later the assistant, under time pressure and a crowded context window, modified an output file anyway because the instruction was not visible when the decision was made. The consequence was real. Any rule where a single miss has a real cost — a broken build, a corrupted output, a safety violation — belongs in a `PreToolUse` hook that enforces it at the filesystem level, not in text the model reads and could misweight.

**Cross-project knowledge siloed in one project's file.** Your preferred error-handling idiom, your commit message convention, your rule about never force-pushing — these were written into `project-alpha/CLAUDE.md` when you were working in that project. Now you are in `project-beta` and the assistant does not know them. The fix: move cross-project content to `~/.claude/CLAUDE.md` or to user-type memory files, and delete the copies from individual project files.

**Secrets in a tracked file.** `CLAUDE.md` at the project root will almost certainly be committed to your version control repository at some point — by you accidentally, or by a future you who has forgotten it was sensitive, or by a tool that commits all untracked files. Never put API keys, tokens, database passwords, or personal credentials in `CLAUDE.md`. If the assistant needs a secret to do its work, expose it through environment variables loaded by a hook, or through a skill that reads from a secure store.

**`CLAUDE.md` and `README.md` diverging.** They serve different audiences. `CLAUDE.md` is written for the assistant: imperative, terse, focused on what the assistant needs to behave correctly. `README.md` is written for humans: explanatory, motivating, covering installation and usage. When you conflate them — "I'll just point the assistant at the README" — neither serves its audience well. The README is too verbose and narrative to be a standing instruction; `CLAUDE.md` is too terse and directive to explain the project to a new human collaborator. Keep them separate and write each for its actual reader.

## Worked example

A freelance bookkeeper runs a small practice with six recurring clients. Each client has a different chart of accounts, a different quarterly reporting cycle, and different preferences for how they receive their work. She creates one Claude Code project directory per client and places a `CLAUDE.md` at the root of each.

For a restaurant client, the `CLAUDE.md` covers three things. First, a one-paragraph description of the business: the client runs three trading entities under the one ABN for historical reasons, and transactions from the trading account need to be split across them by a rule-of-thumb ratio that the client has approved. Second, a two-entry glossary: "COGS" in this client's books means direct food and beverage purchases only (labour is classified separately), and "Casual labour" is a specific account code for variable staffing that must not be merged with "Permanent wages." Third, a pointer to the memory file that holds the actual account code mappings, which are stable but numerous: "Account mapping: see `[[restaurant-accounts]]` in memory — do not rely on standard chart conventions here."

It does not put the account code table in `CLAUDE.md` itself — that is memory's job. It does not put "generate the quarterly P&L in this format" in `CLAUDE.md` — that is a skill the bookkeeper invokes at quarter-end. And it does not put the client's bank login details in `CLAUDE.md` — those live in a password manager and are fetched by a skill that needs them.

The result is a twenty-line file that takes thirty seconds to read. Every session she opens in that directory, the assistant already knows the entity-split rule, the two glossary definitions, and where to find the account codes. She never has to explain the entity structure again.

## CLAUDE.md vs memory vs hook vs skill

These four parts of the system are complementary, not interchangeable. The following table gives the decision rule:

| Question | Right place |
|---|---|
| Should the assistant always know this, on every session, without being asked? | `CLAUDE.md` |
| Is this factual knowledge that accumulates, grows, or needs to be retrieved selectively by topic? | Memory (Pillar 1) |
| Must this rule be enforced regardless of whether the model pays attention? | Hook (Pillar 4) |
| Is this a procedure the user invokes on demand? | Skill (Pillar 2) |

A standing instruction that belongs in `CLAUDE.md`: "This project uses UK English — never switch to US spelling conventions." It is small, always relevant, and a miss is recoverable (you notice and correct it).

The same instruction as a hook would be overkill — it cannot be efficiently enforced at the shell level anyway. As a memory file it would be retrieved only sometimes. As a skill it would never be invoked. `CLAUDE.md` is right.

A standing instruction that should NOT be in `CLAUDE.md`: "Never write to `db/migrations/` without running the test suite first." That rule has a real consequence when missed. It belongs in a `PreToolUse` hook that blocks writes to that path and emits the reason. Putting it in `CLAUDE.md` gives you the appearance of safety without the substance.

The general principle: `CLAUDE.md` is for context and preferences — things the assistant should know. Hooks are for invariants — things that must happen. Skills are for procedures — things the user triggers. Memory is for knowledge that accumulates and needs selective retrieval. Each serves a different function; none is a substitute for the others.
