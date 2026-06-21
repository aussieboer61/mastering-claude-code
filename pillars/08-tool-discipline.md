# Pillar 8 — Tool Discipline

## Principle

Every tool call has a cost — latency, tokens consumed, context window space occupied, and sometimes a permission prompt that pulls the human back into the loop — and a value, which is the information or change it produces. Mature tool use is the habit of reaching for the cheapest tool that produces the needed value, and of batching independent calls into a single assistant turn so that wall-clock time stays short and the context cache stays warm. The goal is not to minimise tool calls for their own sake; it is to make every call count, so that the workflow feels fast and legible rather than sluggish and cluttered.

## Why it matters

The same task done with the wrong tools is slower, noisier, more permission-prompt-heavy, and consumes more of the context window than necessary — that context space is a finite resource you need for reasoning, not for raw file dumps. A session that reaches for `cat` instead of `Read`, serialises five independent searches instead of batching them, or pulls a 30KB log file into the main context instead of delegating it, will feel hesitant and expensive compared to one that uses the right tool in the right configuration. Done well, tool discipline is largely invisible: the session finds what it needs quickly, changes only what it should, and leaves the context holding distilled information rather than noise.

## Components

**Dedicated file tools (Read / Edit / Write) over shell equivalents.** `Read` renders output with line numbers, which makes it auditable and makes subsequent edits precise. `Edit` records a structured diff that is reviewable at a glance and is safer than `sed` because it requires you to state the exact string to replace — it will refuse if the string is ambiguous or absent. `Write` creates or overwrites a file atomically. All three generate clean audit trails and avoid the permission prompts that Bash commands typically trigger. Reserve Bash for genuine shell work: running a test suite, invoking a build tool, querying a running process, anything that is inherently a subprocess.

**Search tools (Grep / Glob) for known targets; a subagent for open-ended sweeps.** When you know what you are looking for — a function name, a config key, a phrase across a set of documents — `Grep` is the right entry point: it runs fast, returns only the matching lines with context, and does not load irrelevant content. `Glob` finds files by pattern when you know the shape of the path but not its exact location. Neither is the right tool when you do not yet know what you are looking for; in that case, fan out a fast exploration-style subagent and ask it to return a structured map rather than serialising twenty reads yourself.

**Parallel tool calls in one assistant turn for independent work.** If two or more tool calls do not depend on each other's results, issue them in the same turn. The runtime is bounded by the slowest call rather than their sum, and the context cache benefits from receiving all results together. Sequential tool calls should be the exception, reserved for genuine dependencies: you need the result of call A before you can form call B.

**Deferred tools and ToolSearch.** Most tools are not loaded by default. Before reaching for a one-off ToolSearch to load a single tool, ask whether there is a logical bundle that addresses the whole task. A single ToolSearch query that names the toolkit (for example, the name of an MCP server) returns the entire set of related tools in one round-trip. Load what you need for the task at hand; do not load more than that, because every loaded tool consumes a small amount of system-prompt space and adds noise to the tool-selection decisions the model makes.

**MCP servers as task-appropriate toolkits.** When a task involves a specific external system — a browser, a database, a version-control host, a calendar, a native application — there is usually a tiered set of options: a dedicated MCP for that system, a general-purpose browser MCP, and finally computer-use as a last resort. Prefer the most specific tier available. A dedicated MCP uses the system's API directly: it is fast, returns structured data, and does not depend on screen layout. A browser MCP can navigate and extract from any web interface but is slower and more fragile than a native API. Computer-use can operate any visible desktop application but interprets pixels, which is brittle and slow. Reach down the tier list only when the upper tiers are unavailable or insufficient for the task.

**Subagent as context buffer.** When a tool call would return a large payload — a full log file, a lengthy document, a bulk database result, a large directory listing — consider whether you actually need all of it in the main context. If what you need is a summary, a count, a list of anomalies, or the answer to a specific question, delegate the retrieval and interpretation to a subagent. The subagent does the heavy reading; you receive 200 words back instead of 25 kilobytes. This is not primarily about cost; it is about keeping the reasoning context clean. A context window cluttered with raw data is a context window where your judgment calls compete with noise.

**Right host, not just right tool.** Tool selection does not end with choosing the right function call — it extends to choosing the right execution environment. If you have a fast-feedback orchestrator host and a separate heavy-compute executor host, long-running work (builds, test suites, ETL jobs, large data processing) belongs on the executor, not the orchestrator. The orchestrator's job is responsiveness; the executor's job is throughput. Running heavy work on the orchestrator degrades the interactive loop even when the executor is sitting idle. Before kicking off any long-running subprocess, ask: which host is built for this? Route accordingly. The same principle applies beyond compute: any fast-feedback loop paired with a heavy backend should push the heavy work to the backend, whether that is a render farm, a build cluster, a database server, or a long subagent run that should not block the main session.

## How to apply it

**Step 1 — Default to dedicated tools.** Before writing a Bash command to read, edit, or write a file, ask whether Read, Edit, or Write covers the need. They usually do. Reserve Bash for tasks that are intrinsically subprocess work: compiling, running tests, restarting a service, querying a live system state.

**Step 2 — Batch independent calls before issuing them.** Pause before each assistant turn and check: are any of these calls independent? If yes, issue them together. This habit compounds — a session that consistently batches parallel work finishes faster and uses the context cache more efficiently than one that serialises by default.

**Step 3 — Fan out searches in parallel when you do not know where something lives.** Do not serialise: search one directory, find nothing, search another. Issue all plausible search locations in parallel and collect the results in one pass.

```
# Instead of:
Grep("MyConfig", "/project/src")          # wait
Grep("MyConfig", "/project/config")       # wait
Grep("MyConfig", "/project/tests")        # wait

# Issue all three in one turn:
Grep("MyConfig", "/project/src")
Grep("MyConfig", "/project/config")
Grep("MyConfig", "/project/tests")
```

**Step 4 — Route large outputs through a subagent.** Before issuing a tool call, estimate its output size. If it is likely to exceed a few hundred lines, or if what you actually need is a derived answer rather than the raw content, spawn a subagent with a tight brief. Ask it to return the answer, the summary, or the anomaly list — not the raw file.

**Step 5 — Watch for repeated permission prompts and allowlist them.** If the same class of Bash command keeps triggering a permission dialog, that is a signal to evaluate whether it should be allowlisted. A recurring prompt for a safe, predictable command is friction that slows the session without adding safety value. Conversely, a prompt for a command that modifies shared infrastructure is friction that is earning its keep; do not remove it.

**Step 6 — Load deferred tools in bundles, not one at a time.** When a task requires a toolkit you have not yet loaded, use a single ToolSearch query that names the toolkit at the server or category level. One call returns the full set; picking tools one-by-one costs one round-trip per tool and invites you to under-load, leaving yourself without a tool you will need two steps later.

## Failure modes

**Reading a file with Bash `cat` instead of `Read`.** The output arrives without line numbers, bypasses the dedicated tool's audit trail, and usually triggers a permission prompt. The only winner is familiarity — `cat` feels natural because it always has. It is never the right choice when `Read` is available.

**Editing a file with `sed` instead of Edit.** `sed` requires you to write a correct regex, applies it blindly to all matches, and leaves no diff to review. Edit's `old_string` / `new_string` contract forces you to be explicit about what you are changing, fails safely when the target string is not found, and produces a reviewable diff. Use `replace_all` when you genuinely mean every occurrence; use the default (single-match) mode when you mean one specific site.

**Serialising independent searches.** Waiting for each Grep to return before issuing the next one when all queries are independent is pure dead time. The habit of serialising everything "to be safe" is not safe; it is just slow. Sequential ordering is only warranted when result B depends on result A.

**Loading deferred tools one by one.** Discovering you need a browser tool, loading it, using it, discovering you also need a second browser tool, loading that — each discovery costs a round-trip that a single ToolSearch on the server name would have avoided. When you know you are entering a new tool domain, load the bundle first.

**Pulling a large result into the main context when a summary would do.** A 20KB log file in the main context occupies space that would otherwise hold your reasoning about what to do next. If you needed "find any errors in this log", the log itself is not what you needed — the list of errors is. Delegate retrieval and interpretation together; bring back only the derived result.

**Reaching for computer-use when a native MCP is available.** Computer-use is the right tool for native desktop applications with no API and no browser interface. It is not the right tool when a dedicated MCP or browser MCP would do the same job faster and more reliably. Pixel-based interaction breaks on layout changes; API-based interaction does not.

**Running heavy work on the orchestrator host.** When the session is running on a lightweight or interactive host and a more capable executor is available, routing long-running work — builds, test suites, bulk processing — to the local host instead is a tool-discipline failure. The symptom is "everything feels slow" even though the executor is idle. The cause is conflating two different jobs: the orchestrator host keeps the fast feedback loop open; the executor host absorbs throughput. Correct by checking which host is in front of you, then ssh-delegating any long subprocess to the executor before starting it.

## Worked example

A research historian is working through a large archive of digitised field notes — several hundred plaintext files spread across thematic subdirectories. She needs to find all references to a specific surveying instrument across the entire corpus, then read just the passages where it appears, then edit a draft essay to replace an outdated name for the instrument with the term she has confirmed is correct.

Her first instinct is to open the files one at a time. She reads the first directory using Bash `ls`, reads ten files in sequence with `cat`, and finds two references — but the session's context is now carrying most of those ten files, most of which contained nothing useful. She is 10% through the archive and her context is already cluttered.

She resets and applies tool discipline. She issues a single `Grep` call targeting the instrument name across the entire archive root with recursive matching, which returns 23 matches across 14 files with their line numbers and surrounding lines — in one turn, in a few hundred tokens, with nothing irrelevant loaded. She then fans out 14 parallel `Read` calls, each scoped to a narrow line range around the match, collecting only the relevant passages. Her context now holds exactly the material she needs. Finally, she uses `Edit` with `replace_all` to rename the instrument throughout her draft essay — one call, no regex, a clean diff to confirm before proceeding. The entire task takes three assistant turns instead of several dozen, and the context window holds evidence and reasoning rather than hundreds of lines of files that contained no references at all.

The shift was not about working harder. It was about matching the tool to the actual information need at each step: search to locate, targeted Read to retrieve, Edit to change precisely.

## A short rule of thumb

Use the most specific tool that does the job. Batch every independent call into the same turn. Route large outputs through a subagent and bring back only the derived result. Load deferred tool bundles once, not one tool at a time.
