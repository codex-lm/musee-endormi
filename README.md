# Le Musée endormi · The Sleeping Museum · El museo dormido

A turn-based stealth puzzle set in a museum at night. You are a small creature
who must collect the enchanted gems and reach the exit — without ever ending a
turn in a guard's lantern beam.

**Play**: `index.html` is fully self-contained (no build, no dependencies,
no network). Open it in any browser. Also available via GitHub Pages.

## Rules

- Grid board, seen from above. On your turn, **move one cell** (arrows,
  WASD/ZQSD, or the on-screen pad) or **wait**.
- After each of your actions, every guard takes one step of its patrol, or a
  sentry statue turns its gaze one quarter. All guard behaviour is
  **fully deterministic** — no randomness.
- The pale beam is a guard's lantern. **Ending your turn on a lit cell, or
  touching a guard, means capture** — the level restarts immediately.
- **Stone walls and tall display cases block the light.** Behind glass you
  are invisible.
- Collect every enchanted gem, then reach the exit door (it lights up green
  once the last gem is yours).
- The **decoy** (once per level) distracts the nearest guard for two turns:
  it stops walking and stops watching.
- Finish a level **at or under the target number of moves** to earn its
  medal. Targets are the true optimum found by the built-in solver.

Eight short levels introduce the rules one by one: one guard, then vision
blocking, a rotating statue, the decoy (level 4 cannot be solved without it),
then two and three guards in step.

## Controls

| Input | Action |
|---|---|
| ↑ ↓ ← → / WASD / ZQSD | move |
| Space | wait one turn |
| L or X | throw decoy |
| U | undo |
| R | restart level |
| touch | on-screen D-pad + Wait / Decoy / Undo |

Languages: **English (default), Français, Español** — switch any time, the
choice is remembered.

## Development

- Single static file: `index.html` (engine, solver, UI, i18n, synthesized
  WebAudio sounds — no assets, no libraries).
- The engine is pure and deterministic: `applyAction(state, action)` returns
  the next state; `watchedBy(state)` computes lit cells (walls and vitrines
  block rays); `solve(level)` finds an optimal solution by BFS.
- `window.__musee` exposes the engine for QA; `?debug=1` overlays cell
  coordinates and state.
- Tests (23 assertions incl. solvability of the 8 levels, ray occlusion,
  determinism, capture rules, decoy semantics, i18n parity, 40k-action fuzz)
  live in the workshop at `games/musee-endormi-dev/` and run against this
  exact `index.html` — they are deliberately kept out of the published
  static package.

## Credits & license

- Concept and specification: Cédric Bernadac.
- Implementation, art, sounds and tests: Z-Code (automated production).
- Consult: Kimi K3.1 Pro (see DELIVERY.md).
- MIT license — see [LICENSE](LICENSE).
