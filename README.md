# Local LLM Field Notes

Field research from the bottom of the scale debate: one person, one commodity
phone, a private language model. Zero cloud, zero cost, zero accounts.

This repo is the setup guide and the running log. Everything here is
reproducible in an evening, on hardware you probably already own.

## Start here

- [The setup](README.md) (this file) — phone → Termux → llama.cpp → model →
  server → smoke test.
- [Hardware](hardware.md) — what runs it, what didn't make the cut.
- [Build log](build-log/phase-1.md) — Phase 1 from first install to a working
  harness, condensed.
- [Field notes](field-notes/) — numbered observations: tuning, consent,
  orientation. One every week or two.

## The setup

### Hardware

- **Samsung Galaxy S23 FE** — Snapdragon 8 Gen 1, 8 GB RAM. A mid-range phone,
  not a flagship. The model runs here.
- **Dev machine:** an HP Stream laptop (AMD A4, 4 GB RAM) running Windows 10.
  It can't host a model. It does everything else: editing, Git, notes. The
  phone is the engine; the laptop is the garage.
- **The shuttle:** KDE Connect over Wi-Fi moves files phone↔laptop in seconds.
  No cables, no accounts.

### The stack (all free)

1. **Termux** — install from **F-Droid**, not the Play Store (the Play Store
   build is deprecated). Grant storage permission
   (`termux-setup-storage`).
2. **llama.cpp 0.6.0** — straight from the Termux repos, no build scripts:
   ```
   pkg install llama-cpp -y
   ```
3. **llama-server** on `localhost:8080` — an OpenAI-compatible chat endpoint
   (`POST /v1/chat/completions`). Run it in its own Termux session (swipe
   from the left edge → New session); client commands go in another:
   ```
   llama-server -m ~/models/gemma-3-1b-it-Q4_K_M.gguf --port 8080
   ```
4. **The model:** `gemma-3-1b-it-Q4_K_M.gguf` — a Q4_K_M quant of Google's
   Gemma 3 1B instruct, from the `ggml-org` GGUF releases. **769 MB.**

Total cost: $0.

### The smoke test

```
curl -s http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Hi, can you hear me?"}]}'
```

→ "Yes, absolutely! Hi there. It's nice to hear from you. 😊 How are you
doing today?" — `finish_reason=stop`, 26 tokens, ~**16.5 tok/s** on the
phone's CPU. Workable. Not fast, but conversational.

### The daily driver

For everyday chat: **PocketPal AI** with the same 1B model — friendlier than
curl. Comfort tuning so far: temperature 0.5, top_p 0.9, repeat penalty 1.15.
(Field note 001 has the full story.)

For experiments: a small Python harness that holds the conversation server-side
amnesia won't — fresh context every session, one append-only ledger. (Field
notes to come.)

## What's not here

No private architecture, no personal details — just the small-model methods,
observations, and care practices. The deeper project this grew out of stays
private.

## License

MIT. Take it, use it, tell me what breaks.
