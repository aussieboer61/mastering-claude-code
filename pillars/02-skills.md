# Pillar 2 — Skills

## Principle

A skill packages three things into a single, addressable unit: the instructions an agent follows (the body), the tools it is permitted to use (the frontmatter allowlist), and a description that serves both as human documentation and as the signal Claude matches against to trigger the skill without an explicit invocation. When you type `/your-skill`, Claude loads that file and executes it. When you do not, Claude reads every available description and decides whether the current task matches one — the skill fires automatically if it does. The description is load-bearing in both directions: it tells you what the skill does, and it tells Claude when to reach for it unprompted.

## Why it matters

Without skills, multi-step procedures live only in your head or in old transcripts. You re-explain the same sequence every session, details vary each time, and the assistant drifts from your intent as context grows stale. Skills convert "something I worked out once" into "something we repeat reliably" — and they give Claude the situational awareness to reach for the right procedure without waiting to be told.

## Components

### File location

Skills live in one of three scopes:

- **User scope** (`~/.claude/skills/<skill-name>/SKILL.md`) — available in every session on this machine. For procedures you use across contexts: a style-enforcement pass, a weekly review, a morning orientation.
- **Project scope** (`.claude/skills/<skill-name>/SKILL.md` inside a project directory) — available only when Claude Code opens that directory. For project-specific procedures: this book's citation format, a word-count gate before submission.
- **Plugin scope** — skills distributed as installable packages. Use when sharing or versioning a skill independently of any project.

A project-scope skill with the same name as a user-scope skill takes precedence, letting you override generic behaviour for a specific context without touching the shared original.

### Frontmatter

The YAML frontmatter block at the top of `SKILL.md` controls metadata and constraints:

```yaml
---
name: style-pass
description: Apply house style to the current section — enforce sentence length limits,
  flag passive constructions, correct em-dash and ellipsis formatting, and check for
  overused transition words. Use when the user says "style pass", "clean up the prose",
  "run style on this section", or after finishing a draft section and before handing off.
allowed-tools:
  - read
  - write
model: claude-haiku-4-5
---
```

Key fields:

- **name** — the slash-command slug. Lowercase kebab-case, short enough to type without looking.
- **description** — the primary trigger mechanism. Required. See description discipline below.
- **allowed-tools** — restricts which tools the agent may use. Omitting it allows all tools. Tighten this deliberately: a skill that only reads and rewrites prose has no business running shell commands.
- **model** — overrides the session default. Procedural skills (formatting passes, checklist runs, template fills) can run on a smaller, cheaper model without sacrificing quality.

### Body

Everything after the frontmatter is the instruction set the agent receives when the skill activates. Write it as a precise internal procedure — step-by-step, with explicit decision points, output formats, and instructions on what to do after the main task. Treat the body as a contract: ambiguity is filled inconsistently. The system uses a layered loading model: name and description are always in context; the body loads when the skill triggers; supporting files under `references/` subdirectories load only when referenced from the body. If the body grows long, move reference material — style guides, glossaries, templates — into a subdirectory and add a pointer from the body.

### Description discipline

The description does double duty. Keep it under 150 words:

1. State what the skill produces — the output, not just the intent.
2. List literal trigger phrases. Claude matches on meaning, but concrete examples anchor the match: "use when the user says 'style pass'" outperforms "use for prose improvement tasks."
3. Lean toward over-specification. The system undertriggers more often than it overtriggers; vagueness means Claude bypasses the procedure silently.

### User-invocable vs proactive vs both

Most skills should work both ways. You can type `/style-pass` to invoke explicitly; Claude invokes it proactively when the task matches. Write the body as if Claude must execute without further guidance — in the proactive case, it does. Skills with "invoke manually only" semantics are legitimate; state that in the description.

### A note on `skill-creator`

`anthropic-skills:skill-creator` is a skill bundled with the `anthropic-skills` plugin — not something you build yourself. Run `/skill-creator`, describe the procedure, and it interviews you on edge cases, writes a draft `SKILL.md`, generates test prompts, and iterates toward a working description. It is a useful on-ramp when writing your first skill.

## How to apply it

**Identify a candidate.** The third-time test: if you have explained the same multi-step procedure three times across sessions, it belongs in a skill. Other candidates: sequences where order matters, procedures where a missed step is expensive, context-switches at predictable moments.

**Start drafting.** Run `/skill-creator` and describe the procedure — it interviews you and produces a draft. Or write from scratch using the frontmatter template above; that is the minimum viable structure. What matters is committing to the file.

**Scope the tools.** Ask what the skill actually needs. `read` and `write` for prose editing; `bash` for running a word-count check; `read` alone for summarisation. Grant nothing beyond the minimum.

**Test the transcript.** Invoke with `/skill-name` against a realistic scenario. Read the full transcript, not just the final output — look for skipped steps, wrong assumptions, or stalls where the body should have provided information.

**Tune the description.** If Claude does not invoke the skill proactively, add concrete trigger phrases. The `skill-creator` description-optimiser generates trigger and non-trigger eval queries and iterates toward higher match rates.

**Version it.** Treat the skills directory as code. Commit with a message explaining what changed. `git diff` is your rollback when a skill misbehaves after an edit.

## Failure modes

**Bloated skills that should be split.** A skill that drafts a section, optionally runs a style pass, and optionally generates a summary is three skills in one. Split on independent code paths. Skills compose — one skill body can invoke another.

**Vague descriptions that never trigger.** "Useful for writing tasks" matches nothing reliably. Name the output, list trigger phrases, name the context. Vagueness is the most common reason a skill sits inert while Claude handles the same task ad hoc without your procedure.

**Hardcoded paths that break outside one context.** A user-scope skill embedding `/home/yourname/specific-project/outline.md` does the wrong thing everywhere else. Use relative paths, environment variables, or invocation arguments. Reserve absolute paths for skills genuinely pinned to one location.

**Skills that wrap a single command.** If the body is one command with no branching, it does not earn the maintenance overhead. Skills pay off when there are multiple steps, decision points, or non-obvious reference context.

**Skills that should be subagents.** A skill that runs for forty-five minutes, fans out in parallel, or reports intermediate progress belongs in Pillar 3. If the body says "continue in the background," that is a subagent trigger, not a skill body.

## Worked example

A freelance non-fiction writer is producing a book-length report. Each chapter must pass a house style before it goes to the editor: sentences capped at 28 words, no passive constructions in topic sentences, em-dashes typeset consistently, and a transition-word blacklist. By chapter four, the writer has explained this style guide to Claude three times from memory, and it comes out differently each session.

She opens `/skill-creator` and describes the procedure. The draft is named `style-pass`, with a description triggering on "style pass", "clean this up", or "prep for editor". The body loads `references/house-style.md` and applies rules in a defined order — sentence length, passive constructions, em-dash normalisation, blacklist scan — then produces a short change log rather than silently returning revised text.

Testing reveals one gap: the skill rewrites without flagging changes for approval. She adds one line to the body: "Display the change log and wait for user confirmation before saving." The description gets one more trigger phrase — "run style on this chapter" — and the skill is committed. From that point on, saying "this section needs a style pass" invokes the procedure identically every time, against the same reference file, with the same output format.

## Skill vs subagent vs hook

Use a skill when the procedure is bounded, single-track, and invocable at a moment of your choosing. Use a subagent (Pillar 3) when the work is long-running, parallel, or should continue while you do something else — a skill can invoke a subagent for a heavy phase. Use a hook (Pillar 4) when behaviour should fire automatically on a system event — session start, file save, tool call — with no invocation needed. The boundary test: a skill whose sole purpose is "run every session start" is a hook; one whose body says "continue in the background for two hours" is a subagent. Skills are the deliberate middle ground — repeatable, human-scale, executed on demand or on recognition.
