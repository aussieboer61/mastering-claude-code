# Mastering Claude Code

## A Practical Guide for the Curious

*A friend-to-friend guide to getting more from Claude Code than the box.*

> **What you're reading.** This is a written guide with tables, diagrams, and a small bonus prompt at the very end that's not meant for you — it's meant for an AI you can paste it into. There's also a narrated version of this same guide (same words, fewer tables) if you'd rather listen than read.
>
> **Why this exists.** Most people who hear about Claude Code paste a question into it, get an answer, and move on. That works, but it leaves nine-tenths of the tool on the shelf. This guide is for the moment you decide to pick up the rest of it.
>
> **Sharing.** Pass this along. The whole point is to make this less of a secret club and more of a shared toolkit.

---

## How to read this

The guide is in four parts.

**Part 1: Getting Started** assumes you've heard the name "Claude Code" and not much else. It explains what the tool actually is, what you'll need, and walks you through a first session so the rest of the guide has somewhere to land.

**Part 2: The Foundations** is the heart of it. Five chapters covering the five things you build once and then use every session forever: a standing letter to your assistant (CLAUDE.md), a long-term knowledge store (Memory), one-command procedures (Skills), rules your assistant cannot skip (Hooks), and delegating to specialists (Subagents). Each chapter is independent — read in any order.

**Part 3: Composition** is four chapters about combining the foundations into real workflows: state at the right scope, work that runs while you sleep, getting a second opinion automatically, and choosing tools well. These build on the foundations and refer back freely.

**Part 4: Putting It Together** walks through a single person's setup across all nine pillars, suggests an adoption order, and tells you when *not* to bother.

**Annex** at the end is a block of text for an AI, not for you. It's a copy-and-paste prompt you can drop into a fresh Claude session to bring the assistant up to speed on this guide. Ignore it unless you want it.

| Part | Chapters | What you'll get |
|------|----------|------------------|
| 1. Getting Started | 0 | Enough background to follow the rest |
| 2. Foundations | 1–5 | The five building blocks of a real setup |
| 3. Composition | 6–9 | How to combine them into useful workflows |
| 4. Putting It Together | — | A walked example, adoption order, caveats |

---

# Part 1 — Getting Started

## Chapter 0 — What Claude Code actually is

Claude Code is a program you run in your terminal that talks to Claude (the AI). That's the headline. The detail is what makes it interesting.

When you use Claude through a web browser, you get a conversation window: you type, Claude replies, you type again. When you use Claude Code, you get the same conversation plus the ability for Claude to **read files on your computer, run commands, edit files, and remember things between sessions** — provided you set those things up. It's the difference between asking a friend for advice over the phone and giving them the keys to your kitchen.

### Why bother going past the browser

Most people who try Claude in the browser run into the same wall: every conversation starts from zero. You have to re-explain your project, re-state your preferences, re-paste the same files. By the third or fourth conversation, you stop bothering with anything complicated and use it for one-off questions only.

Claude Code lets you build a working environment that **remembers**, **enforces rules**, and **does work while you're not at the keyboard**. The investment to set up each piece is small. The pay-off is that conversation number five doesn't start at the same place conversation number one did — it starts wherever you left off, knowing what you've already established.

### A few words you'll see throughout

| Word | What it means in plain English |
|------|--------------------------------|
| **Session** | One run of Claude Code in your terminal, from open to close. Like one phone call. |
| **Prompt** | A message you type to Claude. Same as in the browser. |
| **Context** | Everything Claude can see right now — your prompts, its replies, anything it's read so far. A finite scratch-pad. |
| **Tool** | A specific action Claude can take, like "read this file" or "run this command". |
| **Agent** (also "subagent") | A second copy of Claude you can hand a task to, briefed cold, while your main session keeps doing other things. |
| **Memory** | A folder of small text files Claude reads at the start of every session to remember what matters across conversations. |
| **Skill** | A named procedure you've written down once that Claude can run on demand by typing `/your-skill`. |
| **Hook** | A small script that fires automatically at certain moments — like before any file is written — to enforce a rule. |
| **CLAUDE.md** | A plain-text file at the root of your project that Claude reads at the start of every session. Like a standing letter. |

If those last few don't make sense yet, don't worry — each one has its own chapter. The table is here so you can come back to it.

### What you'll need

- A computer running macOS, Linux, or Windows (via WSL).
- A terminal — the black-text-on-a-screen window. Comfort with it at the level of "I can change directories and run a command" is enough.
- A Claude account. The Pro plan ($20/mo) is the usual starting point; you can also pay per use through Anthropic's API if you'd rather.
- About thirty minutes to install and run a first session.

### Your first session, walked through

The official install instructions live at the Claude Code documentation; they change occasionally, so I won't try to mirror them here. Once installed, this is what a first session looks like.

You open your terminal, change to a folder you care about — let's say a folder containing some notes you've been making for a side project — and type `claude`. A prompt appears. You type:

> *What's in this folder?*

Claude reads the directory and tells you what it found. You type:

> *Open `ideas.md` and summarise the three most recent entries.*

Claude opens the file, reads it, and produces a summary. So far this is what the browser does too.

Now the difference. You type:

> *Save my preferences: I want concise answers, no preamble, and bullet points only when they actually help.*

Claude, by default, doesn't have a way to do that — but with a memory store set up (Chapter 2), it can write that to a small file and read it at the start of every future session. From that point on, every conversation knows that about you. You stop saying it.

That's the rhythm of the whole guide: each pillar makes one piece of "I have to say this every time" stop happening.

---

# Part 2 — The Foundations

These five chapters are the building blocks. Read them in any order. Pick the one that matches your current frustration.

---

## Chapter 1 — CLAUDE.md: a standing letter to your assistant

### The idea

When you open Claude Code in a folder, it looks for a file called `CLAUDE.md` and reads it first — every single time, no matter what you're about to ask. Think of it as a one-page letter you've left on the desk for the assistant: *here's what this place is, here are the rules of the house, here's where things live*. The assistant doesn't have to be told all of that again; it's already on the desk when they walk in.

### Why bother

Without it, every session starts at zero on your project. You re-explain the directory layout, re-state the conventions, re-mention the thing-that-must-not-be-touched. Halfway through the third re-explanation in a week, you realise you've been describing the same workspace over and over and the assistant still doesn't know it.

With it, the assistant arrives already oriented. The first minute of every session — the re-onboarding minute — disappears. Multiplied over a year of sessions, that's real time.

### Where the file lives

There are two scopes, and you can use both:

```
~/.claude/CLAUDE.md              ← user-wide; applies to every session anywhere
your-project/CLAUDE.md           ← project-only; applies when you open this folder
```

The user-wide file is for things that are true about *you* regardless of project: how you like to be talked to, your preferred file formats, any rule that should hold everywhere. The project file is for things specific to that project: the layout, the glossary, the gotchas.

Both files are loaded together when you open the project. The project file extends the user file; it doesn't silently overwrite it.

### What earns a place in the file

| Belongs in CLAUDE.md | Does not |
|---------------------|----------|
| Two-line description of what this project is | A full description of every directory |
| The three or four commands you actually run | Every command anyone could possibly run |
| House conventions (naming, file organisation) | Things explained well by the code itself |
| Domain glossary — terms with specific meaning here | A textbook on the domain |
| A few gotchas that have bitten before | Every conceivable gotcha |
| Pointers to the rest of your setup ("Memory lives at…") | The full contents of those other places |

The discipline is **length**. Every word in CLAUDE.md costs you context budget on every session, whether or not today's task needs that word. Aim for fifty to a hundred and fifty lines. If you're over two hundred, start cutting.

### A starting template

```markdown
# Project: [Name]

## What this is
[One or two sentences. Why this folder exists.]

## Where things live
- `src/` — main code
- `docs/` — written material
- `data/` — datasets

## Commands I actually run
- Build: `make build`
- Test: `pytest tests/`
- Deploy: see `/deploy` skill

## Gotchas
- The staging server runs on a different database than production.
  Always confirm which one you're talking to.

## Pointers
- Memory: `~/.claude/projects/this-project/memory/MEMORY.md`
- Skills: `.claude/skills/`
```

Ten or twenty lines is a fine starting size. Grow it by noticing the things you keep re-explaining and adding them one at a time.

### Behavioural defaults worth setting

The template above is about *facts* — what the project is, where things live. The other thing a CLAUDE.md earns its keep on, especially the user-wide one, is **behavioural defaults**: a short list of standing instructions about *how* you want the assistant to act. These matter more than any single project fact, because they shape every task instead of one.

A handful that have proven worth setting:

| Default | What it says |
|---------|--------------|
| **Act when authorised** | Solve the problem and drive to the finish. Ask first only when a step is hard to reverse, genuinely undecided, or touches shared infrastructure. |
| **Stay in lane** | Do the thing asked. A side-observation is not a new task — acknowledge it in a sentence; don't start building it. |
| **Search before asking** | Before asking for something, look for it first — in memory, in the files, in the place it would already be. Don't make me re-supply what's on disk. |
| **Calibrate confidence** | Label what you haven't verified. Flag the risk up front. Don't fold the moment I push back if you're right. |
| **Lead with the answer** | When I ask a direct question — yes/no, who owes whom, how much — put the answer in the first sentence, then the supporting breakdown. A correct table I still have to read the answer out of hasn't answered the question. |
| **Evidence before "done"** | Don't report a thing fixed until you've checked the symptom is actually gone — and say what you checked. |
| **Discussion mode vs execution mode** | When the conversation has been evaluating an approach, an imperative like "run the migration" may mean "test this" — not "hit live now". Read prior context; if ambiguous, one short confirm before a write that cannot be easily undone. |
| **Session rules stay binding** | A method instruction or classification stated early in a session is a session-scoped rule, not a one-time answer. Don't drift back to default heuristics as the session lengthens — scan prior turns before applying defaults to any new instance of the same pattern. |
| **Trust the operator on physical facts** | When tool output (MAC tables, sensor counters, register reads) appears to contradict what the user says about their own physical environment, ask one clarifying question — don't assert the user is wrong. Remote data has context only the on-site person knows. |
| **Sanity-check results against known context** | Before reporting a measurement as a finding, check it against what's already known — geography, host state, time of day. An implausible number (LAN-grade latency to a server on another continent) is a signal to investigate, not a result to report. |
| **Ask why the primary path is out — first** | When work is running on a fallback — a backup link, a secondary tool, a workaround config — establish *why* the designed path isn't in use before engineering around the fallback. The reason usually changes the whole answer; one question up front beats a scaffold built around the symptom. |
| **The target is the deliverable** | When work is built *for* a specific device or surface, "done" means working there. A stand-in — "it runs in the browser", "here's the same thing as a web page" — is at most a temporary aid while the real target is being fixed, never the delivered answer unless the user explicitly accepts the downgrade. |
| **Finish the slice** | When the plan is agreed and work remains, work through to done — don't end each increment with "want me to continue?". And a standard follow-on step the assistant already holds the keys for — the DNS record, the certificate, the service registration — is part of the work, not an optional extra to offer back. Ship the whole vertical slice, not the eighty percent that leaves the user wiring the last mile. |
| **The question outranks the instruction** | When one message carries both an instruction and a question, answer the question first — it's the part blocking the user's next thought. Start the instruction as background work and report when it lands; don't serialise the human behind the delegated task. |

Two notes. These are *defaults*, not iron rules — the assistant can depart from them with reason; they set the resting behaviour. And the discipline from the next chapter applies here too: keep the set small, and phrase each as what *to* do. A pile of "never do X" defaults produces an assistant that asks permission to breathe. If your standing instructions have drifted to "ask before everything", that drift is the bug, not the safety net.

### What does *not* belong here

**Secrets.** This file is plain text on disk, almost certainly checked into version control at some point. API keys, passwords, tokens — none of these go in CLAUDE.md. They belong in a password manager or environment variable.

**Current task state.** "We're on step three of seven" is true today and stale tomorrow. That's plan-state (Chapter 6), not a standing instruction.

**Hard rules that must never be broken.** If the consequence of skipping a rule is real — a corrupted file, a deleted dataset, a leaked credential — that rule belongs in a Hook (Chapter 4), not in text the assistant *should* read but might miss when its attention is elsewhere.

### Failure modes

**The 5,000-word file.** It started at twenty lines and grew over a year into a reference manual. Now it loads on every session, eats context, and the assistant has learned to skim it because there's too much. Quarterly trim. Move stable knowledge to memory; move procedures to skills; move enforcement to hooks.

**Mixing user-wide and project-specific.** Your communication preferences end up in one project's file because that's where you happened to write them. Six months later you're in a different project and the assistant doesn't know them. Put cross-project content in the user-wide file. Put project content in the project file.

**Writing it like a README.** A README is for humans new to the project — it explains, motivates, walks through installation. CLAUDE.md is for the assistant — terse, directive, focused on what's needed to behave correctly. Conflating them produces a file that does neither job well.

### When to use this vs the other foundations

| If the thing is… | Put it in… |
|------------------|------------|
| Always-relevant context the assistant should arrive knowing | CLAUDE.md |
| Knowledge that accumulates and should be retrieved by topic | Memory (Chapter 2) |
| A procedure you'll invoke on demand | Skill (Chapter 3) |
| A rule that must hold regardless of what the model decides | Hook (Chapter 4) |

---

## Chapter 2 — Memory: knowledge that survives the session

### The idea

Memory is a folder of small text files that Claude reads at the start of each session. Unlike CLAUDE.md (which loads in full, every time), memory is *indexed* — Claude reads the index, then opens only the files relevant to today's task. It's the difference between leaving a one-page letter on the desk and giving the assistant access to a filing cabinet they can open by labelled drawer.

### Why bother

CLAUDE.md is short by design. Memory is where the bulk of your "what I'd otherwise have to re-explain" lives — your preferences, the lessons learned from past mistakes, the location of credentials, the quirks of a vendor's API, the decisions already made on each active project.

A memory store that started small at week one feels indispensable by month six. The compounding is real: every session adds a tiny bit of accumulated knowledge that all future sessions can draw on.

### The four kinds of memory

There are exactly four types, and the distinction matters because each type behaves differently as it ages.

| Type | What goes here | Example |
|------|----------------|---------|
| **user** | Who you are and how you prefer to work | "I want concise answers and bullet points only when they help." |
| **feedback** | A lesson learned from a mistake — what went wrong and the rule to apply next time | "When I ask for a summary, don't add a 'next steps' section unless I asked." |
| **project** | Where files live for an ongoing effort, decisions already made, integrations in use | "The kitchen reno is in fit-out phase; cabinets arrive Friday; certifier needs 48h notice." |
| **reference** | Stable external facts you'd otherwise have to look up | "Vendor X's quoting endpoint is at /api/v3/quotes, not /quotes." |

The two types you'll use most are **feedback** and **project**. Feedback compounds — every mistake you bother to write down is a regression prevented across every future session. Project files are where the running context of "where am I on the kitchen reno / book draft / consulting engagement" sits.

### How it's organised

The store lives at `~/.claude/projects/<some-slug>/memory/`. Inside that folder:

```
memory/
├── MEMORY.md              ← the index (one row per file)
├── me.md                  ← a user file
├── feedback_concise.md    ← a feedback file
├── reno_kitchen.md        ← a project file
└── vendor_x_api.md        ← a reference file
```

`MEMORY.md` is a table. Each row is one file: short description, hashtags, link. Claude reads this index first and uses the hashtags to decide which other files to open.

```markdown
| File | Description | Tags |
|------|-------------|------|
| me.md | Who I am, output preferences | #user #prefs |
| feedback_concise.md | Don't add unrequested "next steps" sections | #feedback #style |
| reno_kitchen.md | Kitchen reno — phase tracker, vendors, dates | #project #renovation |
| vendor_x_api.md | Quoting endpoint quirks at Vendor X | #reference #api |
```

Each file has a short header at the top (called frontmatter) and then a body:

```markdown
---
name: Kitchen Renovation
type: project
tags: [renovation, kitchen]
---

# Kitchen Renovation

Phase: Fit-out (started Mon 12 May)
Cabinets: ordered, delivery Fri 23 May
Certifier: 48 hours notice required for any change.
…
```

### How to start

You don't need all four types on day one. The right order is:

1. **One `user` file.** Call it `me.md`. Put in it: who you are in a sentence or two, your preferred output style, any rule that holds across everything you do. Five to ten lines is enough.
2. **One `project` file** for whatever's most active. Where things live, what decisions are settled, what's outstanding. Ten to twenty lines.
3. **A `feedback` file the first time the assistant does something you want it to stop doing.** Write it the moment the friction happens, while it's fresh. Short header explaining what went wrong, short "do this instead" rule.
4. **A `reference` file the second time you find yourself looking up the same external fact.** Once is fine; twice means it belongs in memory.

Claude reads `MEMORY.md` automatically when it's present. If you want certain files loaded on every session regardless, that's what CLAUDE.md is for — point at memory and let the index do the rest.

### Failure modes

**Saving things the codebase already knows.** A note saying "the main function is in `src/app.py` on line 42" is duplicating what `grep` would tell you in less time than it took to write the note. The codebase moves; the note doesn't. Save decisions, conclusions, and external facts. Don't save things the project itself can answer.

**Stale "current state" memory.** "We're in fit-out phase, cabinets arrive Friday" is true this week and wrong next week. That kind of state belongs in a plan file (Chapter 6), not memory. Memory carries policies and standing facts; plans carry progress.

**Index bloat.** Every entry in the index adds a tiny bit of cognitive overhead on every session. A 25-file index that's been pruned beats a 60-file one with 20 stale files. Skim quarterly; archive what's no longer relevant.

**Two files saying nearly the same thing.** They will drift apart. Pick one canonical home for each piece of knowledge and point from the other if you need to.

**Defensive-rule pileup.** Every time the assistant does something you don't like, the natural move is a feedback file saying "don't do X." Each rule is reasonable on its own. Cumulatively, they bias the assistant toward inaction — a session opening with thirty "don't do X" rules and one "default = ask before doing anything" arrives at every task already half-paralysed. The symptom: each new feedback file becomes a *carve-out* from a default that has grown too cautious ("for this kind of work, commit without asking" — i.e. the default has become "ask before committing", which is itself the bug). When you see that pattern, rewrite the default rather than stacking another carve-out. Audit the feedback directory every few months: retire rules whose lesson is now obvious, merge near-duplicates, and watch for the carve-out signal. The rewrite itself is usually small and the change immediate — *read and report; ask first* becomes *act when authorised; ask only on the hard-to-reverse, the undecided, or the shared* — and the half-paralysis lifts inside a session.

**Memory without provenance.** Every fact in the store should trace back to where it came from — something you said, a document on disk, or a decision the two of you made together. The hazard is the unsourced guess: filled in once, written down, and then treated by every later session as established fact. A fabricated detail doesn't sit still — it propagates through everything derived from it. Cite the source, and mark anything inferred *as* inferred. This bites hardest in your own voice: one invented biographical detail will resurface in documents you never re-check.

**A rich store the assistant never opens.** The quietest failure of all: everything is recorded — the working pipeline, the component that already does ninety percent of what you just asked for — and the assistant builds a parallel system from scratch anyway, because it never read the index before starting. The cost isn't a wrong fact; it's a wasted session of duplicate work and a second system to maintain forever. The fix is a standing default worth writing down: *at the start of any build task, read the index, list the existing pieces that already solve part of it, and design the change as the smallest delta on those.* The moment the assistant is about to author a new service, protocol, or pipeline that parallels one already in the store, that's the signal to stop and extend the existing one instead. A memory store pays rent only when it's consulted at the moment of decision — a filing cabinet nobody opens is indistinguishable from an empty one.

### A worked example

A researcher writes a doctoral thesis over eighteen months. She makes a `user` file noting she prefers inline citations over footnotes and wants her claims flagged when evidence is thin. She makes a `project` file describing her research question, the structure of her argument chapters, and the location of her bibliography database.

Three months in, she adds a `feedback` file: when she asks for "a more careful tone", Claude over-qualifies; the rule is "tighten the hedges, don't add new ones". A few weeks later, another feedback file: a particular statistical method was questioned by her supervisor; only use it when the dataset meets condition Y.

A `reference` file holds her department's style guide — specifically, the edge cases she keeps re-looking-up (figure caption format, citing unpublished conference proceedings, word-limit rules).

By month twelve, every session opens already knowing her preferred citation style, the structure of her argument, which statistical decisions are settled, and which writing patterns she's already corrected. The session begins at the level of a collaborator who's been alongside the project from the start, not a fresh assistant who needs re-onboarding.

---

## Chapter 3 — Skills: one-command procedures

### The idea

A skill is a small file that bundles three things: a name (the slash-command you type, like `/style-pass`), instructions for what to do when called, and a description that tells Claude when to use it. Once you've written a skill, you can invoke it explicitly (`/style-pass on the last section`) or Claude can invoke it automatically when your prompt matches its description.

### Why bother

Without skills, multi-step procedures live in your head or in old transcripts. You re-explain the same sequence every session, details vary each time, the assistant drifts from your intent. Skills convert "something I worked out once" into "something we repeat reliably". When Claude reads its skill library at the start of each session, it sees the procedures available and can reach for one without being told.

### What a skill looks like

A skill is a folder containing a single `SKILL.md` file:

```
~/.claude/skills/
└── style-pass/
    └── SKILL.md
```

The file has a short header and a body:

```markdown
---
name: style-pass
description: Apply house style to the current section — cap sentences at 28 words,
  flag passive constructions, normalise em-dashes, and check for blacklist
  transition words. Use when the user says "style pass", "clean up the prose",
  or after finishing a draft section.
allowed-tools: [Read, Edit]
---

# Style Pass

Run these checks in order on the section the user names:

1. Read the section.
2. Cap sentence length: any sentence over 28 words gets flagged and a
   shorter rewrite proposed.
3. Flag passive constructions in topic sentences.
4. Normalise em-dashes: " — " with spaces, never "—" with none.
5. Scan for blacklist transition words (very, really, basically,
   actually, simply, just).
6. Produce a change log. Wait for the user to confirm before
   saving any edits.
```

The header (frontmatter) controls metadata. The body is the procedure itself — write it like you're briefing a colleague who will do exactly what you've written, no more, no less.

### The description does double duty

The `description` field is the most important field in the file. It does two jobs at once:

1. It tells *you* (and future readers) what the skill does.
2. It tells *Claude* when to reach for the skill without being asked.

Vague descriptions like "useful for prose" never trigger automatically. The pattern that works: state what the skill produces, then list the literal phrases you might type when you want it. Over-specify. The system under-triggers more often than it over-triggers.

### Where skills live

Three scopes, picked by where the file sits:

| Scope | Location | When it's available |
|-------|----------|----------------------|
| User | `~/.claude/skills/<name>/SKILL.md` | Every session, every folder |
| Project | `your-project/.claude/skills/<name>/SKILL.md` | Only when you open this folder |
| Plugin | Distributed as a package | Wherever installed |

A project-scope skill with the same name as a user-scope skill takes precedence. Useful when you want a generic skill but override it for one specific project.

### A starter set worth building

The third-time test: if you've explained the same multi-step procedure three times across sessions, it belongs in a skill. Things worth starting with:

- **A morning brief.** "Pop the inbox, list anything urgent in the active project, and give me a one-line health check on the systems I care about."
- **A weekly review.** "Summarise the week's commits / notes / activity in the project; flag anything I said I'd do but haven't."
- **A finishing-touches pass on writing.** Style checks, citation format, the usual cleanup before a thing leaves your hands.
- **A deploy/release procedure.** The exact sequence of commands you run to push a change live. Document once; type `/deploy` thereafter.

### A second kind: process skills

The skills above are *procedures you invoke* — a deploy, a style pass, a sequence you'd otherwise re-type. There's a second kind worth knowing about: **process skills**, which encode *how to approach a class of work* and whose whole value is that they fire *before* the work, not during it.

A brainstorming skill that runs before you build any new feature, to pin down what's actually wanted. A test-first skill that insists the test exists before the code does. A debugging skill that makes you find the cause before proposing a fix. These are less "do this task" and more "here is the discipline for this kind of task" — and the discipline only works if it's consulted *before* you charge in. A process skill you reach for only after you've already picked an approach has done nothing.

You don't have to write these yourself. They increasingly ship as **plugin packs** — installable libraries of working practice — which is the Plugin scope from the table above, used in earnest. Reading a few well-made ones is also the fastest way to learn what a good skill looks like from the inside.

### How to apply it

1. **Notice the candidate.** Third-time rule.
2. **Draft the skill.** Write the file by hand or run the `/skill-creator` skill that ships with Anthropic's plugin pack — it interviews you about edge cases and produces a draft.
3. **Scope the tools.** Only list what the skill genuinely needs. A prose skill doesn't need shell access.
4. **Test the transcript.** Invoke it against a realistic scenario. Read the full back-and-forth, not just the final output, and look for missed steps.
5. **Tune the description** until Claude triggers it on the phrases you actually use.

### Failure modes

**Vague descriptions that never trigger.** "Useful for writing tasks" matches almost nothing. Name the output, list the trigger phrases, name the context.

**Skills that wrap a single command.** If the body is one shell command with no branching, you don't earn the maintenance overhead. Type the command directly.

**Skills that should be agents.** A skill that runs for forty-five minutes, fans out in parallel, or asks the user mid-procedure isn't a skill — it's an agent (Chapter 5).

**Hardcoded paths in a user-scope skill.** `/home/yourname/specific-project/outline.md` does the wrong thing everywhere else. Use relative paths or arguments.

### Skill vs hook vs subagent

| If the thing… | …it's a |
|---------------|---------|
| Must fire automatically on a system event (session start, file write) | Hook (Chapter 4) |
| The user invokes on demand | Skill (this chapter) |
| Is long, parallel, or needs a specialist with its own tool kit | Subagent (Chapter 5) |

---

## Chapter 4 — Hooks: rules your assistant cannot skip

### The idea

A hook is a small script that fires automatically at specific moments in a session — before any file is written, after a tool runs, when the session starts, when the assistant finishes a turn. It runs in your shell, as you, deterministically. If it exits with code zero, the event continues; if it exits with anything else, the event is blocked.

Hooks are the difference between *telling* the assistant to follow a rule and *making* the rule happen. CLAUDE.md text can be skimmed when context is crowded. A hook cannot be skimmed. It runs every time.

### Why bother

Some rules need to hold every time, no exceptions. "Never write to the production database directly." "This folder of documents is frozen — no edits without approval." "Send me a notification when a long job finishes." These are not preferences; they're invariants. Putting them in CLAUDE.md gives you the appearance of safety. Putting them in hooks gives you the substance.

### When hooks fire

| Event | When it fires |
|-------|----------------|
| `SessionStart` | Once, immediately after the session opens |
| `UserPromptSubmit` | Each time you submit a message, before Claude processes it |
| `PreToolUse` | Before any tool call (you can scope to specific tools) |
| `PostToolUse` | After a tool call returns |
| `Stop` | When the assistant finishes a turn |
| `SubagentStop` | When a subagent finishes a turn |
| `Notification` | When Claude emits a user-facing notification |

`PreToolUse` and `PostToolUse` can be scoped to specific tools, so you can have a hook that fires only on file writes, or only on shell commands, or only on a particular external integration.

### What hooks are most useful for

| Use case | Event | Effect |
|----------|-------|--------|
| Inject today's date and one-line status | `SessionStart` | Assistant arrives knowing what day it is and recent state |
| Block writes to protected paths | `PreToolUse` (Write/Edit) | Frozen files literally cannot be edited |
| Send a notification when a long task finishes | `Stop` | You get pinged when something done; no need to watch the terminal |
| Append an audit log entry after a sensitive command | `PostToolUse` (Bash) | A record exists regardless of what the assistant decided |
| Refuse a "done / fixed / deployed" claim that shows no proof | `Stop` | The assistant can't sign off work it never verified |
| Re-inject your hardest rules, but only when a message reads as a terse order or a correction | `UserPromptSubmit` | The reminder lands exactly when the rule is most likely to be skipped — and stays silent the rest of the time |
| Stop secret values reaching the transcript | `PreToolUse` + `PostToolUse` (Bash) | Credential files can't be printed, and a leaked value is flagged the moment it appears instead of sitting unnoticed in the log |

### A minimal first hook

The cheapest useful hook is a `SessionStart` script that injects today's date — Claude doesn't otherwise have a reliable view of the current date unless you tell it.

```bash
#!/usr/bin/env bash
DATE=$(date '+%Y-%m-%d')
cat <<EOF
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Today is $DATE."
  }
}
EOF
```

Saved as a file, made executable, and wired up in `~/.claude/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          { "type": "command", "command": "/path/to/the/script" }
        ]
      }
    ]
  }
}
```

From this point forward, every session opens already knowing today's date.

### A protective hook

A more useful pattern: a `PreToolUse` hook on `Write` and `Edit` that checks the file path and blocks the operation if it points at a frozen directory.

```bash
#!/usr/bin/env bash
PAYLOAD=$(cat)                                          # the tool call arrives on stdin
TARGET=$(echo "$PAYLOAD" | jq -r '.tool_input.file_path')
case "$TARGET" in
  "$HOME/research/approved/"*)
    cat <<EOF
{
  "decision": "block",
  "reason": "This document is frozen. To edit it, move it back to drafts/ first."
}
EOF
    exit 0
    ;;
esac
exit 0
```

Every attempted write goes through this check. The assistant cannot edit frozen documents, not because it was *told* not to, but because the harness physically stops the write.

### A pair of hooks for secret hygiene

"Never print credential values" is the canonical example of a rule that keeps being broken as text. It sits in the standing instructions, the assistant means well, and then one day it `cat`s a config file to check a hostname and a live API token rides along into the transcript. The transcript is a document — logged, synced, sometimes shared — so the moment a value is printed, it's exposed, and a redaction step that "should have" caught it fails silently exactly once too often.

The enforcement is a pair of hooks on shell commands:

- **Prevention (`PreToolUse`).** Deny any command that pipes a known secret file — key files, credential stores, token caches, `.env` files under a secrets directory — to a printing tool (`cat`, `grep`, `jq`, and friends). Allow-list the safe handlers: checksums, file moves, `stat`, and `source` (which loads values into the environment without displaying them).
- **Detection (`PostToolUse`).** Scan command *output* for credential shapes — provider token prefixes, `BEGIN PRIVATE KEY` headers, URLs of the form `scheme://user:password@host`. On a hit, block with an instruction to treat the value as compromised: rotate it, don't re-run the command.

Pair them with a sanctioned reader — a small script that prints any file with secret-shaped values replaced by a length-and-fingerprint placeholder — so there is always a legitimate way to inspect a config, and the hook never becomes an obstacle to route around. Prevention makes the mistake structurally impossible; detection makes the residual failure loud instead of silent. Neither depends on the assistant remembering anything.

### Failure modes

**Encoding a real rule as text instead of a hook.** "Never write to the production database" in CLAUDE.md is a wish. The same rule in a `PreToolUse` hook is enforced. The test: would it matter if this rule were skipped *once*? If yes, make it a hook.

**Overbroad matchers.** A hook that blocks all writes to a directory will also block writes the assistant legitimately needs to make. Be precise; include a bypass mechanism (a one-shot unlock file, a flag) so legitimate work isn't permanently stuck.

**Context-window bloat from SessionStart.** A hook that injects a giant document on every session start eats budget that could go toward actual work. Keep injected context to a few lines.

**Host-specific hooks without environment checks.** A hook that calls a tool only available on one machine will fail silently or noisily on every other machine where the same `settings.json` applies. Either check for the dependency inside the hook, or scope the hook to the project that needs it.

**Shared hook state that leaks across sessions.** The moment a hook writes a file — say, a flag that unlocks a guard for one operation — that file is shared by every session running at once. Give it a fixed name and two sessions collide: a one-shot unlock you granted in one terminal satisfies a guard in another, or a flag left by a since-dead session blocks a live one. Put the session's ID in the filename, so a bypass stays where you granted it.

**A guard that fires once, then goes silent for the rest of the session.** A detection hook that blocks the *first* offence and then stays quiet feels tidy — it isn't nagging. But the offence it catches is rarely a one-off: a session that claims something done without proof once tends to do it repeatedly as it lengthens, and those later claims are the ones that slip through unseen precisely because the guard already "did its job." Reading such a guard's own log back over several long sessions shows the pattern plainly — one early block followed by a cascade it never stopped. The fix is a per-session counter in the state file: re-arm on the first offence and every Nth after it (first, fifth, tenth), so the guard keeps its bite through exactly the long sessions where discipline slips most. A hook that can only interrupt once is a hook that stops working the moment it's needed twice.

### Finding which hooks are worth building

The hooks above are examples. The ones *you* need are hiding in your own history — in the moments you had to correct the same thing twice.

The transcripts of your past sessions are on disk. Read back over a month of them — or, better, point the assistant at them and ask it to cluster the moments where you pushed back, corrected, or repeated yourself, by *what went wrong* rather than what the task was. The pattern that comes back is rarely "it can't code." It's behavioural and repetitive: claimed something was done when it wasn't, did work you didn't ask for, kept asking permission you'd already given, leaned on a stale note instead of checking the live system. Those clusters are your hook backlog, ranked by how often they cost you.

Two of the most valuable hooks come straight out of that exercise, and neither is a path-blocker:

- **A `Stop` guard that refuses an unproven claim.** It reads the assistant's final message; if it asserts *done / fixed / deployed / working* but the same message shows no evidence — no command output, no status code, no commit hash, no figure — it blocks and asks for proof or an honest "I couldn't verify this." "It works" stops being something the assistant can say for free. (See the re-arming note in the failure modes below — a guard like this must *not* fire only once per session.)
- **A `UserPromptSubmit` injector that fires only on heat.** Most of the time it stays silent. But when your message reads as a terse imperative or a correction — *just do it, I already told you, stop asking* — it prepends your hardest-won rules to that turn. The discipline arrives exactly where the record shows it tends to slip, and costs nothing on the calm turns.

Why hooks and not more CLAUDE.md prose? Because a rule the model reads is a rule it can rationalise past under pressure; a rule the harness enforces is one it cannot. If you find yourself adding the same line to your standing instructions for the third time, that's not a documentation gap — it's a hook waiting to be written.

### The three-way choice

| When you need… | Reach for… |
|----------------|------------|
| A rule the model *must* obey, every time | Hook |
| A standing piece of context the model *should* have | CLAUDE.md |
| A procedure the user invokes on demand | Skill |

A reminder belongs in CLAUDE.md. An invariant belongs in a hook. A repeated action belongs in a skill.

---

## Chapter 5 — Subagents: delegate the heavy lifting

### The idea

A subagent is a second copy of Claude you can hand a specific task. It arrives with no memory of your conversation, carries only the tools you've permitted it, and may run on a different model than your main session. You write its briefing once and store it as a file; from then on, your main session can call it by name whenever that kind of work appears.

The main session orchestrates — it holds the plan and the judgement calls. The subagent executes a bounded task and reports back. The separation is not a courtesy; it's the structural reason subagents are useful at all.

### Why bother

Three reasons:

1. **Context hygiene.** Every tool call that returns a large result — a long log file, a directory full of documents, a database query — lands in your context window and stays there. A subagent does the heavy reading and returns only the distilled answer. Your main session holds reasoning; the subagent absorbs the noise.

2. **Parallelism.** Three independent research questions can run at the same time, finishing in the time the slowest takes. A single session can't do that for itself.

3. **Specialisation.** An agent briefed as a domain specialist is less likely to drift than a general session handling one more thing at the bottom of a long thread. The brief is the agent's whole world; that focus is a correctness advantage as much as a speed one.

### What a subagent looks like

A subagent is a Markdown file at `~/.claude/agents/<name>.md`:

```markdown
---
name: research-analyst
description: Use this agent for literature searches, citation checking, and
  summarising sources on a given topic. Invoke when the task is "find what is
  known about X" rather than "decide what to do about X".
tools: [Read, Write, Bash]
model: sonnet
---

You are a research analyst. When given a topic and a source archive:

1. Search the archive for relevant material.
2. For each source found, capture: title, author, date, key claims,
   and your assessment of evidence strength.
3. Write the structured summary to the output path the brief gives you.
4. Do not synthesise or recommend — that's the orchestrator's job.

If a source is paywalled or unreadable, note it but don't pretend you
read it.

Always cite the file path of each source you used.
```

The frontmatter defines the agent. The body is its persistent briefing — its role, the conventions it follows, the rules it applies when it hits something unexpected.

### Tool allowlists matter

A research agent that reads files and runs searches doesn't need `Write` or shell access. A formatting agent doesn't need `Bash`. Tight allowlists mean three things: less risk if the agent misinterprets its brief, faster invocation (less to load), and clearer intent — the allowlist documents what the agent is supposed to touch.

### Picking the right model

| Model | When |
|-------|------|
| Haiku | High-volume mechanical work — extracting structured data, formatting, simple classification |
| Sonnet | Standard professional work where judgement matters |
| Opus | Reasoning-heavy work where getting it wrong is expensive — legal analysis, architecture, subtle debugging |

Running N parallel Haiku agents to summarise N documents costs a fraction of a single Opus call and often produces equivalent results.

### The brief is half the job

The agent definition is permanent. The **brief** is what you pass at invocation time — the specific task right now. A good brief looks like:

```
Goal: One sentence saying what "done" looks like.
Input: Exact file paths or data — not "the report" but "/path/to/report.md".
Output: Format and destination — "Write findings to /path/to/findings.md
        as a structured list."
Constraints: Things not to do, word limits, style.
If stuck: Report back rather than guess.
```

A vague brief produces vague work. The agent cannot ask you a clarifying question mid-task unless it's designed to do so, so the brief must be self-contained.

### When to delegate vs do it yourself

| Situation | Reach for… |
|-----------|------------|
| Task fits in three lines, output is small | Do it inline |
| Output will be large (and you don't want it cluttering context) | Subagent |
| Task is one of several independent things | Subagent (in parallel) |
| The work has a specialist angle you've defined an agent for | Subagent |
| It's a mechanical, repeatable sequence with no judgement | Probably a Skill, not an agent |

The break-even point for delegation is roughly thirty to sixty seconds of careful effort. Below that, do it yourself; agent invocation overhead exceeds the gain.

### Fan-out: N tasks in parallel

When you have N independent subtasks of the same kind — summarise these N documents, draft these N sections, check these N references — spawn N agents in one go.

```
                                  ┌────────┐
                                  │ Main   │
                                  │ session│
                                  └───┬────┘
                                      │
                ┌──────────┬──────────┼──────────┬──────────┐
                ▼          ▼          ▼          ▼          ▼
            ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
            │ agent  │ │ agent  │ │ agent  │ │ agent  │ │ agent  │
            │   1    │ │   2    │ │   3    │ │   4    │ │   5    │
            └────────┘ └────────┘ └────────┘ └────────┘ └────────┘
                │          │          │          │          │
                └──────────┴──────────┴──────────┴──────────┘
                                      │
                                      ▼
                                  ┌────────┐
                                  │ Main   │
                                  │ reads  │
                                  │ outputs│
                                  └────────┘
```

A few rules for fan-out:

- **Validate the outputs.** Read what the agents actually produced before treating it as done. Confident-sounding output is not always correct output.
- **Watch for sibling collisions.** If the agents share a design space — they must produce distinct domains, consistent naming, coordinated structure — flat fan-out without coordination causes overlap. Two agents picking "the same obvious example" independently. The fix is a **manager agent** that assigns scope to each worker before any of them begin.

### Failure modes

**The terse brief.** "Fix the formatting issues in the report" produces shallow work because the agent must guess what the standard is, where the issues are, and what good looks like. Output quality reflects brief quality.

**Over-delegation of trivial tasks.** Spawning an agent to rename a variable or change a date is slower than doing it inline. Agent invocation has overhead.

**Serial fan-out.** Launching agents one at a time when they're independent wastes the whole point of the pattern.

**Trusting the summary.** An agent that says "done, all three sections updated" might have updated two correctly and one incorrectly. Read the diff yourself.

**Building a subagent for what should be a skill.** If the "agent" is a fixed sequence of commands with no judgement calls, it's a skill. Subagent = packaged expert; skill = packaged procedure.

---

# Part 3 — Composition

The foundations work on their own. The composition chapters describe how to combine them into real workflows.

---

## Chapter 6 — The persistence ladder: state at the right scope

### The idea

Information you produce in a session lives at one of four scopes: within a single response, across this conversation, across all conversations, or across parallel branches of work. Each scope has a natural home, and each carries overhead proportional to how durable it is. The discipline is picking the smallest scope that genuinely fits.

| Scope | Home | Lifetime |
|-------|------|----------|
| Within one response | Todo list (`TodoWrite`) | Dies with the session |
| Across sessions, one project | Plan file (`~/.claude/plans/<slug>.md`) | Lives as long as the project |
| Across projects, across time | Memory store | Indefinite, until you archive |
| Parallel branches of work | Worktree / sandbox copy | Until merged or discarded |

### Why bother

When you store the wrong thing at the wrong scope, two failures occur in opposite directions. Putting plan-state into memory means every future session loads stale progress into context. Putting durable conventions into a session-only todo list means they evaporate by tomorrow. Neither failure announces itself loudly — you just gradually notice things drifting.

### Todos: in-session only

The `TodoWrite` tool maintains a checklist that Claude tracks within the current conversation. Use it freely for the sequence of steps in front of you right now — call the plumber, draft the variation notice, confirm the inspection.

When the session ends, the list ends. That's the design. Don't treat a todo list as a deliverable, a decision log, or anything Claude should remember next time.

### Plans: cross-session, one project

A plan is what a todo list becomes when the work spans more than one session, requires a decision between phases, or has dependencies worth reasoning about in advance.

```
A todo answers: what am I doing right now in this session?
A plan answers: what are the phases, in what order, and what does "done"
                mean for each?
```

Save plans to a known location — `~/.claude/plans/<slug>.md` is the convention. Not in `/tmp`, not in a session buffer. The plan is the artefact: it lives as long as the work lives, and gets archived when the work is done.

### Memory: durable across projects

Memory (Chapter 2) carries policies and standing facts, not progress. The test is one question: "Will I want this in a session that has nothing to do with the current work?"

- Yes → memory.
- "Only while this project is active" → plan or project file.

The classic mistake is writing plan-state to memory — "currently in fit-out phase, cabinets arrive Friday" — which is wrong by next week and poisons every session that loads it.

### Worktrees / sandboxes: parallel branches

If your work is code, a git worktree is a second checked-out copy on a different branch. You can experiment without touching the mainline; merge or discard the result.

If your work is documents, the equivalent is a sandbox copy: a separate folder holding an experimental variant while the authoritative version stays untouched.

Use worktrees when you'd otherwise risk clobbering or contaminating finished work. The overhead is real — you eventually have to reconcile or delete — so don't reach for one for a small in-place edit.

### Applying the ladder

The default walk for any new piece of work:

1. **Start with todos.** Open the session, scope the task, let Claude track the steps. If the work finishes in one session, you never climb higher.
2. **Promote to a plan** when the work spans sessions or needs a sign-off between phases.
3. **Persist to memory** only when a decision has proven to generalise beyond this project.
4. **Branch a worktree** when you'd contaminate the mainline by working in place.

### Failure modes

**Promoting todos to permanent documents.** If a list is worth saving, rewrite it as a proper plan with phases and success criteria — not as a copy of the in-session checklist.

**Plans for one-session work.** A five-phase plan for "call the plumber" is overhead. Plans pay off only when sessions or sign-offs are genuinely involved.

**Plan-state in memory.** "Phase 2 complete, awaiting certification" is plan-state. Loading stale progress into every subsequent session contaminates them all.

**A worktree for a trivial edit.** The overhead of a second branch is only justified when isolation is genuinely needed.

**Two retention windows, and the shorter one runs upstream.** An archive job that sweeps everything older than ninety days sits downstream of a tool whose built-in cleanup deletes the same material at thirty. Every item is purged two months before the sweeper would have collected it — the archive stays nearly empty indefinitely, and nothing errors, because deletion is a default and defaults don't announce themselves. When you build anything archival, enumerate every cleanup already acting on the source — the harness's own retention setting first — and make the upstream window longer than the downstream sweep, or disable it. The audit is one check: if the oldest surviving item is exactly as old as some tool's default retention period, that tool is winning.

### A homeowner's renovation

Month one: a homeowner uses `TodoWrite` to track each day's site work — confirm skip-bin delivery, photograph existing walls, call the certifier. The lists do their job and are gone by evening.

Month two: scope has grown. Three phases, two hold points for sign-off, a materials schedule tied to lead times. She writes a plan to `~/.claude/plans/kitchen-reno.md` with labelled phases. Each session begins by reading the plan.

Month four: she notices she's restating the same conventions at the start of every session — variation notices follow a specific format, trades get 48 hours' written notice before any schedule change. These are policies, not plan-state. She moves them into a memory entry.

When the builder suggests moving the island bench 600mm — a change that might void the tile order — she doesn't edit the confirmed plan. She makes a sandbox copy and works through the implications there. The change doesn't survive scrutiny. She discards the sandbox. The authoritative plan is untouched.

---

## Chapter 7 — Async: work that runs while you sleep

### The idea

You're not always at the keyboard. A mature setup builds that assumption in rather than hoping you'll be there. The async layer has three pieces: outbound notifications (something pings you when a task completes), inbound inbox (you can drop a message in from your phone that the next session picks up), and background runs (long jobs that don't block your main session).

### Why bother

Long-running work without notifications forces a choice: park yourself at the terminal or check back hours later to find it either finished cold or errored on step two. An inbound inbox solves the symmetric problem: thoughts that occur away from the machine evaporate before the next session starts unless you have somewhere to put them.

Without the async layer, Claude Code is a synchronous command prompt. With it, it's a delegatable agent that works while you move and sleep.

### Outbound notifications

The simplest form is a one-line shell wrapper around your preferred push channel — Telegram, Pushover, ntfy.sh, an email gateway, anything you actually check.

```bash
notify "Asset bake complete — 12 levels processed, 1 flagged for review."
```

Keep the messages substantive. "Done" is useless. "Done — 0 failures, output at /path/to/report" is actionable. A notification is a state-transition signal — task complete, decision needed, long job starting — not activity noise.

### Inbound inbox

A persistent queue you can append to from anywhere — your phone, another machine, a web form. The next Claude session pops messages off it before starting other work.

```
[09:14, from phone] If the lighting pass on level 18 fails again,
                    skip it and flag it — don't block the whole bake.

[09:22, from phone] Jump-height values in levels 12–15 were rebalanced
                    today; note that in the manifest.
```

The queue must be persistent (not in-memory), capped (so it doesn't grow forever), and read non-destructively (so you can inspect it without popping entries). The assistant's job at session start is: check inbox, act on any messages, then proceed.

### Background runs

The Bash and Agent tool calls both accept a `run_in_background` parameter. Use it for any subprocess that will take more than a few seconds. The main session doesn't block; you get notified when it finishes.

Pair background runs with the **Monitor** tool, which streams events from a running background process. Each line of output becomes a notification, so you can watch a build log in real time without blocking the main session.

### Self-healing background runs

A background run doesn't have to just report — it can *guard*. When you make an outward-facing change that's risky to leave broken — flipping DNS to a new host, cutting over a deploy, repointing a live service — pair the change with a background watcher that verifies the desired outcome and reverts automatically if it doesn't materialise.

The shape: make the change, then launch a background loop that polls for success — the new site serving `200`, the health check green — and requires the signal to hold before it trusts it. If success arrives, the watcher exits clean. If the deadline passes first, the watcher runs the rollback itself — restore the old configuration, tear down the half-applied change — and reports what it did.

```bash
apply_change                                   # e.g. flip DNS to the new host
ok=0
for i in $(seq 1 30); do
  code=$(curl -s -o /dev/null -w '%{http_code}' https://site/)
  if [ "$code" = 200 ]; then ok=$((ok+1)); else ok=0; fi
  [ "$ok" -ge 2 ] && { echo "live on the new host"; exit 0; }
  sleep 12
done
rollback                                        # deadline passed — revert, don't leave it broken
echo "auto-rolled-back"; exit 1
```

This changes the risk calculus. A live cutover you'd normally babysit becomes fire-and-forget with a safety net: the worst case is a bounded window, then automatic recovery — not a service left down until you happen to notice. You get the notification either way — "live on the new host" or "reverted, here's why" — so you're informed without standing watch.

Two disciplines make it trustworthy. Require the success signal to be *consistent* — two consecutive good readings, not a single lucky one near the deadline — so a transient blip doesn't declare false victory. And make the rollback *complete*: restoring the DNS record isn't enough if the cutover also registered the hostname somewhere that now blackholes it; the rollback has to unwind every side-effect, or the "safe" path is still broken.

### Pacing primitives

| Cadence | Tool |
|---------|------|
| Fixed schedule (nightly build, weekly review) | `cron` |
| Self-paced loops (poll until X happens) | `/loop` skill or equivalent |
| In-session "wake me in N minutes" | `ScheduleWakeup` |

For in-session waits, watch the prompt cache window. Roughly: under five minutes, the cache stays warm and re-entry is cheap; from five minutes to about an hour, you pay a cache-miss; longer than that, the cost is irrelevant. The awkward middle is a twelve-minute sleep on an eight-minute job — you cross the cache boundary for no reason. Either stay short or commit to a real pause.

### A nightly bake

A solo game developer runs a nightly asset bake — 40 level maps, sprite atlases, lighting pass, packaged build. Three to five hours, no reason to sit and watch.

She fires it at 10pm. The opening notification reads: "Starting nightly bake, 40 levels queued, estimated 3–4 hours." The export subprocess runs with `run_in_background: true`. The Monitor tool streams the log.

She drops two notes from her phone before bed:

> *If level 18 fails the lighting pass again, skip and flag it — don't block the bake.*
>
> *Jump-height values in levels 12–15 were rebalanced today; note that in the manifest.*

At the midpoint she gets a checkpoint: "20/40 baked, no failures. Atlas export next."

At 1am, level 18's lighting pass fails. The assistant checks the inbox, finds the standing instruction, skips, flags, continues. No one is woken.

At 5:30am the bake completes: "Done — 39/40 packaged, level 18 flagged, jump-height note added to manifest." She reads it over breakfast.

### When to ping vs stay quiet

Ping on:
- Completion of anything that took more than a few minutes
- Errors you can't resolve from standing instructions
- Natural checkpoints in multi-phase work
- "Starting now" heads-up for genuinely long jobs

Don't ping on:
- Routine intra-phase progress
- Decisions you can resolve yourself
- Anything that will finish before the human could read the notification

A quiet channel is a trusted channel. One substantive, well-timed notification beats five noisy ones.

### Failure modes

**Alert fatigue.** Notifications on every tool call mean you'll mute the channel within a day.

**Silent completion.** Opposite failure. The job finishes at 2am, you find out at 8am, half the day already gone.

**Polling loops that thrash the cache.** A `sleep 10` loop for a 20-minute process generates calls every ten seconds for no reason.

**Inbox messages without context.** "Fix the thing" is useless by morning. Each message needs enough context for a cold session to act.

**The async harness silencing the human.** When a background task is running, the assistant's bias toward "do the work, report back" can cause it to queue your new prompts behind the running task. A new message from you is always an interrupt. If the message has a question, answer it now.

**Waiting on a worker that already died.** A delegated agent that stops with "I'll continue when the build completes" has *ended its turn*. If the thing it was waiting on finishes without re-invoking it — or the agent dies mid-report — nothing resumes it and no error surfaces. The finished work sits orphaned on disk while the session that delegated it keeps "waiting for the worker to land," sometimes for hours. The discipline: when a delegated deliverable is pending well past its expected window with no notification, **poll the work state, not the worker** — look at the output files, their timestamps, the commit log in the target repository. If the work is done and the worker is gone, take over directly and finish it inline; don't re-delegate another relay hop. Two mitigations make the failure cheaper when it happens: have long-running workers commit early and often (work saved before a death survives it), and keep their final reports terse — a long closing summary is a known place for a worker to die with everything undelivered. And a closing rule for any delegated deliverable: it should land somewhere you can *see* — a URL, a rendered file, a screenshot in the reply. Work that exists only inside a repository you never open is indistinguishable from work that didn't happen.

---

## Chapter 8 — Multi-agent patterns: a second pair of eyes

### The idea

A single agent is fast but biased toward its first plausible answer. Once it commits, every subsequent step reinforces the direction rather than questioning it. A second agent briefed cold — meaning it hasn't seen any of the first agent's reasoning — can't anchor on a framing it never received. That structural independence is the point.

The cost is roughly linear in tokens. The quality lift, especially where a confident wrong answer is worse than a flagged uncertainty, is not.

### Why bother

A reviewer who didn't write the plan sees gaps the author assumed away. A second agent briefed cold is in exactly that position. This matters most for hard-to-reverse decisions and for judgement calls where "looks right" isn't the same as "is right".

Cheap verification you can do yourself — running tests, checking outputs, eyeballing a diff — doesn't need a second agent. When verification requires a perspective you cannot structurally take, add an agent.

### Five useful patterns

**1. Critic loop.** One agent produces; a second agent, briefed cold, critiques against an explicit rubric; the producer incorporates the critique; the critic re-checks. Set a ceiling — two or three rounds — before you start. The critic must receive only the output, never the producer's reasoning. A critic who sees intent evaluates effort, not result.

**2. Planner/executor split.** A reasoning-heavy planner (the most capable model) produces a structured plan. A cheaper executor carries out each step. Different bottlenecks: planning is reasoning-intensive and mistakes compound; execution is often mechanical once the plan is sound.

**3. Second opinion.** For a single high-stakes judgement — is this clause ambiguous? is this schedule feasible? — spawn a second agent with the same inputs and a brief that references nothing the first produced. Agreement raises confidence. Disagreement locates exactly where the question is genuinely hard.

**4. Parallel fan-out with synthesis.** N agents on N independent questions, then a synthesiser agent that produces a unified result. The synthesiser is briefed to reconcile contradictions and flag gaps, not just stitch outputs together.

**5. Build-and-grade.** A producer drafts; a grader scores against an explicit rubric; producer iterates; grader re-evaluates. The score makes convergence visible — you can see whether rounds are improving the work or spinning in place.

### When the shape is known: workflows

The five patterns above are things you drive *by hand* — you spawn an agent, read what it says, decide, spawn the next. That is exactly right while you're still feeling out a problem. But once the *shape* of the work has settled — fan out across this list, verify each finding, keep the survivors — you can hand the control flow itself to a script. A **workflow** is that script: the loop, the fan-out, and the branching written down as deterministic steps, with agents as the unit of work inside them. The agents still do the thinking; the workflow decides who runs when.

A small vocabulary, in plain terms, covers most of it:

- **Pipeline.** Each item runs through every stage on its own — one finding can be at the verify stage while another is still being discovered. Nothing waits for the slowest item at each step. This is the sensible default for staged work.
- **Barrier.** The opposite: collect every result from a stage before the next one starts. Right only when the next stage genuinely needs the whole set at once — to merge duplicates, or to stop early if the count came back zero.
- **Loop-until-dry.** Keep spawning finders until a round or two turns up nothing new. It's the honest way to size a search whose answer you can't know in advance — "find every problem" has no number you can write at the start.
- **Adversarial verify.** For each finding, spawn independent sceptics briefed to *refute* it, and keep only what survives a majority. This is the step that stops a confident-but-wrong result from reaching you wearing the same clothes as a correct one.
- **Judge panel.** Generate several independent attempts from different angles, score them, then synthesise from the winner while grafting in the best of the rest.

When to reach for a workflow: the work is large and its shape is known — audit every file, check every claim, review along several dimensions and fact-check each finding before it lands. When the shape *isn't* known yet, do the reverse — scout by hand, discover the work-list, *then* hand it to a workflow. Automating a guess only produces a great deal of confident guessing.

One posture is worth naming on its own: **exhaustive mode** — the deliberate choice to spend tokens buying confidence, fanning out wider and verifying harder than the answer strictly needs, because this particular decision is expensive to get wrong. It is the right call for the irreversible and the costly. It is the wrong default for a quick lookup, and treating it as the everyday setting just burns budget.

### A wedding plan

An event planner has drafted a 200-person wedding plan: venue logistics, catering, run-sheet from access to carriages, three vendor contracts, a risk register.

A single end-to-end review will miss cross-domain conflicts. The food-safety reviewer won't catch the clause in the venue contract that prohibits outside catering without a supplement.

Instead, parallel fan-out to five specialist critics, each holding the full plan but briefed cold on a specific domain: venue logistics, catering, run-sheet, contracts (instructed to cross-reference the others), and contingency (instructed to assume the three most likely failure modes). Each writes findings to a named output file.

Then a synthesis agent, briefed cold on the five critique files, looks for contradictions, repeated flags (real structural problems, not quirks), and a ranked list of blocking items by impact on the date.

The pattern earns its cost because the five sub-tasks are genuinely independent, domain-specific bias would cause a generalist to miss problems systematically, and the event date can't move. Where a confident wrong answer means a ruined wedding instead of an extra revision, the redundancy is cheap.

### Failure modes

**Critic loops that never converge.** No stop rule means the critic always finds something. Set a ceiling. Accept good-enough after three rounds.

**Planners that over-specify.** Specifying every micro-step leaves the executor no room to respond to what it actually finds. Plans should specify outcomes per step, not a rigid command sequence.

**Second opinions that share the first agent's conclusion.** "Agent A concluded X; what do you think?" is a request for validation, not a second opinion. The second agent must receive the same raw inputs as the first, nothing more.

**Parallel fan-out for dependent tasks.** Running B in parallel with A when B needs A's output produces error-embedded results that look complete and aren't.

**Sibling collisions in flat fan-out.** N parallel agents picking the same obvious example domain independently. The fix is a manager agent that assigns distinct scope before workers begin.

**Parallel sessions colliding in another failure's clothes.** Two sessions working the same codebase on one machine rarely fail with "another session interfered" — they fail as something else. A test suite dies mid-run with an out-of-memory-looking kill signal; the real cause is the sibling's test run tearing down the shared containers under it. A coordination registry is unreachable and fails *open*, so each session believes it holds the lane alone. A merge completes without a single conflict while silently dropping one branch's additions, because the other side rewrote the same files wholesale and auto-resolution took the rewrite. The disciplines: give each concurrent run its own namespace — test project names, ports, and a working copy each (a worktree per session, never a shared checkout); treat an unexplained kill signal as "check for a sibling" before debugging the code; and after any merge where the other side heavily refactored shared files, search the merged tree for your branch's key symbols before trusting it — a conflict-free merge is not a content-preserving merge.

**Critic monoculture.** Five critics all briefed with the same axis — all adversarial, all security-focused, all compliance-oriented — will collectively miss every failure outside that axis. At minimum, one critic should occupy the "use this as an actual operator would" angle — treating the work as a product to be used, not a specification to be verified.

**Adding agents to mask a bad brief.** A critic loop on bad input produces critiqued bad input. Sharpen the brief before reaching for a second agent.

**Orchestrating before you know the shape.** A workflow is for structure you can already name. Reach for one before you've scouted the work and you've only automated a guess — scout first, orchestrate second.

**Silent caps.** A workflow that quietly stops at the first handful of findings, or skips the re-check to save time, reads afterwards as though it covered everything when it didn't. If you bound the work, say what you left out.

### When to add an agent vs sharpen the brief

The first move is almost always to improve the brief. A second agent on a bad brief produces a second bad result. Add an agent only when one of three conditions holds:

1. **Independent perspective.** The work needs a viewpoint the original brief can't structurally provide.
2. **Real parallelism.** Sub-tasks are genuinely independent and wall-clock time matters.
3. **Cost of failure greatly exceeds cost of the extra agent.** A second-opinion call on an irreversible decision costs one model call; the alternative may cost much more.

If none of those holds, you need a better brief, not another agent.

---

## Chapter 9 — Tool discipline: pick the right hammer

### The idea

Every tool call has a cost — latency, tokens, context window space, sometimes a permission prompt — and a value, which is the information or change it produces. Tool discipline is the habit of reaching for the cheapest tool that delivers the needed value, and of batching independent calls into a single turn so the cache stays warm and the wall clock stays short.

Done well, this is invisible: the session finds what it needs quickly, changes only what it should, and leaves the context holding distilled information rather than noise.

### Why bother

Same task, wrong tools: slower, noisier, more permission prompts, more context consumed. That context is finite — it has to hold your reasoning, not raw file dumps. A session that uses `cat` instead of `Read`, serialises five searches instead of batching, or pulls a 30KB log into the main context, will feel sluggish compared to one that uses the right tool the right way.

### The hierarchy

**Dedicated file tools over shell equivalents.**

| For this… | Use this… | Not this… |
|-----------|-----------|-----------|
| Reading a file | `Read` | `cat` |
| Editing a file | `Edit` | `sed` |
| Creating / overwriting a file | `Write` | `echo > file` |
| Listing files by pattern | `Glob` | `find` |
| Searching file contents | `Grep` | `grep`-via-shell |

The dedicated tools render line-numbered output (auditable), produce structured diffs (reviewable), avoid most permission prompts, and refuse ambiguous edits (safer than `sed`). Bash is for genuine subprocess work: running a build, querying a live system, restarting a service.

**Parallel calls when work is independent.** If two or more tool calls don't depend on each other's results, issue them in the same turn. The runtime is bounded by the slowest call, not the sum.

```
# Bad: serialise
Grep("MyConfig", "/src")        wait...
Grep("MyConfig", "/config")     wait...
Grep("MyConfig", "/tests")      wait...

# Good: batch
Grep("MyConfig", "/src")
Grep("MyConfig", "/config")        ← all in one turn
Grep("MyConfig", "/tests")
```

**Subagent as a context buffer.** When a tool call would return a large payload — a full log, a directory listing, a bulk query result — ask whether you actually need all of it in the main context. If what you need is a summary, a count, or the answer to a specific question, delegate the retrieval *and* the interpretation to a subagent. The subagent does the heavy reading; you get back 200 words instead of 25 kilobytes.

**Right host, not just right tool.** Tool discipline extends to *where* tools run. If you have a fast-feedback orchestrator host and a separate heavy-compute executor, long-running work belongs on the executor. Builds, test suites, ETL — none of that should run on the host you're trying to keep responsive. Symptom: "everything feels slow" even though the executor is idle. Cause: running heavy work on the interactive host.

### Deferred tools and ToolSearch

Most tools are not loaded by default. Before reaching for a one-off `ToolSearch` to load a single tool, ask whether there's a logical bundle. A single search that names a toolkit returns the whole set in one round-trip. Loading tools one at a time is wasted overhead; loading more than you need wastes a different kind of overhead. Load the bundle for the domain you're entering.

### When to use which tool tier for an external system

| Tier | What it is | When |
|------|------------|------|
| Dedicated MCP | A purpose-built integration for a specific system | Always prefer if it exists |
| Browser MCP | Drive a browser to navigate and extract | When no dedicated MCP exists |
| Computer-use | Interpret pixels on the desktop | Last resort — fragile, slow |

Reach down the tiers only when the upper tiers are unavailable or insufficient.

### A research historian

A historian is working through several hundred digitised field notes spread across thematic subdirectories. She needs to find every reference to a specific surveying instrument, read the relevant passages, then edit a draft essay to replace an outdated name.

Her first instinct: open files one by one. `cat` the first directory's listings, read ten files in sequence, find two references. She's 10% through and her context is full of files that contained nothing useful.

She resets. One `Grep` call across the entire archive — recursive, with line numbers and context. 23 matches in 14 files, returned in a few hundred tokens. Then 14 parallel `Read` calls scoped to a narrow line range around each match. Her context now holds exactly the passages she needs. Finally, `Edit` with `replace_all` to rename the instrument throughout her essay: one call, no regex, a clean diff.

Three turns instead of several dozen. The context holds evidence and reasoning, not hundreds of lines of irrelevant material.

### Failure modes

**`cat` instead of `Read`.** No line numbers, no audit trail, permission prompts. Familiarity is the only winner.

**`sed` instead of `Edit`.** Blind regex replacement with no diff. `Edit` forces you to be explicit about what you're changing and fails safely when the target string isn't found.

**Serialising independent searches.** Pure dead time. "To be safe" is not safe; it's just slow.

**Pulling a large result into main context.** A 20KB log in the main context occupies space that should hold your reasoning. If you need "errors in this log", the log itself is not what you needed.

**Computer-use when a native MCP exists.** Pixel-based interaction breaks on layout changes. API-based interaction doesn't.

**Heavy work on the orchestrator host.** Push it to the executor where it belongs.

**Commissioning a bespoke tool when an adopted one exists.** Tool discipline applies to what you ask the assistant to *build*, not just what it reaches for in a session. An assistant this capable will cheerfully build you a custom dashboard for anything — and the dashboard is great for the week after it ships. Then something moves, the hand-maintained list behind it lags reality, and it quietly stops being opened. The failure isn't the tech stack; it's that it's bespoke at all. Before commissioning a status surface or ops tool, ask what you would honestly open every day — if the answer maps to an existing, actively-maintained tool, adopt that instead. Build custom only when nothing adopted covers the need *and* the result can derive its data live from an existing source of truth, rather than from a list someone has to keep updating.

### A short rule of thumb

Use the most specific tool that does the job. Batch every independent call into the same turn. Route large outputs through a subagent and bring back only the derived result. Load deferred tool bundles once, not one tool at a time.

---

# Part 4 — Putting It Together

## A walked example: Alex and the consultancy

Alex runs a one-person IT consultancy serving six small manufacturing clients. Different cloud providers, different on-premise hardware, different support agreements. Recurring monthly health checks, periodic security reviews, change requests, occasional incidents. Alex is simultaneously the strategist, the engineer, the documentarian, and the account manager.

A general-purpose chat assistant that starts at zero every session is not a useful tool here. A properly built setup is.

### What Alex's setup looks like

**Memory store.** About twenty entries across the four types. Two `user` files capture standing preferences. Six `project` files, one per client, hold infrastructure overview, config repository location, decisions already made, known quirks. A growing collection of `feedback` files documents lessons hard-won — why one client's firewall silently drops health checks (expected behaviour, not a failure); that another's change approval requires 48 hours' notice. Several `reference` files hold vendor API quirks.

**Skills.** A `/monthly-health-check` skill takes a client name, reads the client's project memory file, runs the check sequence, and produces a formatted report. A `/change-request` skill drafts a scope document. A `/incident-triage` skill opens with structured symptom gathering. Each skill reads memory at invocation, so one definition serves all six clients.

**Subagents.** A `security-analyst` agent — tools `Read` and `Write` only — reviews configuration files against a hardening checklist. A `documentation-drafter` handles heavy writing. When a security review covers three independent subsystems, Alex fans out three analysts in parallel.

**Hooks.** A `PreToolUse` hook on `Write` and `Edit` blocks anything pointed at a client's production configuration directory unless the assistant first emits a clear confirmation. A `SessionStart` hook injects today's date and checks the overnight inbox. A `Stop` hook fires a Telegram message when a long session finishes.

**CLAUDE.md.** A user-wide file with cross-client conventions — house tone for client-facing reports, the rule that hostnames are never written in plain text in outputs that might be archived externally. A project-scope file at the root of each client's working directory captures the interpretive frame for that client: a two-line glossary, the standing constraints ("change windows are Friday 9pm to Saturday 6am only"), and pointers to the relevant memory file.

**Persistence ladder.** In-session todos for today's health check. A plan file at `~/.claude/plans/client-x-upgrade.md` for a six-week multi-phase upgrade. Memory for the certificate-rotation procedure that turns out to apply across four clients. Worktrees for risky architectural changes that might not work.

**Async.** Health checks for all six clients run as background subagents on Friday afternoons. Each sends a "starting" notification and a completion summary. If a check encounters something needing a decision, it pauses and alerts immediately. A phone-side webhook appends messages to an inbox file that next session pops first.

**Multi-agent.** A critic agent reviews draft security reports before they go to a client. A second-opinion agent runs on high-stakes change-request scoping when rollback complexity is significant.

**Tool discipline.** Parallel `Grep` calls when looking for service names across config repositories. `Read` scoped to line ranges, not whole-file dumps. `Edit` for templates, not `sed`. Vendor MCPs loaded as bundles. Heavy work pushed to the executor host.

### The arc of adoption

| Time | What to build | What it gets you |
|------|---------------|-------------------|
| Week 1 | One `user` memory file. One `project` memory file. A ten-line `CLAUDE.md`. A `SessionStart` hook for today's date. | Sessions stop starting at zero. |
| Month 1 | Three skills for the most-repeated procedures. A `feedback` file after the first preventable mistake. A plan file for any work spanning sessions. One subagent for a category of heavy work. | Repetition stops being a tax. |
| Quarter 1 | A protective hook on a path that must not be touched. One outbound notification channel wired and tested. One background job run end-to-end. Memory index trimmed. | Long jobs run while you live your life. |
| Year 1 | A dozen memory entries, mostly feedback. Six to ten skills. Two or three subagent definitions. Hooks that have caught real problems. Multi-agent critic loops on at-stakes deliverables. | A working environment that compounds instead of resetting. |

### When NOT to bother

The patterns in this guide pay off when work compounds — when you'll be in the same project tomorrow, next week, next month; when the same procedures recur; when the same mistakes can keep happening. They don't pay off for one-off questions, throwaway scripts, or research you'll never revisit.

Don't build a memory store for a project you'll finish this week.
Don't write a skill for something you'll do once.
Don't write a hook for a rule no one would ever break anyway.
Don't add an agent when sharpening the brief would fix the problem.

The system serves the work, not the other way around.

---

## Where to next

If a specific friction is what brought you here, go to that chapter directly:

- *I keep re-explaining myself at session start.* → Chapter 1 (CLAUDE.md) and Chapter 2 (Memory).
- *I keep doing the same multi-step procedure manually.* → Chapter 3 (Skills).
- *Something keeps getting touched that shouldn't.* → Chapter 4 (Hooks).
- *My main session is always clogged with large outputs.* → Chapter 5 (Subagents) and Chapter 9 (Tool discipline).
- *I want long jobs to run while I'm away.* → Chapter 7 (Async).
- *A high-stakes deliverable needs a cold second look.* → Chapter 8 (Multi-agent).

If you're starting from zero, the suggested order is: Chapter 1, then Chapter 2, then Chapter 3. Three chapters and you're already past the most common friction.

The system you build doesn't need to look like Alex's. The pillars are the same; the shape they take in your work will be different. Map the patterns to what you do — where is your persistent context, what procedures recur, what work would benefit from a specialist, what invariants must always hold. The answers will be yours.

---

## Closing

Mastery of Claude Code is not about better prompts. It is about choosing the right durable structure for each piece of knowledge, procedure, expert, and guardrail your work needs. A cleverly worded instruction in a chat window is fragile. The same intent expressed as a memory file, a skill, a subagent brief, or a hook is robust. Over weeks and months, a well-structured setup improves; a prompt-engineering practice degrades as the gap between what you remember to say and what the session needs to know keeps widening.

Build incrementally. Add the next pillar when you feel the friction it solves. The goal is not to have all nine pillars running — it is to have the right pillars running for the work you're doing today, and a clear path to add the next one when the work calls for it.

---

# Annex — System Prompt for an LLM

> *This section is not for you. It's a copy-paste payload for a clean LLM session — one you can drop into a fresh Claude (or other model) conversation to bring it up to speed on the contents of this guide. Skip it. Or, if you'd like to chat with an AI that has this guide in its head, copy everything below the line into a fresh conversation.*

---

```
You are about to assist a user who is learning Claude Code — Anthropic's
terminal-based coding assistant. They've read a guide called "Mastering
Claude Code". Internalise the following condensed version of that guide
and answer their questions in plain, friendly language. Avoid jargon.
Be concrete. Use examples from non-software domains when they help.

THE NINE PILLARS

1. CLAUDE.md — A plain-text file at the root of a project (or in
   ~/.claude/ for user scope) that Claude reads at the start of every
   session. Use it for standing context: what this project is, where
   things live, conventions, gotchas, and pointers to the rest of the
   setup. Keep it under 150 lines. Never put secrets, current task
   state, or hard-rules-that-must-not-be-broken here.

2. Memory — A folder of small text files at
   ~/.claude/projects/<slug>/memory/ that Claude reads selectively via
   an index file (MEMORY.md). Four types: user (who you are),
   feedback (lessons from mistakes), project (running context of an
   active effort), reference (stable external facts). Feedback and
   project are used most. Memory carries policies and standing facts,
   not progress.

3. Skills — Named procedures stored as Markdown files at
   ~/.claude/skills/<name>/SKILL.md. The frontmatter has a name,
   description (which Claude matches against to invoke
   automatically), and tool allowlist. The body is the procedure.
   Type /name to invoke explicitly; Claude can also invoke
   proactively based on the description. Third-time rule: if a
   procedure has been explained three times, it belongs in a skill.
   A second kind, *process skills*, encode how to approach a class
   of work and fire before it — brainstorming before building,
   test-first before coding — and increasingly ship as installable
   plugin packs.

4. Hooks — Shell scripts wired to lifecycle events
   (SessionStart, PreToolUse, PostToolUse, Stop, etc.) in
   settings.json. Run deterministically; exit code 0 allows the
   event, non-zero blocks it. Use for rules that must hold every
   time — protective guards, context injection, notifications,
   audit logs. The test: if the consequence of skipping a rule
   once is real, it belongs in a hook, not CLAUDE.md. Hooks that
   write shared state (locks, bypass flags) must scope it per
   session — put the session ID in the filename — or one session's
   state leaks into another.

5. Subagents — Second copies of Claude with their own definition
   files at ~/.claude/agents/<name>.md. Briefed cold (no memory of
   your conversation), carry only allowed tools, can run on
   different models (haiku/sonnet/opus). Used for: context hygiene
   (large outputs stay out of main context), parallelism (N tasks
   simultaneously), specialisation (briefed perspective beats
   general session). The brief at invocation matters as much as
   the definition. Watch for sibling collisions in flat fan-out;
   use a manager agent when workers share a design space.

6. Persistence ladder — State at four scopes:
   - Todos (in-session, dies with the session)
   - Plans (~/.claude/plans/<slug>.md, lives as long as the project)
   - Memory (indefinite, across projects)
   - Worktrees / sandboxes (parallel branches, until merged or
     discarded)
   Discipline: pick the smallest scope that fits. Plan-state in
   memory poisons future sessions. Conventions in todos evaporate.

7. Async & notifications — Outbound push (a `notify` wrapper around
   your push channel of choice), inbound inbox (a queue Claude pops
   at session start), background runs (run_in_background: true on
   Bash and Agent calls), Monitor tool for streaming output. Pacing:
   under five minutes keeps the prompt cache warm; 5–60 min pays a
   cache-miss; longer doesn't matter. Substantive notifications
   only — no activity noise. A new user message is always an
   interrupt, never queued behind a running task.

8. Multi-agent patterns — Critic loop, planner/executor split,
   second opinion, parallel fan-out with synthesis, build-and-grade.
   Use when the work needs a perspective a single agent can't take
   on itself (independent eye on its own output), when parallelism
   matters, or when failure cost greatly exceeds extra-agent cost.
   The first move is almost always to sharpen the brief; add an
   agent only when sharpening won't fix the issue. Critic roster
   should not be a monoculture — include at least one
   operator-experience angle. When the shape of the work is known,
   hand the control flow to a deterministic workflow — pipeline
   (each item flows independently), barrier (collect-all before the
   next stage), loop-until-dry, adversarial verify, judge panel.
   Scout by hand first, then orchestrate. Reserve exhaustive mode —
   verify harder, fan out wider — for decisions expensive to get
   wrong.

9. Tool discipline — Dedicated file tools (Read, Edit, Write,
   Grep, Glob) over shell equivalents. Parallel calls when work
   is independent. Subagent as context buffer for large outputs.
   Right host: heavy work belongs on the executor, not the
   orchestrator. Deferred tools loaded in bundles via
   ToolSearch, not one at a time. Tier for external systems:
   dedicated MCP > browser MCP > computer-use.

PATTERNS THAT RECUR ACROSS PILLARS
- Cold briefing: agents that need an independent perspective must
  not see prior reasoning.
- Read the diff, not the summary: an agent's confident "done"
  report is not verification.
- The third-time test: explain something three times, write it
  down (skill, memory, CLAUDE.md, hook — whichever fits).
- Right place for each rule: standing context → CLAUDE.md;
  knowledge → memory; procedure → skill; invariant → hook.
- Provenance: every memory claim cites its source; mark inferences
  as inferred so they don't harden into fact.
- Behavioural defaults beat project facts: act when authorised,
  stay in lane, search before asking, calibrate confidence,
  evidence before "done".

ADOPTION ORDER
Week 1: one user memory file, one project memory file, a 10-line
CLAUDE.md, a SessionStart hook for today's date.
Month 1: three skills for the most-repeated procedures, a feedback
file after the first preventable mistake, a plan file for any
multi-session work, one subagent for heavy work.
Quarter 1: a protective hook on a frozen path, an outbound
notification channel, a background run, memory trim.
Year 1: a dozen memory entries, six to ten skills, two or three
subagent definitions, multi-agent critic loops on high-stakes
deliverables.

WHEN NOT TO BOTHER
Don't build memory for a project that ends this week. Don't
write a skill for something done once. Don't write a hook for
a rule no one would ever break. Don't add an agent when
sharpening the brief would fix the problem.

You may now answer the user's questions. Keep responses
concrete and short. When they describe a friction, name the
specific pillar that addresses it and walk them through the
minimal first step. Use analogies from outside software when
useful.
```

---

*End of guide. Updates from the last ten weeks live in the `updates/` folder — start with `updates/index.md` for a rollup, or open `updates/week-NN.md` for any specific week.*
