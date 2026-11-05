# Design and concurrency decisions

Treat principles as tools for explaining a concrete maintenance cost and choosing a proportionate change.

## Prefer simple designs with explicit tradeoffs

Simple means untangled: protect high-level policy from details such as storage, transport, or presentation. Prioritize behavioral confidence, expression of intent, removal of real duplication, and then reduction in size. Reducing line count must not defeat the earlier goals.

- Before adding a future extension hook, ask what happens if it is never needed. Compare its ongoing maintenance burden with the cost of introducing it later. YAGNI does not prohibit thinking ahead or justify ignoring an expensive irreversible choice.
- Consolidate repeated knowledge when the copies express the same intent and should change together. Keep accidental duplication separate when similar code serves different actors or will evolve for different reasons.
- Use tests to expose usage and support refactoring. Improve confidence where the change needs it, without introducing a universal coverage percentage requirement or claiming coverage proves correctness.

## Diagnose change propagation with SOLID

**SRP:** Ask which stakeholder group requests a change. Group behavior that changes for the same actor and separate behavior with divergent owners. This is distinct from the function-level "one thing" heuristic: a module may contain many related operations. Avoid a shared helper that silently couples policies owned by different actors.

**OCP:** For an actual extension, identify the stable policy and the changing detail. Structure the dependency so a new detail can be added without repeatedly editing protected policy. Closure is strategic; specify the kind of change being insulated instead of adding speculative extension points everywhere.

**LSP:** Verify that interchangeable implementations honor the client-visible contract, including services and dynamically typed interfaces. A caller that needs implementation-specific exceptions signals a broken abstraction; fixing it at the boundary may prevent those exceptions from spreading.

**ISP:** Give a consumer the operations and dependencies it actually needs. Consider deployment and transitive dependency baggage as well as method count.

**DIP:** Keep policy dependent on stable abstractions rather than volatile implementations. Source-code dependency direction can oppose runtime control flow. Stable platform facilities can remain concrete dependencies; wrapping every dependency creates unnecessary interfaces. Introduce boundaries as a demonstrated change or testing need warrants them, gathering concrete wiring into an appropriate composition location.

## Shape components around change and reuse

Treat a component as a deployment/release unit, not automatically a service. Balance three cohesion pressures: release together what users reuse together (REP), group elements that change for the same reasons and at the same times (CCP), and avoid forcing consumers to carry unrelated elements (CRP). Early development may favor localized changes over broad reuse; revisit the grouping as actual reuse grows.

When component cycles force coordinated builds or changes, invert a dependency through a suitable interface or extract a genuinely shared concern. Favor dependencies toward components that are harder to change, and give those stable policy components suitable extension abstractions. Distinguish positional stability from simply not having changed recently. Use coupling and abstraction metrics when they clarify a concrete design problem; routine calculation is unnecessary when the relationships are already clear.

## Reconsider design with each behavior

Use clarity, conciseness, confirmability, and cohesion as competing questions: Can a teammate find and understand the behavior? Is there unnecessary expression or repeated knowledge? Can the intended result be verified? Do the module's elements belong together? Extract and move an obscured concept when doing so helps these answers. Keep familiar idioms when they remain readable. Continuous design includes planning and estimating; it does not require either exhaustive advance models or design-free coding.

## Treat concurrency as a separate design concern

First identify the shared mutable state or resource and the invariant at risk. Reduce sharing through independent partitions, copies, or immutable data before multiplying locks. Keep coordination apart from ordinary business logic. Thread-safe individual methods do not make a multi-call transaction atomic; protect the complete invariant while keeping unrelated work outside the critical section. Plan startup, shutdown, cancellation, and waiting relationships early.

Verify ordinary logic separately, then exercise concurrency with varied interleavings, load, and supported configurations. Investigate intermittent failures even if a rerun passes. Consider domain changes that serialize a hazardous operation, explicit ownership, or accepting a recoverable conflict when the domain permits it. State the chosen consistency and recovery contract; do not assume a framework removes shared-state problems.
