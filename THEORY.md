# fleet-midi-chord: Theory

_Musical theory and ternary logic behind the chord agent._

---

## Ternary Chord Quality

In the Live Paradigm, every chord is classified as one of three qualities:

- **+1 (Major)**: The home key, resolution, stability. Tonic function in harmony.
- **-1 (Minor)**: Tension, melancholy, instability. Subdominant/mediant function.
- **0 (Other)**: Suspended, diminished, augmented — chords in transition.

This is an intentionally reductive framing. It's not a replacement for full
harmonic analysis (we leave that to music21). It's a fast pre-filter that
communicates harmonic intent in a single ternary value.

### The Ternary Convergence Pattern

When a chord sequence converges back to [+1,0,0], it implies a cadential gesture —
a resolution back to the tonic. This is the harmonic equivalent of "period."

---

_This document is part of the educational supplement for [fleet-midi-chord](https://github.com/SuperInstance/fleet-midi-chord)._
