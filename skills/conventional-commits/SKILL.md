---
name: conventional-commits
description: Draft, revise, or review Git commit messages using Conventional Commits 1.0.0. Use when preparing a commit, choosing its type or scope, or checking a message for compliance.
---

# Conventional Commits

Write messages that accurately describe the intended commit, following the local [Conventional Commits 1.0.0](references/conventional-commits-1.0.0.md).

Read its [Specification](references/conventional-commits-1.0.0.md#specification) when checking exact syntax or resolving a compliance question. Consult its [Examples](references/conventional-commits-1.0.0.md#examples) for complete message formats and its [FAQ](references/conventional-commits-1.0.0.md#faq) for mixed changes, versioning, incorrect types, squash workflows, or reverts.

## Establish the change

- For a supplied message or change summary, work from that input. Ask only when missing context affects classification or breaking-change status.
- In a repository, read applicable contribution instructions and commit-message tooling configuration. Recent messages can reveal local style, but do not establish compliance by themselves.
- Use `git status --short` and `git diff --cached` to identify the staged commit. Inspect `git diff` only when unstaged work is relevant to the request; keep staged and unstaged changes distinct. Read affected code when the diff alone does not explain intent.
- If nothing is staged, draft from the working-tree changes only when the user has identified that scope, and state that the draft describes unstaged work. Otherwise clarify the intended scope.
- Read the contents of in-scope untracked files directly; `git diff` does not include them.
- Base the message on observed changes. Include issue numbers, migration instructions, or compatibility claims only when supported by the input or repository.
- For unrelated changes, suggest separate commits and a message for each. Keep coupled implementation, tests, and documentation together when they serve one change.

## Apply the specification

```text
<type>[(<scope>)][!]: <description>

[body]

[footers]
```

Bracketed parts are optional; omit their brackets in actual messages.

- Use a noun type: `feat` for features, `fix` for bug fixes; other types are allowed.
- An optional scope is a parenthesized noun identifying a codebase section. Follow the prefix with a colon, space, and short description.
- Separate an optional free-form body and footer section with blank lines, including when the body is absent.
- Footers use a token plus `: ` or ` #`, then a value. Replace token whitespace with hyphens, except in `BREAKING CHANGE`. Values can span lines until another footer begins.
- Mark breaking changes with `!` immediately before the colon, a `BREAKING CHANGE: <explanation>` footer, or both. With only `!`, explain the break in the description. `BREAKING-CHANGE` is an equivalent footer token.
- Treat structural units as case-insensitive except uppercase breaking-change footer tokens.
- SemVer implications: breaking changes mean major, otherwise `feat` means minor and `fix` means patch. Other types imply no version bump by themselves.

## Choose useful wording

These are defaults, not additional specification requirements. Follow explicit user preferences and compatible repository conventions; flag conflicts with the specification when reviewing compliance.

- Prefer lowercase types and established scopes. Omit the scope when it adds no useful context.
- For other work, common choices include `docs` (documentation), `refactor` (restructuring without changing behavior), `perf` (performance), `test` (tests), `build` (build system or dependencies), `ci` (automation), `style` (formatting), and `chore` (maintenance). This list is open-ended.
- Write a concise, imperative description of the concrete change. Follow the message language requested by the user or required by the repository; otherwise match the supplied message or established commit history.
- Follow configured length limits. Conventional Commits itself mandates no numeric length limit, imperative mood, or punctuation style.
- Add a body when motivation or behavior needs explanation. For a break, describe the compatibility impact and known migration path; a breaking change can use any type.
- For reverts, follow repository tooling. The specification leaves revert semantics undefined; `revert` with references to reverted commits is a useful fallback when the SHAs are known.

## Deliver the result

For drafting or revision, return a ready-to-use message in a code block. Explain assumptions only when they materially affect the result.

For review, distinguish specification violations from repository rules and optional style suggestions. Provide a corrected message when the available facts support one. Check that the type, scope, description, and breaking-change markers match the actual change before finishing.

Drafting or reviewing a message does not authorize staging files, creating commits, amending history, or pushing. Perform Git mutations only within the user's requested scope.

## Examples

Bug fix:

```text
fix(cache): expire entries after their configured lifetime
```

Breaking change with migration guidance:

```text
feat(config)!: require an explicit storage backend

Remove the implicit local backend so deployments choose storage deliberately.

BREAKING CHANGE: set storage.backend to local to retain the previous behavior.
```

Documentation with an issue reference:

```text
docs(cli): explain how to resume interrupted uploads

Refs: #284
```

The reference's source, attribution, and full license are stored in [LICENSE-CC-BY-3.0](references/LICENSE-CC-BY-3.0).
