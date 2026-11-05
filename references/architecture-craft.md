# Architecture, craftsmanship, and disputed tradeoffs

Source: Robert C. Martin, *Clean Code*, second edition, early-release source edition identified in source.md. Page numbers below are 1-based PDF positions, not printed-book pagination. Recommendations labeled as adaptations turn the source into bounded agent behavior.

## Protect policy from mechanisms

**Chapters 23-25, PDF pp. 490-502.** Evaluate structure by how cheaply required behavior can change. Identify the business policy, then locate decisions about storage, transport, UI, frameworks, and construction that are leaking into it. A useful boundary keeps a concrete mechanism replaceable without rewriting policy.

- Put the abstraction on the policy side: an application-owned persistence contract is implemented by a storage adapter, rather than business rules importing an adapter-owned contract.
- Shape contracts around what the application needs. Avoid exposing an entire vendor API merely because it is available.
- Defer a technical choice when useful work and realistic experiments can proceed without it. A memory implementation can reveal the required persistence contract before committing to storage technology.
- Check the four architectural concerns separately: visible use cases, operational demands, independent development, and deployment. A design that names business capabilities clearly may still fail its throughput or deployment needs.

**Adaptation:** Honor technology choices already required by the task. Preserve a worthwhile seam without pretending every chosen dependency must be replaced. Explain which concrete change or test becomes easier; a hypothetical future vendor swap alone does not justify an extensive abstraction framework.

## Distinguish dependencies from control flow

**Chapter 27, PDF pp. 530-537.** A runtime call can travel outward while source dependencies still point toward policy. For example, a use case calls an output contract it owns; an outer presenter implements that contract. Trace imports, named types, and data formats as well as the apparent call graph.

- Keep reusable business rules distinct from application-specific orchestration when that separation is useful.
- Translate framework requests, database rows, and vendor result objects at the boundary. Pass simple application-shaped data inward, including only the fields the use case needs.
- Keep presentation formatting in the presenter or adapter rather than making policy construct UI-specific strings and controls.
- Treat object creation and binding as construction concerns, separate from ordinary object use.

The book's four-circle diagram is schematic. **Adaptation:** Use the fewest boundaries that solve the actual coupling problem; do not create four mandatory directories or a separate class for each conceptual circle. Verify a proposed boundary by testing policy without the external mechanism where practical.

## Learn an external interface before spreading it

**Chapter 26, PDF pp. 503-519.** When an external API is unfamiliar, write a small learning test for the exact behavior the application needs before debugging that API inside production logic. Retain useful checks as boundary tests for later upgrades. This tests the application's assumptions about the vendor, rather than attempting to re-test the whole vendor product.

If a collaborator's API is undefined, define the interface the application wishes to call, use a fake for local progress, and later bridge to the real API with an adapter. Concentrate framework, concurrency, and wiring details in low-complexity edge code. In the chapter's example, application logic remains independent of the radio framework and process machinery.

**Adaptation:** Add learning tests when there is meaningful uncertainty. Avoid wrappers that merely rename every external method without protecting an application contract.

## Make evidence and change cheap

**Chapters 28-33, PDF pp. 538-579.** Examine both behavior and structural consequences. Dead code, hidden global state, and coupling can obscure what a program actually does. For a production incident, the book allows an expedient fix; it also argues for cleaning up the resulting structural debt.

Prefer small, reviewable increments with fast, repeatable checks. The book's “proof” is empirical testing, not a mathematical guarantee (pp. 558-559). Coverage shows executed code, not necessarily verified behavior; use it to find gaps rather than as a naive management target. Mutation testing can expose ineffective assertions when the added runtime is worthwhile (pp. 571-573).

**Adaptation:** Preserve the authorized task's scope. Report concrete residual uncertainty and important follow-up work. Do not silently commit, revert, push, deploy, change team policy, or initiate a broad cleanup because the book recommends short cycles. Use existing checks proportionately; keep readiness to release separate from authorization to release.

**Chapters 34-37, PDF pp. 580-592.** Make handoffs understandable and avoid concentrating knowledge in one person. If asked to estimate substantial work, communicate assumptions and a range matching uncertainty; distinguish an estimate from a commitment. Review colleagues' work respectfully and describe code effects rather than personal failings.

## Preserve the appendix's disagreement

**Appendix, PDF pp. 597-646; key summaries pp. 611-612, 623-624, 644-646.** Martin and John Ousterhout disagree about how small methods should be, the value of comments, and whether TDD sufficiently encourages design. Their shared goals do not settle those choices universally.

- Stop extracting when readers must reconstruct a call graph and carry shared state or ordering assumptions across several helpers. Compare the cognitive load of both versions; method length alone is insufficient evidence.
- Preserve comments that explain a nonobvious contract, invariant, algorithmic fact, or rationale. Verify their accuracy; neither removing comments nor adding many comments guarantees clarity.
- Treat TDD and small design/code/test bundles as alternative disciplines. Deliberate design and continuous refactoring remain necessary with either. Passing the next test does not establish that the overall design is appropriate.

When invoking these ideas in review, identify the observed maintenance cost, explain the proposed tradeoff, and present disputed preferences as preferences.
