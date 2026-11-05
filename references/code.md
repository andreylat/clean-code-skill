# Code, interfaces, and refactoring

## Clean in small, behavior-preserving steps

First establish the behavior that must remain stable. Alternate getting a small behavior working with improving its structure. Change one understandable element at a time, then run relevant checks. If a step breaks behavior, diagnose or undo that step before adding more transformations. Preserve unrelated user work when undoing changes.

Use local cleanup to reduce the next reader's effort. A better predicate name or isolated policy can be sufficient. Added structure also adds indirection and cognitive cost; stop when the next proposed abstraction lacks a concrete readability or change-isolation benefit.

## Names form a shared vocabulary

- Choose names that explain purpose, units, and meaningful distinctions. Similar concepts should use consistent terminology; different names should communicate real differences.
- Use domain terms for business concepts and established technical terms for implementation concepts. An invented business metaphor can obscure a familiar algorithm.
- Put related values in a meaningful enclosing concept when that removes ambiguity. Avoid repeating application or container context in every identifier.
- Balance scope and familiarity. Short local names can be clear inside a tiny, conventional scope. Widely visible variables need more context. Convenient short names can suit general public functions, while narrowly scoped private helpers may need longer descriptions. Treat this as a heuristic, not a renaming mandate.
- Follow the language and team's established accessor, interface, and keyword-argument conventions.

## Keep comments that convey otherwise missing information

Before explaining mechanics in prose, see whether a name, predicate, or small abstraction can express the same concept. Keep useful rationale, consequences, constraints from unchangeable APIs, required legal notices, and meaningful public API documentation. Check these statements against actual behavior; an explanatory comment can expose a defect rather than excuse it.

Update comments with the code they describe. Remove obsolete history, redundant narration, and abandoned commented-out implementations when within scope; version control already retains history. Before checking in, resolve temporary TODOs by completing the work, eliminating the need, or tracking the unresolved requirement in the backlog. Honor the repository's issue-tracking convention and authorized scope; do not silently discard unresolved requirements.

## Extract concepts, then reassess their home

Aim for a function whose name summarizes a coherent task and whose body works at a consistent abstraction level. Arrange the public operation and supporting helpers so readers can understand the policy before inspecting its details, subject to language declaration rules.

A meaningful extraction adds a name more abstract than its implementation. Extracting a whole body behind a second identical delegator, or naming each obvious assignment, usually adds no concept. Stop or strategically inline when helpers are entangled and require joint reading without reducing mental load. Do not enforce a universal line limit. Extraction can still be useful temporarily to reveal misplaced behavior before moving it to the appropriate module.

## Make coupling and side effects visible

Treat positional arguments as coupling and opportunities for ordering mistakes. Group genuinely cohesive inputs or use named arguments; fewer parameters alone do not justify unrelated bundles or hidden dependencies. Boolean mode arguments often conceal different operations, but a genuine boolean setting need not become two methods. Prefer clear return values over surprising output parameters where idiomatic.

Purity concerns observable behavior: internal local mutation can remain externally pure. Do not move arguments into shared mutable fields merely to shorten a signature; consider reentrancy, object lifetime, and concurrent calls. Encapsulate paired resource acquisition and release without hiding externally observable changes.

Command/query separation helps clarify intent, but combined operations such as removal-with-return may be appropriate. Preserve required atomicity and exception guarantees. Use exceptions where suitable and consistent error returns in languages such as Go. Follow the language's error model and keep recovery separate from normal processing when that improves clarity.

## Merge duplication that changes together

Distinguish shared knowledge from coincidental similarity. Similar code serving different actors may need to evolve independently; merging it can couple unrelated policies. Code that must change together is a stronger extraction candidate, especially as its size or repetition grows. Tiny repeated initialization is not automatically worth an abstraction. Repeated traversal with varying behavior can use an idiomatic callback or strategy when that centralizes one structural responsibility.

## Choose objects or data by the expected direction of change

Objects hide representation behind behavior; DTOs deliberately expose data. Getters and setters do not by themselves create an abstraction. Prefer object dispatch when new variants should be added without changing existing operations. Prefer data plus procedures when a stable set of variants needs many new operations. A switch is therefore not intrinsically wrong.

Apply Demeter to leaking object internals, not to the number of dots. Traversing an intentional DTO is different from navigating an object's private collaborators. For the latter, ask what operation the caller actually needs and place it with the object that owns the knowledge. Avoid hybrids that expose representation while also pretending to encapsulate behavior.

## Separate policy from implementation when change warrants it

Assess class cohesion through concrete reasons to change, including policies hidden inside method bodies. Extract a complex predicate to name it, then inspect which object's data it principally uses; move behavior when this reveals feature envy. Keep orchestration readable by delegating implementation specifics.

Wait for an actual change to justify a new strategy or boundary rather than speculating about every possible variation. Small classes are useful when they isolate concepts; their count is not a quality score. Test reusable behavioral policies through their contracts and keep incidental private helpers private.
