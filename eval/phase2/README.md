# Phase 2: explanation comparison

Phase 1 calibrates vocabulary boundaries. Phase 2 compares complete explanations on approximately ten real PR/issue cases supplied by the product owner.

Open [`index.html`](index.html) directly in a browser. Import a prepared case bundle, review one card at a time, and export the completed annotations. No server or dependency is required.

## Evaluation contract

Each case freezes the relevant PR/issue input instead of depending only on a mutable URL. Two outputs are generated from the same model family, source snapshot, audience, depth, and user question:

- baseline: no dongbei-explainer project skill;
- full: canonical `dongbei-explainer` composition.

The UI randomizes which output is A or B per case and hides the identity by default. Annotation records the assignment so results can be decoded later. Wording equality is irrelevant.

The reviewer records:

- overall preference on a five-point A/B scale;
- whether A or B lost or distorted technical information;
- whether either answer overdid conversational/Dongbei style;
- whether either answer overexplained jargon;
- a free-form product comment.

## Case bundle

Import a JSON file matching [`case-bundle.schema.json`](case-bundle.schema.json). Keep the initial round at about ten cases. A case is not ready until both outputs and their generation provenance are present.

The source snapshot should contain only material necessary to explain the case. Do not include secrets, private credentials, personal data, or repository content that should not enter this project.

## Output

The browser stores progress in `localStorage`. Exported JSON contains the bundle ID, per-case A/B assignment, ratings, flags, comments, and timestamps. Later tooling should join results by stable case ID rather than display order.
