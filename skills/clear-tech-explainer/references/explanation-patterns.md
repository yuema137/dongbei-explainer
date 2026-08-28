# Explanation patterns

Use the smallest pattern that exposes the mechanism.

## Replacement or indirection

Show `before -> pressure -> changed step -> after`. Name who used to call whom, what is now inserted, and what can vary independently. Dependency inversion and API abstraction fit here.

## State or lifecycle

Trace one object through creation, transitions, and destruction. Process/thread, image/container, and async tasks fit here.

## Resource bottleneck

Separate capacity from activity and locate the waiting stage. GPU memory/utilization and caches fit here.

## Statistical claim

State the hypothetical or sampling process, what the number is conditioned on, and what conclusion it does not permit. Keep the formal definition available.

## Depth preservation

At levels 3–4, conversational framing is an entrance, not a substitute. Show the commit graph, scheduling queue, tensor shapes, likelihood, or equation that carries the distinction.
