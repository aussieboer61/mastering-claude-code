# Pillar 4 — Hooks & Guardrails

## Principle

The hook system is the harness's enforcement layer — a set of shell commands wired to lifecycle events in the Claude Code session, executed deterministically outside the model's control. Unlike a CLAUDE.md instruction or a memory file, a hook cannot be misread, forgotten, or overridden by a confident-sounding response. It runs in your shell, as your user, before or after the event it is attached to, every single time. Use a hook when the behaviour **must** happen — not "should happen when I remember to ask" — but must, unconditionally, on every invocation.

## Why it matters

There is a meaningful gap between "I told Claude to do X every time" and "a hook does X every time." An instruction in CLAUDE.md can be followed faithfully a hundred times and silently skipped on the hundred-and-first if the context window is crowded or the phrasing is ambiguous. A hook has no such failure mode: exit code zero means continue, non-zero means block, and the assistant never sees the tool call if the hook says no. This matters most in four situations: **safety** (prevent writes to protected paths), **context injection** (inject current state that the assistant cannot discover on its own), **notification** (fire an alert the moment something completes or fails), and **audit** (append a timestamped record to a log regardless of what the assistant decides to do).

## Components

### Events

Claude Code exposes the following lifecycle events you can attach hooks to:

| Event | When it fires |
|---|---|
| `SessionStart` | Once, immediately after the session initialises |
| `UserPromptSubmit` | Each time the user submits a message, before the model processes it |
| `PreToolUse` | Before any tool call executes |
| `PostToolUse` | After a tool call returns, before the model continues |
| `Stop` | When the assistant finishes a turn (the main agent stops) |
| `SubagentStop` | When a subagent finishes its turn |
| `Notification` | When Claude Code emits a user-facing notification (e.g., "waiting for input") |

`PreToolUse` and `PostToolUse` support a `matcher` field — a substring or regex matched against the tool name — so you can scope a hook to only `Write` calls, only `Bash` calls, or any subset you need.

### Configuration in settings.json

Hooks live in `~/.claude/settings.json` (user scope, applies to all projects) or `.claude/settings.json` at the project root (project scope, applies only in that directory tree). Project scope takes precedence over user scope for the same event and matcher. The structure is:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "/path/to/your/script",
            "statusMessage": "Loading context..."
          }
        ]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "/path/to/guard-script"
          }
        ]
      }
    ]
  }
}
```

Each event key maps to an array of hook group objects. Each group can have a `matcher` (omit or set to `""` to match all tools) and an array of `hooks`. The optional `statusMessage` string is shown in the session UI while the hook runs.

### What a hook receives

Hook commands receive the event payload as JSON on **stdin**. For tool-use events the payload includes at minimum `tool_name` (e.g., `"Write"`, `"Bash"`) and `tool_input` (the tool's arguments — `file_path`, `command`, etc.). A `PreToolUse` hook for `Write` can therefore read the target path from `tool_input.file_path` and make an access decision before the write happens.

### Exit codes and their meaning

| Exit code | Meaning |
|---|---|
| `0` | Approved — the lifecycle event proceeds normally |
| Non-zero | Blocked — the tool call is cancelled; Claude Code surfaces the reason to the assistant |

For `PreToolUse`, a non-zero exit stops the tool call entirely. The assistant sees the block reason (if you emit one) and can explain it to the user or try an alternative. For `PostToolUse`, a non-zero exit does not undo the tool call (it already ran) but does surface the failure message into the conversation. For `SessionStart` and `Stop`, a non-zero exit is logged but does not abort the session.

### Output back to the assistant

A hook can inject text back into the conversation by writing a specific JSON structure to **stdout**:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Today is 2026-04-26. The project is in draft status."
  }
}
```

This appears as a system reminder in the assistant's context — it is not shown verbatim to the user but is visible to the model. Use this for context injection: pinned facts, current system state, file-path policies, or anything the assistant needs to know at the start of every session or before every write.

For a blocking decision, emit the reason with:

```json
{
  "decision": "block",
  "reason": "This path is frozen. Obtain approval before editing."
}
```

## How to apply it

**Start with one `SessionStart` hook.** The minimum useful hook injects today's date and a one-line status check. Something like:

```bash
#!/usr/bin/env bash
DATE=$(date '+%Y-%m-%d')
jq -n --arg d "$DATE" '{
  hookSpecificOutput: {
    hookEventName: "SessionStart",
    additionalContext: ("Today is " + $d + ". Run hostname before any host-specific action.")
  }
}'
```

This alone closes a common gap: the assistant otherwise has no reliable access to the current date unless you happen to mention it.

**Add a `PreToolUse` guard for destructive paths.** Once the SessionStart hook is working, identify the paths or operations in your workflow that must never be touched without explicit approval. Write a guard script that reads the target path from stdin, checks it against your protected list, and exits non-zero with a `"decision": "block"` JSON payload if it matches. Register it against `Write|Edit|MultiEdit`.

**Add a `Stop` hook for notifications.** When the assistant finishes a turn, fire a notification. Even a simple `curl` call to a webhook is enough. This is especially valuable for long-running or headless sessions where you are not watching the terminal. (The notification ecosystem is covered in depth in Pillar 6.)

**Debug by logging.** Hooks run in your shell — add `set -x` and redirect stderr to a log file during development:

```bash
exec 2>> /tmp/hook-debug.log
set -x
```

Remove before production. You can also dry-run a hook manually by piping a synthetic payload:

```bash
echo '{"tool_name":"Write","tool_input":{"file_path":"/sensitive/path/file.txt"}}' \
  | /path/to/guard-script
```

Check both the exit code and stdout to confirm the hook behaves as expected.

## Failure modes

**Silent failure.** A hook that exits non-zero on an unexpected error (e.g., `jq` not installed, a dependency missing) will block tool calls without a useful reason message. Guard scripts should trap errors and emit a `"reason"` string that tells the user what went wrong, not just a bare non-zero exit.

**Context-window bloat from `SessionStart`.** A hook that injects a large document on every session start eats token budget that could go toward actual work. Keep `additionalContext` focused: the current date, a pointer to where to look, a one-line status. If you need richer context, have the hook summarise or index — not dump — the full content.

**Overbroad `PreToolUse` matchers.** A guard that blocks all writes to a directory will also block legitimate writes the assistant needs to make in the normal course of work. Be precise: match on exact path prefixes, not the whole filesystem. Include a bypass mechanism (a one-shot unlock file, a flag, or explicit user confirmation) so legitimate work is never permanently blocked.

**Encoding behaviour in memory that needs to be a hook.** If a rule is important enough that the work is wrong without it, it belongs in a hook, not in CLAUDE.md. The assistant can miss, misread, or deprioritise a CLAUDE.md instruction when context is tight. It cannot ignore an exit code. The test: would it matter if this rule were skipped once? If yes, make it a hook.

**Host-specific hooks without environment checks.** A hook that calls a tool only available on one machine (a specific binary, a mounted path, a service endpoint) will fail silently or noisily on any other machine where the same settings.json applies. Either check for the dependency inside the hook and exit 0 gracefully when it is absent, or scope the hook to project-level settings that only apply in the relevant working directory.

## Worked example

A legal research workflow maintains a set of source documents that have been marked "approved and frozen" — they have been reviewed by a human, their citation details verified, and they must not be altered by any automated process. The documents live in `~/research/approved/`. The rest of `~/research/drafts/` is freely editable.

A `PreToolUse` hook is registered against `Write|Edit|MultiEdit` in the user-level `settings.json`. The script reads `tool_input.file_path` from stdin, resolves it to an absolute path, and checks whether it falls inside `~/research/approved/`. If it does, the hook emits a `"decision": "block"` payload with the reason `"This document is frozen. To make a change, move it back to drafts/ and re-run the approval workflow."` and exits 0 (the decision field carries the block, not the exit code).

```bash
#!/usr/bin/env bash
PAYLOAD=$(cat)
TARGET=$(jq -r '.tool_input.file_path // .tool_input.notebook_path // empty' <<<"$PAYLOAD")
[ -z "$TARGET" ] && exit 0

ABS=$(realpath -m "$TARGET" 2>/dev/null || echo "$TARGET")
APPROVED=$(realpath -m "$HOME/research/approved")

case "$ABS" in
  "$APPROVED"/*)
    jq -n --arg p "$ABS" '{
      decision: "block",
      reason: ("Frozen document: " + $p + ". Move to drafts/ and re-run approval workflow before editing.")
    }'
    exit 0
    ;;
esac
exit 0
```

The assistant never modifies a frozen document, not because it was instructed not to, but because the harness physically stops the write. If the assistant attempts it, it receives the block reason in its context and can explain to the user what needs to happen next. The rule is enforced the same way on every session, by every version of the model, regardless of how the prompt was phrased.

## Hook vs prompt vs skill

The decision rule is: **hook** when the behaviour must happen every time regardless of what the model is thinking; **prompt or CLAUDE.md** when the behaviour should happen most of the time and a miss is recoverable; **skill** when the behaviour is an action the user explicitly invokes on demand. A hook that fires on `PreToolUse` is not a request — it is a gate. A CLAUDE.md entry saying "always check the style guide" is a standing instruction — useful, often followed, but not enforced. A `/style-check` skill is a packaged action the user runs when they want it. Put safety and invariants in hooks. Put preferences and reminders in CLAUDE.md. Put reusable procedures in skills.
