---
name: code-review
description: Review code changes against requirements and project standards for correctness, compatibility, security, and maintainability. Use for pull requests, revision ranges, or working-tree reviews with actionable findings.
---

# Code Review

Review how a change affects promised behavior, existing users, and the cost of
future changes. Deliver findings that the author can evaluate and act on within
the requested scope.

## Read the guidance

Read the [Code Review Guide](references/code-review-guide.md) before reviewing,
once per working context. Use its risk areas to select checks relevant to the
change. Consult [Follow-up reviews](references/code-review-guide.md#follow-up-reviews)
when reviewing revisions or responding to an author's explanation.

## Establish the scope

- Resolve and record the requested revisions or local inputs and files.
  Distinguish a branch's merge-base diff from an exact revision comparison, and
  staged, unstaged, and untracked work. Confirm the comparison is valid; resolve
  ambiguity from repository context before asking the user.
- Compare in-scope acceptance criteria with the implemented behavior, including
  missing or partial work. Read applicable repository instructions and adopted
  standards, preserving their scope, exceptions, and requirement strength.
  Record consequential assumptions when requirements are unavailable.

## Examine the change

- Build a change map: entry points, affected consumers, state transitions, and
  boundaries crossed. Trace the important paths through implementations and
  tests, then cover the remaining changes within scope. Identify unread or
  truncated material before claiming coverage.
- Read callers, guards, configuration, and data contracts where they determine
  whether a concern is real. Compare prior behavior to distinguish new risks
  from existing problems. Preserve source files, the index, and HEAD during
  inspection; use a disposable working copy for experiments that would change
  them. Keep unrelated cleanup separate.
- Evaluate candidates using the guide's [Evidence standard](references/code-review-guide.md#evidence-standard).
  Run focused checks when they resolve a material uncertainty; identify which
  conclusions come from execution and which come from code inspection. For UI
  changes, verify affected interactions when static evidence is insufficient.

## Deliver the review

- Follow the guide's [Reporting](references/code-review-guide.md#reporting)
  conventions. Group duplicate symptoms by root cause and present required
  changes before suggestions. Apply the guide's
  [Impact and review action](references/code-review-guide.md#impact-and-review-action)
  criteria; keep evidence strength separate from impact.
- State the reviewed scope, verification performed, and material limitations.
  An empty findings list is a valid result; explain what was assessed without
  claiming the absence of all defects. Distinguish readiness within the reviewed
  scope from an assessment limited by missing evidence.
- Return the review to the user. Apply fixes or publish comments when the
  request includes those actions.
