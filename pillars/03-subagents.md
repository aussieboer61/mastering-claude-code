# Pillar 3 — Subagents

## Principle

A subagent is a specialised, briefed-cold worker: it arrives with no memory of your conversation, carries only the tools you explicitly permit, and may run on a different model than your main session. You write its system prompt once, store it as a definition file, and from that point forward your main session can invoke it by name whenever that category of work appears. The main session orchestrates — it holds the plan, the context, and the judgment calls. The subagent executes a bounded task and reports back. This division is not a courtesy; it is the structural reason subagents are useful at all.

## Why it matters

Every tool call that returns a large payload lands in your context window and stays there. Delegate that work to a subagent and only the summary comes back. Subagents also enable true parallelism: three independent research questions can run simultaneously, finishing in the time the slowest takes. Beyond speed, a subagent briefed as a domain specialist is less likely to wander than your general session handling one more thing at the bottom of a long thread — the separation of concerns is a correctness guarantee as much as an efficiency one.

## Components

**Agent definition file** — a Markdown file with a YAML frontmatter block followed by the agent's standing instructions. The frontmatter declares the agent's identity and capabilities:

```yaml
---
name: research-analyst
description: Use this agent for literature searches, citation checking, and summarising academic sources on a given topic. Invoke when the task is "find what is known about X" rather than "decide what to do about X".
tools: Bash, Read, Write
model: sonnet
---
```

The body of the file is the agent's persistent briefing: its role, the conventions it must follow, the escalation rules it applies when it hits something unexpected, and any standing context (file paths, API conventions, format requirements) it needs to function without asking you for basics.

**Description as a router** — the `description` field is read by the orchestrator to decide which agent to invoke. Write it as a crisp statement of when to use this agent, not what it is. "Use for X when Y" is the pattern. Vague descriptions produce incorrect routing; precise ones let the orchestrator delegate automatically without your intervention.

**Tool allowlists** — list only what the agent genuinely needs. A research agent that reads files and runs searches does not need `Write` or `Edit`. A formatting agent that rewrites documents does not need `Bash`. Restricting tools limits blast radius if the agent misinterprets its brief, and it signals intent — a tight allowlist is documentation of what the agent is supposed to touch.

**Model selection** — the `model` field accepts `haiku`, `sonnet`, or `opus`. The rule of thumb: haiku for high-volume, low-stakes, or easily-verified tasks (formatting, data extraction, mechanical transformations); sonnet for standard professional work where judgment and code quality matter; opus for tasks where getting it wrong is expensive and reasoning depth is the bottleneck (legal analysis, architectural decisions, subtle debugging). Running N parallel haiku agents to extract structured data from N documents costs a fraction of a single opus call and often produces equivalent results.

**Foreground vs background invocation** — foreground blocks the main session until the agent returns; use it when the next step depends on this result. Background launches without waiting; use it when the subtask is independent and you have other work to progress. Pillar 6 covers how to collect background results via notifications.

**Manager agent** — a subagent whose job is to coordinate other subagents rather than to execute domain work itself. It receives the overall workstream, assigns sub-tasks to workers, deconflicts shared design decisions before any worker begins, collects their outputs, and returns a single consolidated result to the main session. Use a manager when the workers would need to talk to each other to do their jobs well — when they share a design space, need consistent naming, or must avoid duplicating domains. A manager agent absorbs the orchestration work that would otherwise consume main-session context across many turns.

**Worktree isolation** — for work that touches files (especially in a shared repository), consider giving each agent its own git worktree so their concurrent edits don't collide. This is most relevant for parallel fan-out over a codebase; for research or read-heavy tasks it is usually unnecessary overhead.

**The brief itself** — what you pass to the agent at invocation time is as important as the definition file. The brief is the specific task: what to do, where the relevant material lives (exact paths, not vague descriptions), what the expected output format is, and what to do if something looks wrong. The brief should be self-contained — the agent cannot ask you a clarifying question mid-task without being designed to do so.

## How to apply it

**When to delegate vs do inline** — if a task fits in three lines of your main session and produces no large output, do it inline. Delegate when any of these are true: the output will be large (and you don't want it cluttering your context); the task is one of several that can run in parallel; or the task falls into a domain where a purpose-built specialist will produce consistently better results than your general session handling it as an aside.

**Write a self-contained brief** — before you spawn an agent, prove to yourself that you understand the task well enough to hand it off. A well-formed brief specifies the goal in one sentence, the exact input (file paths, line ranges, dataset locations), the required output format, and the failure condition. Do not hand synthesis work to the agent unless synthesis is its job — "figure out what needs doing and do it" is not a brief.

```
Goal: [one sentence]
Input: [exact paths / data / content]
Output: [format and destination]
Constraints: [things not to change, word count, style guide]
If stuck: [report back rather than guess]
```

**Fan-out pattern** — when you have N independent subtasks of the same type (summarise these N documents; check these N references; draft these N sections), spawn N agents in parallel. Collect their outputs, validate them, then proceed. The validation step is not optional: read what they actually produced before treating it as done.

When the subtasks share a design space — they must produce consistent naming, cover distinct domains without overlap, or make aligned stylistic choices — flat fan-out will produce collisions. Five agents independently choosing their own worked-example domain will converge on the same obvious domains. In those cases, use a manager agent to assign distinct scope to each worker before any of them begin. The heuristic: if you can imagine the workers needing to talk to each other to do their job well, you need a manager. See Pillar 7 for the manager-of-workers pattern in broader multi-agent context.

**Trust but verify** — an agent's summary of its own work is not a substitute for reading the diff or output directly. After a subagent completes a task that modifies files, read the changed content. After a research agent returns sources, spot-check at least one citation. Agents produce plausible-sounding results; your job is to confirm they are correct.

## Failure modes

**The terse prompt** — "fix the formatting issues in the report" produces shallow, inconsistent work because the agent must guess what the formatting standard is, where the issues are, and what good looks like. The agent's output reflects the quality of the brief. A vague brief is an instruction to do vague work.

**Over-delegation of trivial tasks** — spawning a subagent to rename a variable or change a date is slower than doing it inline. Agent invocation has overhead (model call, context initialisation, result parsing). The break-even point is a task that would take you 30–60 seconds of careful effort yourself. Below that, do it yourself.

**Serial fan-out** — launching agents one at a time when they are independent wastes the primary benefit of the pattern. If you find yourself waiting for agent A to finish before starting agent B, and they do not share state, you have serialised work that should be parallel.

**Trusting the summary** — an agent that reports "done, all three sections updated" may have updated two sections correctly and one incorrectly. The confident tone of LLM output is not correlated with correctness. Your verification step is the close of the loop.

**Flat fan-out when sub-tasks share design space** — spawning N parallel workers without a coordinating manager produces sibling collisions when the workers must make choices that should be consistent across the set. Workers cannot see each other's decisions, so they independently choose the same obvious paths: the same example domains, the same naming conventions, the same framing. Detecting and correcting the collision after the fact costs more than preventing it up front. If the workers would need to deconflict in order to produce a coherent whole, assign scope through a manager agent before spawning them.

**Subagent for what should be a skill** — if the "agent" is really just a fixed sequence of shell commands (deploy this container, reload this config, run this migration), it belongs in a skill file, not an agent definition. A skill is a packaged procedure; an agent is a packaged expert. If there are no judgment calls, use a skill.

## Worked example

Suppose you are writing a long-form report on urban heat island mitigation for a consulting engagement. The report has six chapters, each requiring a literature review of roughly 15 sources. Doing all six reviews sequentially in your main session would take a long time, produce enormous context pollution, and risk inconsistent citation style across chapters.

You define a `literature-analyst` subagent: model sonnet, tools `Read` and `Write`, briefed to search a local document archive, extract relevant evidence, and write a structured summary to a specified output file using a citation format you define in the standing instructions. Its description reads: "Use when a chapter requires sourced literature review. Pass the chapter topic, the archive path, and the output file path."

At the start of the report session, you fan out six instances in parallel — one per chapter — each with a concrete brief naming its topic, its source corpus, and its output path. While they run, you draft the executive summary inline. When the agents finish, you read each output file (you do not trust the "done" messages alone), consolidate the six summaries, and proceed to drafting with your context holding only the distilled evidence, not 90 raw documents.

The subagent earned its place because the work was parallelisable, the output was large, and the task was repeatable enough to justify a standing definition. A single one-off lookup would not clear that bar.

## Subagent vs skill vs doing-it-yourself

A skill is a packaged procedure: a fixed sequence of steps, usually shell commands or file operations, that runs the same way every time with no judgment required. A subagent is a packaged expert: it brings a briefed perspective, uses tools adaptively, and can handle variation within its domain. Doing it yourself is simply the main session handling the task inline, with no delegation overhead. The decision rule: if the task is mechanical and repeatable, write a skill. If the task requires domain knowledge, adaptive tool use, or produces output large enough to pollute your context, define a subagent. If the task is small, obvious, and produces compact output, do it yourself. When in doubt, do it yourself first — if you find yourself repeating the same class of work three or more times, that is the signal to invest in an agent definition.
