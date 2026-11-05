# Clean Code Principles

A reusable AI coding skill for code reviews and behavior-preserving refactoring using practical clean code principles.

The skill favors concrete readability and maintenance improvements, small changes, and appropriate verification. It treats function length, arguments, comments, and testing approaches as context-dependent choices.

## Use

Install this repository as a skill named `clean-code` in your coding agent's skills directory. Keep `SKILL.md`, `agents/`, and `references/` together.

Example prompts:

- `Use $clean-code to review this change for readability and maintainability.`
- `Use $clean-code to refactor this function while preserving its public interface and behavior.`
- `Use $clean-code to assess whether these modules need a dependency boundary.`

## Contents

- [SKILL.md](SKILL.md): entry point, working method, and decision rules.
- [Code guidance](references/code.md): names, comments, functions, objects, and classes.
- [Testing guidance](references/testing.md): behavioral confidence, clean tests, and acceptance criteria.
- [Design guidance](references/design.md): duplication, SOLID, components, and concurrency.
- [Architecture and craftsmanship](references/architecture-craft.md): boundaries and disputed tradeoffs.

The references provide self-contained guidance with decision rules and practical tradeoffs.
