# Code Review Guide

## Review decisions

A review helps decide whether a change is ready for its intended use and what
must be addressed first. Evaluate behavior, risk, and future maintenance. Let
the consequences of the change determine the attention each part receives.

Separate three kinds of feedback:

- **Required change:** a demonstrated defect, an unmet acceptance criterion,
  an applicable mandatory rule, or a material design problem with a concrete
  consequence.
- **Suggestion:** an improvement whose benefit is plausible but whose absence
  does not establish that this change should wait.
- **Question:** missing information that could change the assessment. State the
  assumption and explain why the answer matters.

A design problem can justify a required change through a concrete maintenance
burden or a misleading contract, even before a runtime defect appears. For a
mandatory-rule finding, cite the supporting provision and its location, and
show why it applies to this file or behavior. Preserve its exceptions and
distinguish requirements from advice.

## Impact and review action

Use the project's severity scheme when available. Otherwise, use these impact
anchors and explain the affected users and conditions:

| Impact | Typical consequence |
| --- | --- |
| High | Unauthorized access, permanent data loss, or a broken primary workflow under reachable conditions. |
| Medium | A bounded feature or compatibility failure, or a substantial maintenance burden with a concrete affected task. |
| Low | A localized, limited consequence or small improvement without broad disruption. |

Consider exposure, frequency, recovery, and rollout context when ordering
findings. Required versus suggested describes the action needed; it is separate
from impact. A mandatory local rule can require a low-impact correction, while
a speculative severe outcome remains a question until its preconditions are
established. Optional polish alone should not prevent a favorable assessment.

## Understand the change

Record resolved base/head revisions and the comparison method. For local work,
identify included staged, unstaged, and untracked inputs. An empty comparison
means there is no change in that selection; check the selection before drawing
a conclusion. If the reviewed code changes, reassess affected conclusions.

Map in-scope acceptance criteria to implemented paths and relevant checks. Look
for omitted or partial behavior as well as incorrect code. Distinguish an
implementation mismatch from a flawed requirement or deliberately deferred
work. Without a spec, use contracts supported by callers, interfaces, and
documented behavior; state material assumptions instead of inventing scope.

Read enough implementation and caller context to explain how behavior is
reached. Tests and documentation may share the implementation's mistaken
assumption. Applicable project rules govern conventions; a personal preference
needs a concrete engineering rationale to become a required change.

Read the complete diff within the agreed scope, including relevant tests and
configuration. For a focused review, identify the dimensions assessed. Inspect
the source of generated changes when that is more informative than the output.
State omissions, unavailable context, and incomplete diffs explicitly.

Track the relationship to the change. A newly reachable failure in unchanged
code can be a regression. A pre-existing problem nearby is a separate concern
unless the requested scope includes it. Replacing an established behavior is
not automatically wrong; check whether the replacement is intentional and
supported by its consumers and rollout plan.

## Risk areas

Select the rows affected by the change. Use the remaining areas only when the
surrounding behavior gives a concrete reason to inspect them.

| Change touches | Questions to investigate |
| --- | --- |
| Decisions and calculations | Are units, boundaries, empty values, ordering, and error cases handled according to the contract? Does each branch produce the intended result? |
| User interactions | Can users complete affected tasks through loading, empty, failure, and recovery states? Are relevant keyboard and accessibility interactions preserved? |
| APIs, formats, or configuration | Can existing callers and stored data still be read? Are defaults and validation compatible? Are intentional breaking changes coordinated? |
| Storage or deployment | Can old and new application versions coexist during rollout? Can partially migrated data be handled? What happens after interruption or rollback? |
| Identity or external input | Which identity owns the operation and data? Where are authorization and validation enforced? Do alternate paths preserve those checks? |
| State, retries, or concurrency | Which operations must be atomic? Can partial success, repeated delivery, or a different interleaving duplicate effects, lose updates, or leave invalid state? |
| Resource ownership | Who releases connections, files, locks, and background work on success, failure, and cancellation? Are lifetimes and limits explicit? |
| Performance | How do work, queries, allocations, and retained data grow with the expected workload? Does a claim about a regression require measurement? |
| Interfaces and structure | Does the API reveal its constraints? Is one invariant enforced consistently? Does a proposed abstraction reduce the work and knowledge required of its callers? |
| Tests and user guidance | Do tests distinguish correct behavior from a plausible regression? Have affected usage instructions and operational expectations changed? |

## Evidence standard

For a behavioral issue, connect the trigger to a reachable path and then to a
specific consequence. Check the conditions that could disprove the claim:
upstream validation, authorization middleware, downstream handling, feature
configuration, supported versions, and guarantees made by callers. Inspect the
relevant protection before asserting that it is missing.

Verification can be a focused reproduction, a failing existing test, or a
clear trace through the code. Choose the method that resolves the uncertainty.
For concurrency, describe a feasible sequence of events; a passing test run
alone cannot establish that all interleavings are safe. For performance, show
the growth or measured cost at a relevant workload rather than inferring harm
from an unfamiliar construct.

For UI changes, exercise representative affected interactions or inspect a
suitable demonstration when code inspection cannot establish the result.
Screenshots can establish appearance; interactive behavior needs corresponding
evidence. State what remains unverified when the required environment is absent.

For a design concern, identify who bears the cost and when: callers must repeat
an invariant, a routine feature requires coordinated edits, or an interface
permits a misleading combination of options. Describe a simpler direction and
its tradeoff. A pattern name or a function's length alone is insufficient
justification.

Assess test gaps separately from implementation defects. Request a test when
it protects an important behavior or resolves a specific uncertainty. Explain
the scenario and observable result it should cover. Assertions that merely
repeat implementation details provide weak protection; missing tests alone do
not establish a production failure.

Keep facts, assumptions, and unknowns distinct. If a claim depends on an
unverified condition, investigate it or present a question. Assign impact from
the consequence and affected users; record evidence strength through the
verification actually performed. A model's confidence number adds no proof.

Stop investigating a candidate once decisive evidence supports or refutes it;
continue reviewing the remaining scope. If missing context blocks a decision,
state the specific evidence needed instead of expanding a hypothetical into
more findings. Independent verification can help with consequential disputed
claims, but neither a fixed reviewer count nor repeated agreement proves them.

## Reporting

Present required changes in order of consequence and urgency. Group reports
that share a cause and remedy, while retaining enough locations to show the
affected paths. Keep optional improvements visibly separate. Avoid repeating
automated formatting diagnostics unless they need a human decision.

A useful finding contains:

- A small relevant code range and a title naming the failure or improvement.
  For missing work, cite the acceptance criterion and closest integration point.
- The trigger or affected maintenance task, followed by the consequence.
- The code, requirement, rule provision, or executed check supporting the claim.
- A repair direction that addresses the cause, with any important tradeoff.

For example, in a hypothetical invoice service:

> **Required — Preserve request identity on retry (`billing.py:84`).** If the
> remote service creates the invoice but its response times out, this retry
> creates a fresh request ID. The remote deduplication contract uses that ID, so
> the same order can create a second invoice. Reuse the logical operation's ID
> across attempts. Evidence: traced the timeout handler and request-ID contract;
> no live service call was made.

Write directly about the code and its effects. Provide enough reasoning for
the author to evaluate the conclusion. Distinguish a proposed repair from a
verified fix. A positive observation is useful when it explains a decision
worth preserving.

Conclude with the comparison and scope, checks performed, and unresolved
limitations, including consequential requirements or risk areas left unverified.
Give a readiness assessment within that scope: ready, needs changes, or limited
by missing evidence. If no required changes were found, say so. A limited review
can still report confirmed findings; it does not establish that the rest is
ready. Follow the user's requested output format where one is provided.

## Follow-up reviews

Review the latest revision and verify that each proposed repair closes the
reported path. Check adjacent behavior affected by the repair. Update or
withdraw a finding when new evidence invalidates its assumptions; avoid
repeating a resolved issue solely because an earlier comment exists.

When several implementations meet the contract, explain material tradeoffs
and accept a defensible choice. If a substantive disagreement remains, describe
the competing constraints and the decision needed from the responsible owner.
Record any deferred risk clearly enough to be tracked, without presenting a
planned repair as an existing guarantee.
