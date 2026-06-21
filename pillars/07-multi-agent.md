# Pillar 7 — Multi-agent Patterns

## Principle

A single agent is fast but biased toward its first plausible answer. Once it commits, every subsequent step reinforces that direction rather than questions it. A second agent briefed cold cannot anchor on the first's framing because it never saw it — that structural independence is the point. The cost is roughly linear in tokens; the quality lift, particularly where the most dangerous failure is a confident wrong answer, is not. The patterns in this pillar use a second or nth agent not for raw throughput but for the perspective that a single agent cannot give itself.

## Why it matters

A reviewer who did not write the plan sees gaps the author assumed away. A second agent briefed cold is in exactly that position. This matters most for hard-to-reverse decisions and for judgements where a confident wrong answer is worse than a flagged uncertainty. When verification is cheap, do it yourself; when it requires a perspective you cannot structurally take, add an agent.

## Components

### Critic loop (review → fix → re-review)

One agent produces; a second agent, briefed cold, critiques against an explicit rubric; the producer incorporates the critique; the critic re-checks. The loop terminates when the critic has no material objections or when a fixed ceiling is reached — whichever comes first. Set a ceiling of two or three rounds before you start; a loop with no exit condition iterates indefinitely on ever-smaller issues. If major objections persist after three rounds, the problem is the brief or the rubric, not the iteration count. The critic receives only the output, never the producer's reasoning — a critic who knows intent evaluates effort rather than result.

```
CRITIC BRIEF — round {N}
You are reviewing the attached draft. You have not seen any prior version.
Evaluate against this rubric:
  - [criterion 1]
  - [criterion 2]
  - [criterion 3]
Return a structured list: issue / location / severity (critical | minor | suggestion).
Do not propose rewrites. Identify problems only.
```

### Planner / executor split

A reasoning-heavy planner agent — typically the most capable model available — produces a structured plan. A cheaper executor agent carries out each step. The split exists because planning and execution have different bottlenecks: planning is reasoning-intensive and mistakes there compound; execution is often mechanical once the plan is sound. Running an expensive model just for planning and a cheaper model for execution usually beats running either model end-to-end.

The planner's output must be a genuine hand-off document: steps in order, explicit inputs and outputs per step, decision criteria for branches, and guidance for failures. If the plan requires the executor to exercise significant judgment, it is underspecified. The executor should report back per step — a pipeline that runs silently and then says "done" gives no opportunity to catch a bad step before the next builds on it.

### Second opinion / consensus

For a single high-stakes judgement — is this clause ambiguous? is this schedule feasible? — spawn a second agent with the same inputs and a brief that references nothing the first produced. Agreement increases confidence; disagreement locates exactly where the question is genuinely hard, which is itself useful. Reserve this pattern for irreversible actions and judgements whose surface simplicity conceals real complexity. It is expensive for easy questions.

### Parallel research fan-out

N agents in parallel on N independent questions, then a synthesiser that produces a unified result. The pattern compresses wall-clock time and context window cost — only the synthesised result comes back to the main session. The independence requirement is strict: if B depends on A, running them in parallel produces an error-embedded output that looks complete and is not. Map dependencies before spawning. The synthesiser is a full agent, not a concatenation step — brief it to reconcile contradictions and flag gaps, not just stitch outputs together.

Independence means more than data dependencies. When the N sub-tasks share a *design space* — they must cover distinct domains, use consistent naming, or make aligned structural choices — a flat spawn will produce sibling collisions: each worker independently gravitates toward the same obvious choices. Assign scope explicitly before spawning. A manager agent (see Pillar 3) can receive the full workstream, partition the design space, and dispatch workers with non-overlapping briefs, returning a single result to the main session instead of consuming main-session context across many coordination turns.

### Build-and-grade

A producer drafts; a grader scores it against an explicit rubric; the producer iterates; the grader re-evaluates. Unlike the critic loop, the grader produces a score, making convergence visible — you can see whether rounds are improving the work or spinning in place. Useful for content where quality is judgeable but not binary: writing, documentation, analyses, plans. The rubric must exist before the first draft; a rubric reverse-engineered from the draft only measures how well the draft matches itself.

## How to apply it

Start simple: pass a finished output cold to a single critic with an explicit rubric. One cold pass tells you whether the pattern earns its place before you invest in a full loop.

Once single-pass criticism is reliable, formalise it into a loop with a hard ceiling of two or three rounds. Add the planner/executor split only when your workflow routinely produces shallow plans that require backtracking during execution. Add second-opinion calls sparsely — reserved for specific high-stakes decision categories identified in advance, not sprinkled across every step.

Use parallel fan-out only after confirming independence — map the dependency graph before spawning. Always brief each agent cold: no prior conversation, no other agent's reasoning, no hint of what you expect. The independent perspective is the entire point.

## Failure modes

**Critic loops that never converge.** No stop rule means the critic always finds something and the loop runs indefinitely. Set a ceiling before you start; accept good-enough after three rounds over perfect after ten.

**Planners that over-specify.** Specifying every micro-step leaves the executor no room to respond to what it actually finds. Plans should specify outcomes and constraints per step, not a rigid command sequence.

**Second opinions that share the first agent's conclusion.** "Agent A concluded X; what do you think?" is a request for validation, not a second opinion. The second agent must receive the same raw inputs as the first, nothing more.

**Parallel fan-out for dependent tasks.** Running B in parallel with A when B needs A's output embeds errors that only surface at integration time. Map dependencies before spawning.

**Flat fan-out producing sibling collisions.** When N parallel agents share a design space — they must produce distinct domains, consistent naming, or aligned structural choices — spawning them without prior scope assignment causes collisions. Each worker, seeing no other worker's brief, independently picks the same obvious path. Detecting this after the fact requires a second coordination round that costs more than preventing it would have. Before a flat fan-out, ask: could any two workers reasonably make the same design choice independently? If yes, a manager agent should assign scope before spawning.

**Orchestration landing in the wrong layer.** When a workstream has internal coordination needs, the orchestration must happen inside a manager agent — not in the main session across many turns. If the main session is absorbing worker outputs, mediating conflicts, and re-dispatching, it has become the orchestrator, consuming context that should be reserved for the human's interface. A manager agent owns the workstream end-to-end and surfaces only the consolidated result.

**More agents masking a bad brief.** A critic loop applied to bad input produces critiqued bad input. If the first result is bad, sharpen the brief before reaching for a second agent.

## Worked example

An event planner has produced a first draft of a 200-person wedding plan: venue and logistics, catering, a run-sheet from venue access through to carriages, three vendor contracts, and a risk register. A single end-to-end review will miss cross-domain conflicts — the reviewer focused on food safety will not catch the clause in the venue contract that prohibits outside catering without a supplement fee. The solution is a parallel fan-out of five specialist agents, each holding the full plan but briefed to evaluate only their domain.

The planner invokes `venue-logistics-critic`, `catering-critic`, `runsheet-critic`, `contracts-critic`, and `contingency-critic` simultaneously, each with a cold brief — no prior conversation, no hint of the others' scope — and a rubric tailored to the domain. The contracts agent is instructed to cross-reference the venue and catering sections for conflicts; the contingency agent is told to assume the three highest-probability failure modes and check whether the plan survives them. Each critic writes findings to a named output file: issue, location in the plan, severity (blocking / significant / minor). When all five finish, the planner reads each file directly rather than trusting completion messages, then invokes a `synthesis` agent briefed cold on all five critique files. The synthesis brief asks for: contradictions between critics, issues flagged by more than one domain (structural problems, not quirks), and a ranked list of blocking items by impact on the event date.

The pattern earns its cost because the five sub-tasks are genuinely independent, domain-specific bias would cause a single generalist reviewer to systematically miss problems outside their strongest area, and the event date is fixed — a contract clause cannot be renegotiated the week before. Where the cost of a confident wrong answer is a ruined wedding rather than an extra revision, the redundancy is cheap.

## When to add an agent vs sharpen the brief

The first move is almost always to improve the brief, not to add an agent. A second agent on a bad brief produces a second bad result. Before spawning anything, ask whether a clearer goal, a more explicit rubric, or more precise inputs would fix the problem at a single agent.

Add an agent when one of three conditions holds:

**(a) Independent perspective.** The work requires a viewpoint the original brief structurally cannot provide — a critic, reviewer, or second-opinion check. A single agent reviewing its own output cannot escape its prior framing; the fix is a second agent briefed cold.

**(b) Real parallelism.** The sub-tasks are genuinely independent and wall-clock time matters. Serial-by-nature tasks gain nothing from additional agents.

**(c) Cost of failure vastly exceeds the cost of the extra agent.** A second-opinion call on an irreversible decision costs one model call; the alternative may cost much more to recover from.

If none of those three conditions holds, you need a better brief, not another agent.
