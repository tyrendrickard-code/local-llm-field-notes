# Hardware

## What runs the model

**Samsung Galaxy S23 FE** (SM-S711U)
- Snapdragon 8 Gen 1, 8 GB RAM
- Gemma 3 1B Q4_K_M (769 MB) via llama.cpp server: ~16.5 tok/s on CPU
- A mid-range phone, not a flagship. That's the point.

## What doesn't run the model (and why it's still essential)

**HP Stream laptop** — AMD A4-9120e, 4 GB soldered RAM (~1.5 GB usable),
Windows 10 (can't take 11). It cannot host a model. It does everything else:
Python, VS Code, Git, editing, notes. The phone is the engine; the laptop is
the garage.

## The shuttle

**KDE Connect** over Wi-Fi, phone↔laptop. Verified working. Files move in
seconds, no cables, no accounts. (Wi-Fi only — no mobile data in this setup.)

## What didn't make the cut

- **Play Store Termux** — deprecated; F-Droid build only.
- **Building llama.cpp from source** — unnecessary; the Termux repos carry
  0.6.0 and it installs clean with `pkg install llama-cpp -y`.
- **The laptop as model host** — 1.5 GB usable RAM ends that conversation.
