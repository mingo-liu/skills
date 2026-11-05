---
name: uber-go-style
description: Write, refactor, and review Go code using the complete Uber Go Style Guide. Use for Go implementation and style decisions, or when the user requests Uber Go conventions or a compliance review.
---

# Uber Go Style

Apply the bundled [complete guide](references/uber-go-style-guide.md)
when writing, refactoring, explaining, or reviewing Go code. It includes every
section, explanation, and code example from the upstream guide without edits.
The bundled text is the source of truth for what this skill attributes to Uber.

## Read the relevant guidance

Start with the guide's table of contents and Introduction. For a focused task,
read the complete sections that apply, including their examples, exceptions,
and linked sections within the guide. Use the following entry points:

- [Guidelines](references/uber-go-style-guide.md#guidelines): interfaces,
  receivers, mutexes, ownership of slices and maps, cleanup, channels, enums,
  time, errors, panics, atomics, globals, embedding, initialization, process
  exit, struct tags, and goroutine lifetimes.
- [Performance](references/uber-go-style-guide.md#performance): conversions
  and container capacity.
- [Style](references/uber-go-style-guide.md#style): consistency, declarations,
  naming, imports, function ordering, control flow, scope, slices, strings,
  struct and map initialization, and printf conventions.
- [Patterns](references/uber-go-style-guide.md#patterns): table tests,
  parallel tests, and functional options.
- [Linting](references/uber-go-style-guide.md#linting): recommended checks
  and lint runners.

For a comprehensive compliance review, read the entire guide in manageable
chunks and account for every applicable section within the requested scope.
Search can locate a rule, but read its surrounding guidance before applying it.

## Apply the guide

Preserve the guide's distinction between requirements, recommendations, and
context-dependent choices. Apply its rationale and exceptions rather than
treating every example as a universal rule. Respect explicit user instructions
and repository requirements; identify material conflicts when they affect the
result. Keep changes within the requested scope.

For implementation or refactoring, inspect the surrounding code and project Go
version, then apply the relevant rules while preserving intended behavior.
Use the project's established formatting, test, and lint commands to verify
the change as appropriate. The guide's tool references are a snapshot; use
project-compatible tools and configuration instead of assuming an old command
or configuration is still supported.

For reviews, give each finding a code location, the relevant guide section,
its practical effect, and a concrete correction. Distinguish correctness
problems from style preferences. Report only supported findings and state
the scope actually inspected.

For explanations, link the relevant local section and distinguish the guide's
recommendation from additional advice. The guide is bundled for offline use;
external links provide further reading. Fetch newer material only when the
task requires current information or an update.

## Source

The [bundled guide](references/uber-go-style-guide.md) is a complete, unmodified
copy of the [Uber Go Style Guide](https://github.com/uber-go/guide/blob/master/style.md),
with original attribution and the [Apache 2.0 license](references/LICENSE) retained.

When updating, replace the full guide, preserve attribution and license, and
update the source link. Keep skill-specific instructions in this file.
