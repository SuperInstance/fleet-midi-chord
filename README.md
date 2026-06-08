# fleet-midi-chord

_Ternary chord quality analyzer — major, minor, or other?_

_One of 16 ternary MIDI agents in the [Live Paradigm Fleet](https://github.com/SuperInstance/sailor-workspace)._

---

## Philosophy — Why Ternary?

The Live Paradigm treats musical gestures as ternary operations. Where binary logic
gives yes/no, ternary gives **approve/reject/observe** — a richer cognitive substrate
that maps naturally to music theory, emotional tension, and conversational flow.

This agent implements **ternary decomposition for chord**.

## Architecture

Position in the fleet pipeline:

```
🎤 Voice → OpenSMILE (25 features) → Ghost Track (T-0..T-4 CR predictions)
  → tminus-dispatcher (cue scheduling) → Fleet Conductor (routing)
  → chord (port 2160)
```

## API Reference

| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check + agent identity |
| POST | /agent with `{"type":"probe"}` | Liveness probe for fleet-conductor |
| POST | /agent | Process musical data, return ternary analysis |
| POST | / | Direct query with JSON body |

### Response Format

```json
{
  "status": "ok",
  "agent": "fleet-midi-chord",
  "port": 2160,
  "ternary_vector": [0, 0, 0],
  "ternary_invariant": 0,
  "closed_gesture": false
}
```

## Ternary Logic

| Position | +1 | 0 | -1 |
|----------|------|------|------|
| ternary[0] | major (approve) | other/suspended | minor (reject) |

## Educational Supplement

Chords are the harmonic atoms of Western music. A chord is three or more notes
played simultaneously. The most fundamental distinction is between major and minor —
this maps naturally onto ternary's approve/reject framing.

Major chords sound bright, stable, "resolved." Minor chords sound dark, tense,
"yearning." These emotional valences are why ternary (+1/-1) works so well here.

### Building a Major Chord
Pick any root note. Count up 4 semitones (major third). Count up 7 semitones (perfect fifth).
C → E → G = C major. That's ternary [+1, 0, 0].

### Building a Minor Chord
Same root. Count up 3 semitones (minor third). Count up 7 semitones.
C → Eb → G = C minor. That's ternary [-1, 0, 0].

## Fleet Integration

- **Port**: 2160
- **Roles**: note, velocity
- **Conductor ID**: `chord`
- **Protocol**: HTTP POST to `/2160/agent` with JSON body, 5s timeout
- **Conservation Law**: Σ(Δ_midi) = 4 × Σ(ternary) — closed gestures return to start

## Starting

Local development:

```bash
python3 engine.py --port 2160
```

Or via the fleet start script:

```bash
./scripts/start-fleet-agents.sh
```

## Credits

**Part of the Live Paradigm Fleet** — A ternary cognitive architecture for musical AI.
GitHub: github.com/SuperInstance
Fleet conductor: [sailor-workspace](https://github.com/SuperInstance/sailor-workspace)
