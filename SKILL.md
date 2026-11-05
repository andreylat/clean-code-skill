---
name: clean-code
description: Review and refactor code using practical clean code principles. Use when asked for readability improvements, behavior-preserving refactoring, or analysis of responsibilities and dependency boundaries in existing code.
---

# Clean Code Principles

Improve the reader's ability to understand, verify, and change code. Apply context-aware principles for readability, cohesion, testability, and dependency management. Judge a change by the confusion or coupling it removes, rather than conformity to a slogan.

## Choose the relevant guidance

Read only the references needed for the task:

- Names, comments, formatting, functions, side effects, objects, and classes: [references/code.md](references/code.md).
- Regression protection, test clarity, acceptance criteria, and reviewing generated code: [references/testing.md](references/testing.md).
- Duplication, SOLID, component dependencies, continuous design, and concurrency: [references/design.md](references/design.md).
- Architectural boundaries, policy versus details, craftsmanship, and design tradeoffs: [references/architecture-craft.md](references/architecture-craft.md).

The references provide self-contained guidance for each topic.

## Working method

1. Establish whether the user wants a review, edits, or an explanation. Follow the requested scope, repository conventions, and language idioms. A request for review alone does not authorize rewriting the code.
2. Understand the behavior before proposing structural changes. Inspect callers and relevant tests; identify contracts, state changes, error handling, ordering, external effects, and any stated performance constraints.
3. Identify a specific maintenance obstacle: misleading naming, an unexpected effect, mixed abstraction levels, unrelated reasons to change, or policy coupled to a volatile detail. Explain its consequence in this code.
4. Choose the smallest useful improvement. Prefer a local rename, a cohesive extraction, an explicit dependency, or a clearer contract when it resolves the obstacle. Introduce an interface or architectural boundary when an actual change pressure justifies it.
5. For edits, preserve observable behavior unless the user requested a behavior change. Make one coherent transformation at a time and run checks appropriate to its risk. Before a substantial refactor with inadequate regression protection, add a focused characterization test or identify a reliable equivalent check. Do not add tests that merely repeat the implementation or test a trivial cosmetic change.
6. Re-read the result from the caller's perspective. Stop when the requested change is complete, verification supports it, and the code is easier to follow. Avoid polishing unrelated code or increasing navigation merely to make functions shorter.

## Decision rules

- **Intent before mechanics.** Names and contracts should reveal domain meaning, relevant units, and surprising effects. Rename only when the replacement conveys information the reader needs.
- **One coherent abstraction at a time.** A function can orchestrate several steps of one use case. Extract a step when a useful name hides detail at the next level; check whether the resulting call chain is actually easier to read.
- **Keep effects visible.** Distinguish queries from commands where the design permits it. Preserve evaluation order, mutation, resource cleanup, and exception behavior during extraction.
- **Group by reasons to change.** Locate behavior with the state and policies it belongs to. Similar text is insufficient evidence of one responsibility or one reusable abstraction.
- **Reduce genuine duplication.** Share code that represents the same policy and should evolve together. Keep similar code separate when different actors or rules will change it independently.
- **Protect policy from details.** Where a boundary is warranted, let volatile implementation code depend on the policy's contract. A class, callback, function argument, or module can supply the needed separation; use the form that fits the language and application.

## Apply judgment

Small functions, few arguments, TDD, and extensive test coverage can support maintainability. Assess these approaches in context. Do not turn line counts, argument counts, assertion counts, or coverage percentages into automatic rejection rules.

Preserve comments that explain rationale, constraints, protocol requirements, or non-obvious algorithms. Prefer clearer code over comments that narrate it; do not remove useful knowledge just because it appears in a comment.

Do not add speculative layers or patterns to satisfy a principle. Distinguish accidental duplication from shared policy, and weigh the tradeoffs of method length, comments, and testing disciplines. Surface material tradeoffs when recommending an approach.

Craftsmanship guidance does not authorize commits, reverts, deployments, external messages, or process changes. Keep those actions within the user's actual request.

## Report the result

For a review, use the user's requested format. Give actionable findings with a precise location, the problem, its concrete consequence, and a minimal correction. Separate optional preferences from defects; do not manufacture findings to fill a quota.

For edits, state the behavior preserved or intentionally changed, the main structural improvement, and the verification performed. State any verification gap plainly.

For an explanation, connect the principle to the actual code, show the tradeoff, and prioritize the engineering reason.
