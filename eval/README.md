# Calibration

`cases.yaml` contains 16 single-turn concepts across software, systems, ML, and statistics. `multi-turn.yaml` adds six conversations (27% of the 22 case artifacts; 37.5% relative to single-turn cases) to test first-use terminology memory and depth shifts.

`invocation-cases.yaml` checks semantic trigger coverage and false-positive boundaries. It includes plain requests for clarity, depth, lower prose burden, confusion repair, comparison, and causality, plus artifact-only and explicit-tone requests that must not receive Dongbei voice.

The suite is behavioral, not string-matched. For each answer:

1. Check every `must`, `misconceptions`, and `preserve` item.
2. Apply `rubric.md` with short evidence notes.
3. Compare variants in `samples/comparisons.md`.
4. Run `scripts/lint_text` on generated samples as a warning-only dialect check.

## Two calibration phases

- Phase 1 labels expression accessibility and English-term familiarity. Its normalized exports live in `annotations/`.
- [Phase 2](phase2/README.md) compares baseline and full-skill explanations for up to ten real PR/issue cases. Its local HTML UI supports blinded A/B assignment, structured flags, comments, saved progress, and JSON export.

Cross-host runs should use the same canonical skill bytes and input. Codex and Claude Code need not produce identical wording. This repository does not claim live cross-host model results until those runs are actually performed.

Human boundary exports normalized by `scripts/import_annotations` live under `annotations/`. They are versioned calibration inputs; generated skill references must stay traceable to the dataset version.
