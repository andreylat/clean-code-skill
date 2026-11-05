# Testing and behavioral confidence

## Choose a feedback discipline

Choose a feedback discipline suited to the work: TDD, TCR, or small bundles of code and tests. TDD alternates a minimally failing test with the production change needed to pass it. TCR automatically commits success and reverts failure. Small bundles allow either writing order but end a short increment with passing tests covering the intended behavior. Each approach aims to maintain a recent, trustworthy working state that makes structural changes less intimidating. Testing discipline supports higher-level design but does not replace it.

Use the repository's testing discipline and the task's risk to choose a short feedback loop. Do not impose TDD, install a file watcher, commit, or revert merely because this skill was invoked. For a risky refactor, identify missing behavioral protection before changing structure. A passing suite provides evidence within its coverage, not proof of correctness.

When logic is difficult to test because it touches time, an operating system, a framework, or presentation hardware, move decisions into testable code and keep the boundary mechanism thin. Use controlled dependencies where useful. Record practical and subjective verification limits rather than reporting untested behavior as verified.

## Make a test explain one action

- Make Arrange, Act, and Assert easy to distinguish. Keep the behavior under examination visible instead of burying it in object construction, request plumbing, or conversion details.
- Extract test helpers and composed assertions when recurring setup or checking obscures the domain. Let a small testing vocabulary emerge from actual tests rather than designing a framework in advance.
- Focus a test on **one action under test**. Several assertions may describe the result of that action. Avoid chaining actions so a later assertion depends on an earlier operation succeeding.
- Check F.I.R.S.T.: fast, isolated, repeatable, self-validating, and timely. Tests should not require another test to run first or a person to inspect logs to determine success.
- Treat broad test churn after a localized production change as evidence of test coupling. Hide incidental construction and interface plumbing behind appropriate test helpers; keep meaningful behavioral expectations explicit.

Test code deserves the same care for clarity and design as production code. It may reasonably spend more memory or CPU for readability when its own execution environment permits it.

## Specify acceptance in shared terms

For a feature with ambiguous success criteria, translate examples into input state, action, and expected result, using Given-When-Then or another format stakeholders understand. Include happy paths and meaningful failure cases. Keep automation visibly faithful to those examples. Develop acceptance criteria with business and QA participants where available, using language they can review. Choose a tool that supports that collaboration.

Derive criteria from the user's actual requirements and surface consequential ambiguity. Do not invent stakeholder approval or equate an incomplete passing suite with permission to deploy. Preserve already accepted behavior with appropriate regression checks.

## Verify generated code against intent

Generated code can misinterpret ambiguous definitions or change existing behavior during regeneration. Specify domain terms and edge cases, retain executable examples, inspect the actual diff, and run checks against requirements. Do not treat a plausible generated implementation or a generated test as an independent correctness oracle. Evaluate tests against independently stated requirements as well as checking whether they pass.
