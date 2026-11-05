# clean-code-skill

A reusable AI coding skill for code reviews and behavior-preserving refactoring, based on Robert C. Martin's *Clean Code*, second edition, early release.

The skill favors concrete readability and maintenance improvements, small changes, and appropriate verification. It preserves the book's tradeoffs instead of enforcing universal limits on function length, arguments, or test coverage.

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
- [Source details](references/source.md): edition identity and PDF page references.

The references contain operational paraphrases. The source book PDF is not included or required to use the skill.
