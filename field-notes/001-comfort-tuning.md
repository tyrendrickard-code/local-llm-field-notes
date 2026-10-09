Tuning a 1B model like water temperature

*Methods and observations only. Larger work stays private.*

The metaphor: like a parent checking water temperature for a child, so they
don't get burned. Sampling parameters aren't performance knobs at this scale —
they're the band where a small model generates at its best versus where it
strains.

## What changed

| Setting | Was | Now | Why |
|---|---|---|---|
| Temperature | 0.7 | 0.5 | 0.7 is where the burns start; 0.5 keeps coherence while the curiosity stays |
| Top P | 0.95 | 0.9 | Trims the long tail of weird tokens a 1B reaches for |
| Repeat penalty | off (1.0) | 1.15 | Anti-loop nudge |
| Top K | 40 | 40 | Untouched |
| Min P | 0.05 | 0.05 | Untouched |
| Freq/present penalties | 0 | 0 | Deliberately — presence pushes *off* topic, and topic-drift is the strain signature here |

## The read

"Same spark, less burn." Less looping, fewer skid-marks, curiosity intact.
The full comparison (penalty-off at 0.7 vs 1.15 at 0.5) is still being observed.

## The principle

Dose the framework to the mind you actually have. A 1B doesn't need
enterprise tuning — it needs water at the right temperature.
