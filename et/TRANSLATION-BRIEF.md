# Translation brief — "Mastering Claude Code" → Estonian

You are translating one chunk of a public guide about Claude Code (Anthropic's terminal AI assistant) from English into **natural, fluent, idiomatic Estonian**, as a skilled native technical translator would. Not word-for-word: keep the meaning, the wry plain-spoken voice, the paragraph structure and the sentence-level flow. Address the reader as **sina** (informal singular), consistently. Prefer clear everyday Estonian over anglicisms wherever a good Estonian term exists.

## Hard rules
1. Output ONLY the translated markdown, written to the output path given. No preamble, no notes, no English left untranslated except where the rules below say to keep it.
2. Preserve markdown structure EXACTLY: same heading levels and order, same lists, same tables (same number of columns and rows; translate the cell text), same blockquotes, same emphasis, same horizontal rules, same links (translate link text, keep URLs).
3. Code fences: keep code, commands, file paths, flags, YAML/JSON keys, environment variable names, hook event names, tool names, and slash-command names VERBATIM. Human-readable prose inside example files or example prompts (e.g. an example CLAUDE.md, an example skill body, the Annex system prompt) MAY be translated, keeping the syntax intact. Comments in code may be translated.
4. Never translate: `Claude Code`, `Claude`, `Anthropic`, `CLAUDE.md`, `MEMORY.md`, `SKILL.md`, `settings.json`, tool names (Bash, Read, Edit, Grep, Glob, Agent, TodoWrite, WebFetch…), hook event names (PreToolUse, PostToolUse, UserPromptSubmit, Stop, SessionStart…), slash commands (`/retro`, `/plan`…), file/dir names, `MCP`, `API`, `git`, `GitHub`, product names.
5. Do not add, drop or reorder content. Do not add translator notes. Do not summarise.
6. Keep any `<!-- -->` comments and any HTML as they are.

## Glossary — use these consistently (first use may add the English in brackets, e.g. „haagid (hooks)")
- the nine pillars → üheksa sammast (pillar → sammas)
- CLAUDE.md, "a standing letter to your assistant" → CLAUDE.md, „seisev kiri sinu abilisele"
- assistant → abiline
- memory (the pillar) → mälu; memory file → mälufail; memory store → mälusalv
- skill(s) → oskus(ed); skill file → oskusefail
- hook(s) → haak / haagid
- subagent(s) → alamagent / alamagendid; agent → agent
- session → seanss; conversation → vestlus
- prompt (noun) → viip; system prompt → süsteemiviip; to prompt → viipa andma / paluda (by sense)
- context window → kontekstiaken; context → kontekst
- persistence ladder → püsivuse redel; persistent → püsiv; state → olek
- async / asynchronous → asünkroonne; background task → taustatöö
- multi-agent patterns → mitme agendiga mustrid; second pair of eyes → teine silmapaar
- tool discipline → tööriistadistsipliin; tool → tööriist; tool call → tööriistakutse
- terminal → terminal; command line → käsurida; command → käsk
- repository / repo → repositoorium / repo
- workflow → töövoog; task → ülesanne; failure mode → tõrkemuster (or „läbikukkumise muster" by sense); gotcha → lõks
- scope (user/project scope) → ulatus (kasutaja ulatus / projekti ulatus)
- token(s) → token(id); model → mudel; the model → mudel
- plain text → lihttekst; markdown → markdown; file → fail; folder/directory → kaust
- Tier 0 / Tier 0.5 / Tier 1 → 0. tase / 0,5. tase / 1. tase (in headings you may write „Tase 0")
- "the curious" (as in "for the curious") → uudishimulikele
- walked example → läbikäidud näide
- chat box → vestlusaken; browser tab → brauseri vaheleht
- non-coder / people who have never written code → inimesed, kes pole kunagi koodi kirjutanud

## Extra rules for NARRATION chunks only (files n1…n6)
This text is fed to an Estonian text-to-speech engine (TartuNLP) and heard, not read. So:
- Flowing prose only. No tables, no code, no markdown emphasis that carries meaning (keep `#`/`##` headings — they are used to split the audio into chapters — and keep `---` rules).
- Spell numbers out as Estonian words in the right case („üheksa sammast", „viis peatükki", „kolmsada PDF-i"), except years, which may stay digits.
- Where the English narration spells things for the ear (e.g. „CLAUDE-dot-em-dee"), do the Estonian equivalent: „CLAUDE punkt em-dee".
- Write unavoidable English proper names the way an Estonian TTS should say them, phonetically in Estonian orthography: Claude Code → „Klood Koud", Claude → „Klood", Anthropic → „Antroopik", ChatGPT → „Tšätt Džii Pii Tii", GitHub → „Githab", MCP → „em-tsee-pee", API → „aa-pee-ii", JSON → „džeison", YAML → „jaml", Bash → „bäš", Python → „paiton", markdown → „markdaun", terminal → terminal (fine). Slash-command names like /retro → „kaldkriips retro". Tool names (Read, Edit, Bash) → say them phonetically („Riid", „Edit", „Bäš"). Hook event names → spell them phonetically („Pri-Tuul-Juus"). File names: CLAUDE.md → „CLAUDE punkt em-dee", settings.json → „settings punkt džeison". Use your judgement so a listener understands.
- Prefer the Estonian glossary term over the English word every time it appears in narration.
