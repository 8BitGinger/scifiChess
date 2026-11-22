# Nova Gambit

**Sci-fi 3D chess in the browser.** Command the cyan **Aegis Fleet** against the crimson **Void Armada**, a computer opponent, on a holographic board floating in deep space. Every capture plays as a short cinematic attack scene.

---

## Features

- **Full 3D board and pieces** built in Three.js with glow, bloom and shadows
- **Cinematic attack scenes:** each capture adds letterbox bars, moves the camera in and plays an attack based on the attacking piece, ending in an explosion with debris
- **Computer opponent** with three difficulty levels, running in a background Web Worker so the game never freezes
- **Full chess rules:** castling, en passant, pawn promotion, check, checkmate, stalemate and draws
- **Synthesized sound effects** using the Web Audio API, so there are no audio files to load
- **Undo, battle log and captured-unit tally**
- **Orbit and zoom** the camera with mouse or touch

## Unit Codex

| Unit | Chess piece | Attack style |
|------|-------------|--------------|
| Drone | Pawn | Burst of three plasma bolts |
| Raptor | Knight | Leaps into the air and dive-bombs the target |
| Oracle | Bishop | Sustained crystal beam |
| Bastion | Rook | Twin heavy cannon shells with recoil |
| Empress | Queen | Three beams fired at once |
| Sovereign | King | Shockwave rings plus a finishing beam |

## How to Play

1. Open `index.html` in a modern browser (Chrome, Edge, Firefox or Safari).
2. Click one of your **cyan** units. Its legal moves light up:
   - ◯ cyan rings mark open squares
   - ◇ red diamonds mark enemy units you can attack
3. Click a marked square to move. The Void Armada replies automatically.
4. Checkmate the enemy **Sovereign** to win.

### Controls

| Action | Input |
|--------|-------|
| Select / move | Click or tap |
| Orbit camera | Drag |
| Zoom | Scroll wheel or pinch |
| Skip attack scene | **Skip** button, `Space` or `Esc` |

### Toolbar

- **New game:** reset the board
- **Undo:** take back your last move and the AI's reply
- **Difficulty:** Cadet (easy, makes mistakes), Commander (default) or Admiral (searches deepest)
- **Attack scenes:** turn the capture cinematics on or off
- **Sound:** mute or unmute
- **Reset view:** return the camera to its default angle

## Running It

There's no build step. It's a single self-contained HTML file.

```bash
# Option 1: just open it
open index.html

# Option 2: serve it locally (recommended for Web Worker support)
npx serve .
# or
python -m http.server 8000
```

Three.js r128 and its post-processing add-ons load from the jsDelivr CDN, so you need an internet connection on first load.

## Tech Notes

- **Rendering:** Three.js r128 with OrbitControls, EffectComposer, UnrealBloomPass and GammaCorrectionShader
- **Pieces:** built procedurally from primitive shapes, with no external model files
- **Engine:** custom JavaScript move generator, verified with perft tests:
  - Starting position: 20 / 400 / 8,902 / 197,281
  - "Kiwipete" test position: 48 / 2,039 / 97,862
- **AI:** negamax search with alpha-beta pruning, quiescence search, captures searched first (MVV-LVA ordering) and piece-square table evaluation
  - Cadet searches 1 ply with random noise
  - Commander searches 2 ply
  - Admiral searches 3 ply
- **Audio:** sound effects are generated live with Web Audio oscillators and filtered noise

## Known Limitations

- The player always controls the Aegis Fleet (white)
- Pawns always promote to an Empress (queen)
- There's no threefold-repetition draw detection
- Bloom post-processing may run slowly on low-end mobile devices

## Roadmap Ideas

- [ ] Play as the Void Armada
- [ ] Choose which piece a pawn promotes to
- [ ] Custom `.glb` models made in Blender
- [ ] Original soundtrack and ambient score
- [ ] Online two-player mode
- [ ] Opening book and time-limited deeper search for the Admiral level

---

*Nova Gambit: every capture is a battle.*
