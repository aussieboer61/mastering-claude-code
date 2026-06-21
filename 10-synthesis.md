# Synthesis — The Nine Pillars as One System

## The shape of a mature setup

Taken one at a time, the nine pillars read like a checklist of features. Used together, they form a system with a clear structure: a persistent knowledge layer with two halves — automatic, semantic memory (Pillar 1) and manually authored standing instructions in `CLAUDE.md` (Pillar 9) — that every other component can draw on; a procedure layer (skills) that converts repeatable work into reliable one-command operations; a delegation layer (subagents) that routes specialist or parallel work out of the main session; and an enforcement layer (hooks) that holds invariants the other layers depend on. Those five form the harness.

Above the harness sit four composition patterns. The persistence ladder gives the harness appropriate memory at each timescale — ephemeral for right-now work, plan files for multi-session projects, memory for policies that generalise, worktrees for experiments that must not contaminate mainline progress. Async and notifications decouple the harness from your physical presence: long jobs run, complete, and report back whether you are at the terminal or not. Multi-agent patterns add structural independence to any step where a single agent's bias is too expensive to accept — a critic loop, a second opinion on a high-stakes call, a parallel fan-out across independent workstreams. Tool discipline is the thread running through all of them: each pattern is only as fast and clean as the tool choices that execute it.

The interdependencies are what make this a system rather than a collection. A skill can invoke a subagent for its heavy phase. A hook at session start can inject context pulled from memory. A subagent running in the background can push a notification when it finishes, which the async layer routes to your phone. A critic loop that spans multiple rounds relies on the subagent design (briefed cold, correct tool allowlist) and on tool discipline (returning only the structured critique, not the raw content that prompted it). A plan file created by the persistence ladder becomes the brief that a planner/executor pair uses to divide reasoning from execution. The pillars do not add up; they multiply.

A mature setup does not mean all nine pillars active from day one. It means that each piece of work sits at the right rung of the ladder, runs through the right layer, and is held by the right guardrail — and that the setup accumulates value over time rather than needing to be rebuilt from scratch each session.

## A running example: a one-person IT consultancy

Alex runs a one-person IT consultancy serving six small manufacturing clients. Each client has a distinct infrastructure footprint — different cloud providers, different on-premise hardware, different support agreements — and each has recurring work: monthly health checks, periodic security reviews, change requests of varying size, and the occasional incident. Alex is simultaneously the strategist, the engineer, the documentarian, and the account manager. The work is technically varied, never stops accumulating, and demands that Alex remember a large and specific body of context about six different environments at once. A general-purpose chat assistant that starts from zero every session is not a useful tool here. A properly built harness is.

## Walking the pillars

### Pillar 1 — Memory

Alex maintains a memory store at `~/.claude/projects/consultancy/memory/`. The index file (`MEMORY.md`) has around twenty entries across four types. Two `user` files capture standing preferences — Alex's communication style, preferred output formats, and a policy against abbreviating client names in documentation. Six `project` files, one per client, each record the client's infrastructure overview, the location of their config repository, decisions already made (which backup strategy, which monitoring stack, which escalation path), and a short list of known quirks. A growing collection of `feedback` files documents lessons hard-won from incidents: one captures why a particular client's firewall silently drops health-check pings (not a failure — that's expected behaviour); another records that one client's change-approval process requires 48 hours' notice, not 24. Several `reference` files hold vendor-specific API documentation excerpts and the exact command syntax for tools Alex uses across clients.

Every session starts knowing which client's work is in scope, what decisions are already settled, and what patterns have caused problems before. Alex stops re-explaining the same context six times a week. See [Pillar 1](pillars/01-memory.md) for how to structure the index and the four memory types.

### Pillar 2 — Skills

Recurring procedures are packaged as skills stored in `~/.claude/skills/`. The `/monthly-health-check` skill accepts a client name, reads the relevant project memory file to find the infrastructure endpoints, runs a structured check sequence (service uptime, disk usage, backup verification, certificate expiry), and produces a formatted report in the house style Alex sends to clients. The `/change-request` skill takes a description of a proposed change, checks it against the client's known constraints from memory, drafts a scope document, and asks Alex to review before finalising. A `/incident-triage` skill opens with a structured symptom-gathering phase, checks the relevant feedback memory for known false positives, and produces a prioritised action list.

The skills interact with memory directly — each reads the client's project file at invocation to avoid hardcoding any client-specific detail. That means a single skill definition serves all six clients without modification. See [Pillar 2](pillars/02-skills.md) for frontmatter conventions and the description discipline that makes skills trigger reliably.

### Pillar 3 — Subagents

Some work is too large or too domain-specific to run inline. Alex defines a `security-analyst` subagent briefed to review a set of configuration files against a hardening checklist, flag deviations, and write structured findings to an output file. Its tool allowlist is `Read` and `Write` only — it should never execute commands on a client system, only read exported configs. A `documentation-drafter` subagent handles the heavy writing work: given a set of change records and a client brief, it drafts a change report in the client's preferred format without cluttering Alex's main session with large drafts.

When a security review covers three independent subsystems, Alex fans out three `security-analyst` instances in parallel, one per subsystem, and reads each output file before synthesising a combined finding. The parallel run finishes in the time the slowest subsystem takes rather than three times that. The subagent design relies on the memory system: each agent's brief includes the path to the relevant client project file so it is not working blind. See [Pillar 3](pillars/03-subagents.md) for the brief template and the decision rule between subagents and inline work.

### Pillar 4 — Hooks

Two hooks do work that would otherwise require constant vigilance. A `PreToolUse` hook guards the `Write` and `Edit` tools: it reads the target file path from the tool payload and checks whether it falls inside any client's production configuration directory. If it does, it emits a block with the message "Production config path — confirm intent before this write proceeds." The hook runs every time, regardless of which session, which model version, or how the task was framed. Alex's client configs are never accidentally overwritten by a confident but incorrect assistant response.

A `SessionStart` hook injects today's date and a one-line reminder to check the inbox before starting. This closes a consistent gap: without it, Alex occasionally starts work that a phone-side instruction from earlier that morning would redirect. The hook also checks whether a background health-check job from the previous session left a status file, and if so injects a summary of its findings into the session context automatically. The hooks interact with the notification system — the `Stop` hook fires a lightweight Telegram message whenever a long session finishes, so Alex knows the job is done without watching the terminal. See [Pillar 4](pillars/04-hooks.md) for the event model and the exit-code semantics.

### Pillar 9 — CLAUDE.md & Standing Instructions

Memory accumulates facts; `CLAUDE.md` declares standing context. Alex maintains a user-scope `~/.claude/CLAUDE.md` with cross-client conventions — the consultancy's house tone for client-facing reports, the rule that hostnames are never written in plain text in any output that might be archived externally, and pointers to where the rest of the system lives ("memory store at `~/.claude/projects/consultancy/memory/`; skills at `~/.claude/skills/`; plans at `~/.claude/plans/`"). Each client also has a project-scope `CLAUDE.md` at the root of their dedicated working directory that captures the interpretive frame for that client: a two-line glossary, the standing constraints ("change windows are 9 pm Friday to 6 am Saturday only"), the location of their config repository, and a pointer to the relevant memory file for deep detail.

The discipline is to keep each file short. CLAUDE.md is loaded into every session for its scope — bloat there costs tokens and assistant attention on every turn. When Alex notices a CLAUDE.md drifting past 50 lines, that signals the content has outgrown standing-instruction status and belongs in memory (selectively retrieved) or as a skill (invoked on demand). The CLAUDE.md files reference the memory store rather than duplicating it; the memory store carries the facts, CLAUDE.md carries the lens through which the assistant reads them. See [Pillar 9](pillars/09-claude-md.md) for the cascade order and the test that decides what earns a place in the file.

### Pillar 5 — The Persistence Ladder

Alex uses all four rungs, consciously. In-session todos track the steps of a health check currently running — fetch the disk stats, check the cert dates, verify the last backup — and are discarded when the session ends. When a client requests a multi-phase infrastructure upgrade that will span six weeks and require sign-off between phases, Alex writes a plan to `~/.claude/plans/client-x-upgrade-2026.md` with labelled phases, success criteria, and explicit pause points. Each session opens by reading the plan and updating it with completed phases.

When a pattern that started as plan-state generalises — Alex notices the same certificate rotation procedure is needed across four clients, not just one — it moves to a `reference` memory file. The plan entry is replaced with a pointer to memory. When a client requests a risky architectural change that might not work, Alex creates a worktree, runs the experiment there, evaluates it, and either merges it or discards it without touching the mainline work. See [Pillar 5](pillars/05-persistence.md) for the decision rules at each rung.

### Pillar 6 — Async & Notifications

Monthly health checks across six clients take hours when run sequentially with manual review between each. Alex sets them up at the start of a Friday afternoon, fires them as background subagent runs with `run_in_background: true`, and leaves the office. Each health-check run sends a "starting" notification when it begins and a completion notification — with a one-line summary of findings — when it finishes. If a check encounters something that requires a decision (a disk usage threshold crossed, a certificate expiring within two weeks), it sends an alert immediately and pauses rather than proceeding autonomously.

Alex maintains an inbound inbox: a plain text file that a phone-accessible webhook can append to. Instructions dropped from the phone — "skip the NAS backup check for client D this month, they are mid-migration" — are in the inbox when the session starts, and the `SessionStart` hook reminds the assistant to read them first. Background subagent output is never silently abandoned: a standing rule in Alex's system prompt requires reading the last background run's output file before any new session starts. See [Pillar 6](pillars/06-async.md) for the notification design and the pacing primitives.

### Pillar 7 — Multi-agent patterns

Two situations reliably warrant a second agent. First: security review findings before they go to a client. A draft security report represents Alex's judgment, and Alex is too close to it to catch every gap or overstatement. A critic agent — briefed cold with only the finished draft and an explicit rubric (accuracy, completeness, tone, absence of vendor blame) — runs one cold pass and returns a structured list of issues. Alex addresses the material ones and sends. The critic loop pays off twice per year when it catches something that would have damaged the client relationship.

Second: high-stakes change-request scoping. When a proposed change has significant rollback complexity, Alex spawns a second-opinion agent with the same change description and infrastructure context, no reference to Alex's existing analysis. If the two analyses agree, confidence is high. If they disagree, the disagreement pinpoints exactly where the risk is genuinely uncertain — which is the most useful output of all. Both patterns depend on subagent design (cold briefing, correct tool allowlist) and on keeping the context clean (tool discipline) so the critic receives a legible document rather than a cluttered dump. See [Pillar 7](pillars/07-multi-agent.md) for rubric design and the conditions that justify adding an agent.

### Pillar 8 — Tool discipline

Alex's sessions are fast because the tool choices are correct at each step. Finding all references to a specific service name across a client's config repository is one parallel `Grep` call, not twenty sequential reads. Reading the relevant section of a large log file is a `Read` call scoped to the relevant line range, not a `cat` of the whole file. Editing a config template uses `Edit` with an explicit `old_string` / `new_string` pair, not a `sed` command that would apply blindly to every match. When a task involves the client's cloud provider — querying resource states, checking billing alerts — Alex loads the provider's MCP toolkit with a single `ToolSearch` call rather than falling back to the browser or screen-scraping.

The subagent-as-context-buffer pattern is in constant use: when a security analyst subagent needs to read 40 config files, it returns a structured findings list to the main session, not 40 files. The main session holds Alex's reasoning, not raw material. Batching independent tool calls into single turns is a standing habit enforced by a note in Alex's `CLAUDE.md`. See [Pillar 8](pillars/08-tool-discipline.md) for the tiered tool selection hierarchy and the parallel-call discipline.

## The first month, the first quarter, the first year

**Week one.** Set up the memory store. Write one `user` file (preferences, standing defaults). Write one `project` file for the most active client or project. Create a five-to-ten-line `CLAUDE.md` at the root of that project with the bare minimum standing context. Create a `SessionStart` hook that injects today's date. That is enough to feel the difference from day one.

**Month one.** Identify the three most frequently repeated procedures and write skills for them. Write your first feedback file after the first mistake the new setup allows you to prevent. If any ongoing work already spans multiple sessions, promote it to a plan file. Test one subagent for one category of heavy work.

**Quarter one.** Add the production-path guard hook. Wire one outbound notification channel. Run a background job for the first time and confirm the notification arrives. Review the memory index; archive or delete anything already stale. You now have the full harness running at basic configuration.

**Year one.** The memory store has a dozen or more entries, most of them feedback files accumulated from real mistakes. The skills directory has six to ten entries covering everything recurring. Two or three subagent definitions handle the specialist work you used to do inline. The hooks have caught at least one thing that would have been a real problem. You have run multi-agent critic loops on several high-stakes deliverables. The system has saved you, conservatively, a few hours a week — not by doing your thinking for you, but by not making you repeat yourself.

## What the system feels like once it's running

You stop re-explaining yourself. Each session opens knowing the relevant client or project, the decisions already made, the patterns to avoid. The procedures that used to require re-prompting now invoke reliably with one phrase. Background jobs run and report back; you are not watching terminals. The high-stakes deliverables get a cold second read before they go out.

What you are left with is attention on the actual work — the judgment calls, the client conversations, the decisions that genuinely need a human. The system handles the overhead of continuity, consistency, and context. It does not make decisions for you; it makes sure that when you make them, you have the right information available and the right guardrails in place. That is what a durable working environment is for.

## Where to go next

Each pillar chapter covers its topic in full, with failure modes, worked examples, and the decision rules for when to use each tool. If a specific layer is where your friction is right now — re-explaining context, unreliable procedures, unguarded writes, lost state between sessions — go to that pillar chapter directly.

The running example here is a one-person IT consultancy. Your work may look nothing like it. The nine rungs are the same. Map them to what you do: where is your persistent context, what are your repeatable procedures, what work would benefit from a specialist perspective, what invariants must always hold? The answers will be different; the structure will be the same.
