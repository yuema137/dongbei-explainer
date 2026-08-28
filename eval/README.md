# Calibration

`cases.yaml` contains 16 single-turn concepts across software, systems, ML, and statistics. `multi-turn.yaml` adds six conversations (27% of the 22 case artifacts; 37.5% relative to single-turn cases) to test first-use terminology memory and depth shifts.

The suite is behavioral, not string-matched. For each answer:

1. Check every `must`, `misconceptions`, and `preserve` item.
2. Apply `rubric.md` with short evidence notes.
3. Compare variants in `samples/comparisons.md`.
4. Run `scripts/lint_text` on generated samples as a warning-only dialect check.

Cross-host runs should use the same canonical skill bytes and input. Codex and Claude Code need not produce identical wording. This repository does not claim live cross-host model results until those runs are actually performed.

Human boundary exports normalized by `scripts/import_annotations` live under `annotations/`. They are versioned calibration inputs; generated skill references must stay traceable to the dataset version.
