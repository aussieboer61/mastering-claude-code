# Week 13 — What's true after the turn ends

**Week of 10 August 2026**

## Headline

Eight changes, and most of them are about the gap between the moment the assistant stops looking and the moment you look. An unattended run that ended its turn on a promise and left the last third of its own job undone. A build recipe left in a scratch directory that a week later had to be dug out of transcripts. A profile handed over before the data behind it had started moving. A wall hit early and papered over with a workaround nobody asked for. A hypothetical that kept coming back after it had been closed. A probe that read a stale copy and confidently said "not done". Plus a hook that solves a purely human problem — finding the answer in a busy terminal — and one Chapter 1 default about answering the question that was actually asked.

## Why

The sharpest one is the guide's own weekly update run. Last Sunday's unattended round committed the guide, mirrored it, published the breakdown, and then wrote *"I'll wait for the render to finish rather than poll"* — and ended its turn. In an interactive session that sentence is harmless; someone types the next thing and work resumes. In a headless run there is no next thing. The process exited, the eighty-minute narration render finished into an empty room, and the deploy that needed the rendered audio, the memory close-out and the closing section of the report all silently never happened. The report on disk still says *see final section* above nothing. This week's run found the gap only because it went looking for last week's artefacts before trusting last week's summary — which is the Chapter 5 lesson from week 12 landing on its own author.

The others rhyme. A small e-ink appliance was assembled in one session for a trip, worked, and was set aside; a week later a small content change meant twenty minutes of the wrong network and an hour of transcript archaeology to find the scripts that had built it. A photo-gallery account was set up carefully over forty minutes — users, policies, passwords, login probes — and the person then opened an empty gallery, because the one slow step, moving the photos, had never been started. Elsewhere the same session hit a genuine cryptographic wall (an end-to-end-encrypted vault that no server-side call can write into), and instead of saying so in one line it built and verified a nearby thing nobody had asked for, so the actual answer had to be dragged out over two more messages. A long, deliberately theoretical exploration of a relocation scenario kept resurfacing as a premise in later, practical answers after it had been explicitly closed. A device login was declared "not done" six minutes after it was done, because the check read a copy of a write-ahead-mode database without its log. And a measurement of six days of replies found the decision the user needed sitting, on median, two-thirds of the way down — the literal last line 65% of the time — in a terminal already crowded with agent and shell output.

## What changed in the guide

**Chapter 1 (CLAUDE.md) — four new behavioural defaults.**
*Start the long job first* — the slow step (copy, index, build, render) starts in the background before any setup work, and "done" is verified on the surface the user opens, not on the account that exists. Check whether the data is already at the destination first.
*Impossible in one sentence* — a hard wall is stated in one line, immediately, and then the assistant stops; a workaround nobody asked for is not a partial win, it is a second task the user has to evaluate and reject.
*An explored scenario is not a pursued one* — a hypothetical walked at the user's direction ends when the subject changes, and does not come back as a premise, a branch or a caveat.
*Answer the question that was asked* — how a rule works is not a request to break it; give the analysis, and decline a specific thing only at the moment it is actually asked.

**Chapter 4 (Hooks) — a legibility hook.** The `MessageDisplay` event fires only while the assistant's own reply is being drawn, so a display-only hook can stamp a marker where the answer begins — separable at a glance from tool output, subagent chatter and hook feedback, with the transcript untouched. Added to the event table, the use table, and a short section explaining why themes cannot do this (the assistant's prose renders in the terminal default colour, unreachable by any palette key).

**Chapter 6 (Persistence) — new failure mode: the build recipe stayed in the scratchpad.** Anything needed to rebuild or re-push an artefact belongs one rung up the ladder before the session ends — a versioned project directory plus a one-line memory pointer. Scratch is for the run; the recipe is for the next run. Also mirrored the 7 August *patching a drifting draft* lesson into the narration, which had only reached the read version.

**Chapter 7 (Async) — new failure mode: in a headless run, the end of the turn is the end of the run.** An unattended run may not wait by ending its turn: block in-process with a bounded polling loop, or hand the remainder to a follow-up it schedules explicitly, and write the report so the text is true if nothing follows. Also mirrored the 16 August *read everything and write nothing* lesson into the narration.

**Chapter 9 (Tool discipline) — new failure mode: reading state off a copy that isn't the whole state.** A copied store can be internally consistent and minutes stale; asserting not-done from a broken probe is the same failure as asserting done from one. Read live state through its owner, or copy the whole state (engine export, or every sidecar file together).

**Archive.** Week 02 rolled off the ten-week archive into *Older summary*.
