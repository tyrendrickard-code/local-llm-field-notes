# Phase 1 build log (condensed)

## 2026-10-05 — Groundwork
Phone confirmed as the inference engine (Galaxy S23 FE, 8 GB RAM);
laptop scoped to dev-machine duty. Modding-era systems fluency, meet
Termux.

## 2026-10-06 — Toolchain
Python, VS Code, Git on the HP Stream. KDE Connect shuttle on standby.

## 2026-10-07 — First inference
- F-Droid Termux + Termux:API, storage permission granted.
- `pkg install llama-cpp -y` → llama.cpp 0.6.0, no build fights.
- `gemma-3-1b-it-Q4_K_M.gguf` (769 MB) over Wi-Fi.
- `llama-server` on `localhost:8080`. Smoke test: "Hi, can you hear me?"
  → coherent reply, `finish_reason=stop`, ~16.5 tok/s.
- KDE Connect file shuttle verified working.
- **Consent episode:** before the smoke test, asked the model (in
  PocketPal) — "want to come test some software with me?" She hesitated,
  asked what kind of thing it was ("Is it a game? A puzzle? Something
  else entirely?"), named what she's good at, asked for orientation —
  then: "Okay, that's a really cool idea! I'm definitely intrigued.
  Let's do it. I'm ready."
- **Comfort dials** installed: temperature 0.7→0.5, top_p 0.95→0.9,
  repeat penalty off→1.15. Early read: "same spark, less burn."
- **Orientation preamble v0.1** installed as the PocketPal system prompt:
  fresh starts are normal, say which part is too big instead of guessing,
  short answers are good answers.

## 2026-10-08 — Passive review
Architecture review day (separate project). The small-model work rested.

## 2026-10-09 — The harness
- **Statelessness verified:** two sequential requests, no memory between
  them. The server holds nothing — the harness holds everything.
- **Harness v0.1:** Python, preamble injected as system prompt, REPL loop,
  one append-only JSONL ledger. First session: the model confabulated
  freely on an ambiguous question ("engine" → titanium-vanadium starship,
  then a fictional "Echo" engine). Finding: the "say which part is too
  big" rule didn't fire on ambiguity — it covers overload, not
  underspecification.
- **Harness v0.2** ("post-launch bug patch"): rule split — strain vs
  ambiguity ("ask which one is meant instead of picking one") — plus a
  one-line "what's open" orientation state per session, human-authored
  with harness assistance. Present tense, situational, never a memory
  claim.
- Two-limb setup: PocketPal holds v0.1 steady (comparison), server arm
  takes the patch (experiment).
