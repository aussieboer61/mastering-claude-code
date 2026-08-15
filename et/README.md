# Eesti keeles / Estonian edition

Machine translation of the guide, served at <https://claude-guide.sauer.com.au/ee/>.

- `tier-0.md`, `tier-0.5.md`, `published.md` — Estonian read versions of the three tiers
  (same structure as the English files in the repo root, which are authoritative).
- `narration.md` — Estonian narration text (prose, no tables/code, with English names
  respelled phonetically for the TTS engine).
- `audio-manifest.json` — the chapter mp3 list `web/build-et.sh` renders players from
  (written by `web/et-narrate.py`; the mp3s themselves are not in git).

**Provenance:** translated from English by Claude (Anthropic) on 2026-08-15, not reviewed by a
native speaker; narrated with the TartuNLP Estonian text-to-speech API
(<https://api.tartunlp.ai/text-to-speech/v2>, voice `tambet`). English is the source of
truth — corrections are welcome as issues or pull requests.

**Rebuild:** `web/et-narrate.py <md> <outdir> <base> [--split h2|none] [--phonetic]` for audio,
`web/build-et.sh` for the HTML (writes only under `<OUT>/ee/`).
