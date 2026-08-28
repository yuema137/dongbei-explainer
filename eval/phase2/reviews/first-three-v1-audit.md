# Audit: first three phase-2 full variants

Status: failed calibration sample. The outputs were technically sound but the full skill did not create enough explanatory gain over baseline.

## Human annotation result

In all three cases A was baseline and B was full. The product owner chose “B slightly better” three times, not “B clearly better”. The comments identified:

- PR #248: B improved comprehension, but `composition authority`, `typed composition projection`, `Regime-A`, and `CAP-SCOPE` remained unexplained; long project-local English labels may need a Chinese responsibility description rather than unconditional preservation. Dongbei voice was not perceptible.
- PR #232: B was clear, but still felt cold, rigid, and conventionally technical, with no meaningful Dongbei presence.
- PR #219: B failed to explain `sidecar`, and the voice remained too light.

These annotations confirm insufficient distance from the baseline: internal terminology still set the entry cost, and the requested conversational register was too weak to notice.

## Root evaluation error: wrong audience

The v1 bundle described the first three readers as senior software/ML systems engineers familiar with runtime concepts. That is not the product audience. The default reader has a general STEM background and may have no CS training. This bad condition directly encouraged the outputs to skip `sidecar`, `watchdog`, `composition projection`, authority boundaries, and other software-internal concepts. V1 remains frozen as a failed calibration round; its remaining six cases should not be annotated.

## Shared failure

All three answers inherited the PR author's abstraction boundary. They reordered clauses and added conversational markers, but still expected the reader to understand project-local nouns before seeing a concrete mechanism. The result sounded less formal without becoming much easier to picture.

This is not fixed by increasing dialect density. It requires conversational reconstruction: start with a small situation, identify actors and changed actions, map any analogy to real components, then restore formal names and boundaries.

## PR #248

The v1 full answer opened with `composed task`, TIDMAD semantics, `typed composition projection`, and task-owned blocks. These are the things needing explanation. A better entry is a shared workflow whose new task label has changed while several stations still read TIDMAD's old instruction card. Then map the stations to scope, health, run identity, and prompts. The resume fingerprint consequence should be traced with an old workspace, not merely named.

## PR #232

The v1 answer did include a data trace, but its main claim—why a third task proves genericity—remained abstract. The reader needs the falsifiable before/after: if the core had a DAVIS branch or imported `examples/`, this would be another bespoke pipeline; instead the same interfaces consume a different manifest, tensor shape, deliverable, and metric. The global-MSE numerical counterexample is strong and should stay.

## PR #219

The v1 answer was closest to the target, but `sidecar`, prediction persistence, and watchdog timing appeared before a concrete timeline. The useful trace is: at 56.8 s the old deadline becomes 85.1 s; validation starts; its estimate is calculated locally but not written where the watchdog reads; the process dies at 86.1 s. A short “预算算出来但没贴到值班表” analogy maps cleanly to local state versus persisted sidecar.

## Skill changes

- Voice is now a reconstruction pass, not a lexical surface pass.
- Project-local nouns no longer inherit Tier-1 status from the reader's seniority.
- Dense PR/issue explanations default to one worked trace.
- Structural analogies are encouraged when internal artifacts are themselves unfamiliar, but must be mapped and terminated quickly.
