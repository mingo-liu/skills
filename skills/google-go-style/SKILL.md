---
name: google-go-style
description: Write, refactor, and review Go code using Google's Go Style Guide, Style Decisions, and Best Practices. Use for Go implementation and readability questions, or when Google Go style is requested.
---

# Google Go Style

Write, refactor, and review Go code using Google's Go Style Guide, Style
Decisions, and Best Practices. Prioritize clarity and simplicity, apply the
guidance in context, and keep changes focused on the user's task.

## Read the relevant source

Before applying this skill, read the [overview](references/index.md) and the
[core style guide](references/guide.md). The overview explains the documents'
authority and scope; the guide establishes the principles and core guidelines.
Read them once per working context, then consult the relevant sections below.

| Work being performed | Required reference sections |
| --- | --- |
| Names, packages, receivers, constants, initialisms, getters, variables | [Decisions: Naming](references/decisions.md#naming); [Best Practices: Naming](references/best-practices.md#naming) for naming tradeoffs |
| Comments, documentation, examples, named results | [Decisions: Commentary](references/decisions.md#commentary); [Best Practices: Documentation](references/best-practices.md#documentation) |
| Imports, aliases, grouping, blank or dot imports | [Decisions: Imports](references/decisions.md#imports); [Best Practices: Imports](references/best-practices.md#imports) |
| Errors, wrapping, logging, initialization, panics | [Decisions: Errors](references/decisions.md#errors); [Best Practices: Error handling](references/best-practices.md#error-handling); the panic and must-function sections under [Decisions: Language](references/decisions.md#language) |
| Literals, slices, control flow, copying, goroutines, generics, receivers, other language constructs | [Decisions: Language](references/decisions.md#language) |
| Flags, logging, contexts, randomness | The relevant heading under “Common libraries” in [Decisions](references/decisions.md); [Contexts](references/decisions.md#contexts) when applicable |
| Tests, assertions, failures, comparisons, subtests, tables, helpers, test packages | [Decisions: Useful test failures](references/decisions.md#useful-test-failures), [Test structure](references/decisions.md#test-structure), and [Best Practices: Tests](references/best-practices.md#tests) |
| Package boundaries, global state, interfaces, variables, function arguments, CLI design, string construction | The matching heading in [Best Practices](references/best-practices.md), plus the corresponding [Decisions](references/decisions.md) section if present |

The bundled documents preserve the complete guide content, adapted for local
Markdown reading.
For a full Google Go style audit, read all four documents. For a focused change,
read the applicable sections, including exceptions and linked explanations,
before deciding how a rule applies. Search the larger files by heading or term:

```sh
rg -n '^#{1,4} |<a id=' references/decisions.md references/best-practices.md
rg -n -i 'receiver|initialism|context|goroutine|panic|table-driven' references/
```

Run these commands from the skill directory, or use absolute paths to it.

## Apply the guidance

- Resolve tradeoffs in the guide's priority order: clarity, simplicity,
  concision, maintainability, then consistency.
- Treat the core guide as normative and canonical. Style Decisions is
  normative, not canonical, and subordinate to the guide. Best Practices is
  advisory; evaluate its alternatives in context instead of presenting every
  recommendation as a requirement.
- Preserve the force and scope of each statement: “must,” “should,” and
  “may” differ. Read exceptions before reporting a violation. Distinguish
  Google's internal conventions and library examples from dependencies actually
  available in the target repository.
- Inspect the requested code, nearby conventions, repository instructions, and
  supported Go version. Respect explicit user and repository requirements;
  explain a material conflict with Google style instead of silently replacing
  those requirements. Local consistency alone does not override the guide.
- Keep changes within the task. Avoid unrelated style churn; the overview does
  not justify mass rewrites. When fixing nearby deviations, avoid spreading an
  existing deviation or exposing it in additional APIs.
- Format changed Go code with `gofmt` (or the repository's equivalent workflow).
  Go source has no fixed line-length limit. Run relevant repository checks and
  tests when implementation behavior changes; formatting alone does not prove
  correctness.
- In reviews, identify the concrete location and readability impact, cite the
  relevant bundled section or official URL, and separate requirements from
  optional improvements. Do not invent a rule when the documents are silent.

## Sources and licensing

References come from [Google Go Style](https://google.github.io/styleguide/go/)
by Google and the [google/styleguide contributors](https://github.com/google/styleguide).
See [LICENSE](references/LICENSE) for terms. Consult official sources when
current guidance is requested.
