# Go Studio Prototype Review

## What this prototype does

This is a single-file browser Go app (`HTML + CSS + JS`) that provides:

1. **Playable Go board UI** for 9x9 / 13x13 / 19x19 with responsive layout and canvas rendering.
2. **Human vs CPU gameplay** with selectable side, rank-style difficulty presets, komi, pass/resign, undo, hints, score estimate, and record export.
3. **Core rules engine** covering move legality, captures/liberties, suicide prevention, simple ko, passing, and game end after two passes.
4. **Prototype AI opponent** using a heuristic move scorer, candidate pruning (beam), and shallow negamax lookahead that varies by difficulty.
5. **Session UX extras** like system log, move history table, coordinate toggle, and status panels.

## Top 10 most impactful improvements

1. **Move engine computation off the main thread (Web Worker).**
   Prevent UI stalls on 19x19 and deeper search.

2. **Replace hand-tuned search with a stronger pluggable engine path.**
   Add MCTS + policy/value integration interface (or wasm engine bridge) while keeping current heuristic engine as fallback.

3. **Rules completeness: superko variants + dead-stone adjudication flow.**
   Current logic enforces only simple ko; competitive play needs superko options and explicit dead-stone marking.

4. **SGF import/export + replay navigation.**
   JSON export is useful, but SGF unlocks interoperability with analysis tools and sharing.

5. **Proper clock/time controls.**
   Add byo-yomi / Canadian timing, pause/resume, timeout states, and timing metadata in records.

6. **Deterministic testing harness for engine correctness.**
   Add unit/property tests for capture, ko, suicide, pass-end scoring, and regression suites for tactical positions.

7. **Game analysis mode.**
   Post-game graph of eval swings, blunder detection, alternative lines, and "why this move" explanations.

8. **State architecture refactor.**
   Separate pure game state/reducer from rendering and DOM side effects to improve maintainability and testability.

9. **Accessibility and keyboard-first interactions.**
   ARIA labels, focus management, keyboard move cursor, high-contrast mode, and screen-reader-friendly logs/history.

10. **Performance profiling + incremental render strategy.**
    Track frame/move timing and avoid full redraws where possible (dirty regions/layers) for smoother large-board interaction.
