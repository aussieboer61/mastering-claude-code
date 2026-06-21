# Pillar 5 — The Persistence Ladder

## Principle

State lives at four scopes: within a single response, across a conversation, across all conversations, and across parallel branches of work. Each scope has a natural tool — todos, plans, memory, and worktrees — and each tool carries overhead proportional to its durability. The discipline is to pick the smallest scope that your work genuinely needs. Reaching for a durable tool when an ephemeral one would do introduces friction; reaching for an ephemeral tool when you need durability means redoing work. The ladder is not a ranking of quality; it is a map of fit.

## Why it matters

When you store ephemeral state in memory, the memory store fills with session-specific minutiae that obscures the permanent signals it exists to carry. When you carry multi-phase work only in an in-session task list, a single lost conversation erases your entire plan. When you let experimental work accumulate in your primary working document or directory, you contaminate finished work with half-formed ideas. Each mismatch costs something; none of them announces itself loudly until the damage is done.

## Components

### Tasks (in-session)

The `TodoWrite` tool creates a structured task list that Claude Code tracks within the current session. Use it for the sequence of actions needed right now: "call the plumber to confirm Tuesday start", "check whether the structural inspection certificate has arrived", "draft the variation notice for the window relocation". It is a working memory aid, not a planning artefact and not a record. When the session ends, the list ends with it. Do not treat a todo list as a deliverable, a decision log, or a specification for future sessions. Its job is to keep Claude from losing its place during a complex multi-step response.

```
TodoWrite([
  { "id": "1", "content": "Check delivery status for framing timber", "status": "in_progress" },
  { "id": "2", "content": "Draft site instruction for relocated door opening", "status": "pending" },
  { "id": "3", "content": "Confirm inspection booking with certifier", "status": "pending" }
])
```

Use todos freely and discard them freely. Their value is tracking, not archiving.

### Plans (multi-step within or across sessions)

A plan is what a todo list becomes when the work spans more than one session, requires a human decision between phases, or has dependencies that need to be reasoned about in advance. A good plan states phases, not just steps. It records why a phase exists, what the success condition is, and what decision is needed before the next phase starts. A plan written as a flat list of bullets is a glorified todo list; a plan written with phases, owners, success criteria, and decision points is a genuine coordination artefact.

Save plans in a known location — not `/tmp`, not a session-local buffer. A conventional path like `~/.claude/plans/<slug>.md` means the plan survives reboots, can be referenced in a new session by reading the file directly, and can be committed to a project folder if the work requires auditability. The plan is the artefact: it lives as long as the work lives, and it gets archived or deleted when the work is done.

A plan answers: what are the phases, in what order, and what does "done" mean for each? A todo list answers: what am I doing right now in this session?

### Memory (cross-session, cross-project)

The auto-memory store is for state that outlives any individual project and any individual plan. It is where conventions, preferences, recurring decisions, and hard-won lessons live. Pillar 1 covers the memory system in full; this rung's relationship to the others is the important thing to understand here.

The test for whether something belongs in memory is: "Will I want this in a session that has nothing to do with the current work?" If the answer is yes, it belongs in memory. If the answer is "only while this project is active", it belongs in a plan or a project-local file. The classic mistake is saving plan-state to memory — "we are currently in the fit-out phase, kitchen cabinets arrive Friday" — which becomes stale the moment that phase ends and poisons every future session that loads the memory. Conventions go to memory; progress goes to the plan.

### Worktrees (parallel, isolated)

In a software project, a git worktree creates a second checked-out copy of the repository in a separate directory on a different branch. Claude Code's Agent tool can run a subagent inside a worktree so that experiments proceed without touching the main working tree — you merge or discard the result when ready.

```bash
git worktree add ../project-experiment feature/alt-approach
```

The principle transfers directly to non-software work. If your deliverables are documents, spreadsheets, or plan files rather than source code, a "worktree" is a sandbox copy: a separate subdirectory holding the experimental variant while the authoritative version stays untouched. The mechanism differs; the discipline is identical.

Use worktrees (or sandbox copies) when you want to explore an alternative in parallel with ongoing work, or when a subagent needs to make many changes that might be thrown away. The overhead is real — a second branch or directory that eventually needs reconciliation or deletion — so isolation is not justified for a minor in-place correction. The test: would doing this directly risk clobbering or confusing the current authoritative work?

## How to apply it

The default ladder-walk for any new piece of work is the same regardless of domain.

Start with todos. Open the session, scope the task, and let `TodoWrite` track the steps. If the work completes within the session, you never need to climb higher.

Promote to a plan when the work spans sessions or requires a sign-off between phases. Write the plan to a file, record what is done and what comes next, and confirm the next phase if the user needs to decide. Begin each new session by reading the plan file before generating a fresh todo list.

Persist to memory only when a decision has proven to generalise beyond this project. "We chose a particular subcontractor for this job" is plan-state. "All our projects book inspections at least five working days in advance and use a standard variation log format" is policy — write it to memory once and delete the stale plan-state it replaces.

Branch a worktree when you want to test an alternative without disturbing the mainline. Create the sandbox, run the experiment, integrate or discard. Never create one "just in case" — start in place and branch only when the experiment is real.

## Failure modes

**Promoting todos to permanent documents.** A session todo list that gets saved to a file, copied into a shared workspace, or treated as the project record is occupying the wrong scope. If the list is worth saving, it is a plan, and it should be rewritten as one with proper phases and success criteria.

**Writing a plan for work that fits in one session.** A five-phase plan for "call the plumber and confirm Tuesday's start time" is overhead that slows you down and teaches you nothing. Reach for a plan only when sessions or sign-offs are genuinely involved.

**Saving plan-state to memory.** Memory carries policy; the plan carries progress. "Phase 2 (structural) is complete, awaiting certification before fit-out begins" is not memory. Writing it to memory will be wrong next week, and loading stale progress into every subsequent session contaminates them all.

**Creating a worktree for a trivial edit.** The overhead of a second directory — eventual reconciliation, managing two authoritative-looking copies — is only justified when the isolation is genuinely needed. A small correction to the main document is fine. Reserve isolation for exploratory work that might not survive.

**Never promoting recurring patterns to skills.** A pattern that appears in your todos every session — "always pull up the variation log, always check the inspection schedule, always draft the daily site diary entry" — is a candidate for a skill (Pillar 2), not a permanent fixture of the todo list. Todos are for session-specific sequences; persistent workflows that recur across many sessions belong as reusable skills.

## Worked example

A homeowner is coordinating a multi-month renovation: demolition in month one, structural framing and inspections in month two, and fit-out across months three and four. She opens a session the morning before the first site visit and uses `TodoWrite` to track the day's work: confirm the skip bin delivery window, photograph the existing wall positions before demolition starts, call the building certifier to schedule the frame inspection, and draft a variation notice for a window that has moved 400 mm from the approved drawings. The work fits in one session. The todo list does its job and is gone by evening.

Two weeks later, the scope has grown beyond any single session: three phases, two hold points requiring certifier sign-off before work can proceed, a materials schedule tied to lead times, and a variation log both parties must track. She writes a plan to `~/.claude/plans/kitchen-reno-2024.md` with labelled phases — Demolition, Structural, Rough-in, Fit-out — each with a success condition and a note at the hold points: "pause here, do not proceed until inspection certificate received". Every new session begins by reading the plan file and generating a fresh todo list for that day's work. When framing is certified, she marks the phase done and confirms what the next phase requires before moving on.

Midway through fit-out, she notices she has been restating the same conventions at the start of every session: variation notices follow a specific format, quoted prices are GST-exclusive until final invoice, and trades receive 48 hours written notice before any schedule change. These are not plan-state; they are policies for every renovation she will ever manage. She moves them into a memory entry so they load automatically. Meanwhile, the builder suggests moving the island bench 600 mm to improve traffic flow — a change that would relocate two power points and might void the tile order already placed. Rather than editing the confirmed fit-out plan directly, she creates a sandbox copy in a separate folder and works through the cost and flow implications there. The change does not hold up. She discards the sandbox and the authoritative plan is untouched.

## When to use which (decision rule)

If the state dies with this response, use a todo.
If the state needs to survive across sessions or requires a sign-off between phases, write a plan.
If the state will be useful next month in a completely different project, write it to memory.
If the work would contaminate or confuse what is already authoritative if done in place, create a worktree (or a sandbox copy for non-code work).
