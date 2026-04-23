# Hikaru Milestone Reference Plan (MIT-only AI Reuse)

## Project policy (mandatory)
- Only MIT-licensed AI bot code may be copied/adapted into this repository.
- Any third-party AI code added must include source URL, license, and pinned commit/tag in `THIRD_PARTY.md`.
- If a non-MIT engine is ever supported, it must be done through an external adapter process and not by copying code into this repo.

## Milestone 0 — License Gate (MIT-only intake)
**Goal:** Ensure every reused AI codebase is MIT before integration.

### Tasks
- Create/maintain `THIRD_PARTY.md` with: project, repo URL, license, commit/tag, and copied files.
- Create/maintain `LICENSE_POLICY.md` with the MIT-only rule for copied AI code.
- Use a standardized intake checklist for all future bot candidates.

### Exit criteria
- No non-MIT copied AI code in-tree.
- Every imported file is traceable to source + license.
- Team agreement that non-MIT engines may be adapter-supported only.

## Milestone 1 — Engine Abstraction Layer
**Goal:** Decouple current prototype AI from integrated MIT bot code.

### Tasks
- Define an `EngineAdapter` interface (`init`, `genmove`, `analyze`, `setLevel`, `shutdown`).
- Wrap current in-browser AI as `InternalEngineAdapter`.
- Preserve current engine modes and strength ladder behavior through the adapter.

### Exit criteria
- Game runs unchanged with `InternalEngineAdapter`.
- Engine can be swapped by configuration without UI changes.

## Milestone 2 — MIT Bot Code Integration (Direct Adaptation)
**Goal:** Integrate selected MIT bot AI code directly in-repo.

### Tasks
- Import first approved MIT bot under `engine/mit_bot/<name>/`.
- Add normalization layer to map bot outputs to game board model.
- Add deterministic tactical/regression test positions.

### Exit criteria
- MIT bot can play full games via `EngineAdapter`.
- No legality regressions (ko/suicide/capture).
- Strength uplift vs current heuristic baseline on internal suite.

## Milestone 3 — Node.js Runtime Path (Minimal Dependencies)
**Goal:** Support stronger local execution with minimal dependencies.

### Tasks
- Add Node host mode using built-in modules where possible (`child_process`, `readline`, timers).
- Implement process lifecycle, timeout, and crash handling.
- Keep browser-only fallback path for zero-install use.

### Exit criteria
- Dependency footprint remains minimal.
- Engine works in browser-worker mode and optional Node host mode.
- UI remains responsive during engine compute.

## Milestone 4 — SGF & Review Upgrade (AI-aware)
**Goal:** Improve SGF and review UX to expose AI insights.

### Tasks
- Expand SGF handling from mainline-focused parsing toward richer game-tree support.
- Store AI review artifacts per move (point loss, alternatives, confidence).
- Add review actions: “jump to biggest mistake” and “show top alternatives”.

### Exit criteria
- Replay/review supports AI annotations.
- Import/export remains backward compatible with current SGF flow.

## Milestone 5 — Rank Calibration & Difficulty Productization
**Goal:** Convert prototype difficulty into stable, explainable strength tiers.

### Tasks
- Build benchmark harness (fixed seeds/opening sets; 9x9/13x13/19x19).
- Map levels to target outcomes (beginner/intermediate/club).
- Prefer calibrated weakening (policy/value constraints) over randomness-only weakening.

### Exit criteria
- Difficulty labels produce consistent win-rate deltas.
- Rank descriptions align with measured behavior.

## Milestone 6 — Quality Gates + Release Readiness
**Goal:** Ensure maintainability and regression safety.

### Tasks
- Add regression tests for rules engine, SGF parser, and adapter conformance.
- Add performance budget checks (move latency/avg think time).
- Finalize docs: architecture map, adding-a-bot guide, troubleshooting.

### Exit criteria
- One-command test run passes.
- Move generation latency is within agreed budget.
- Documentation is sufficient for future maintenance.

## Suggested timeline
- Week 1: Milestones 0–1
- Week 2: Milestone 2
- Week 3: Milestone 3
- Week 4: Milestone 4
- Week 5: Milestones 5–6 hardening
