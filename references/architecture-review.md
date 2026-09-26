# Architecture and Review: Make Responsibility Visible

Use this reference when translating requirements into a maintainable design or inspecting a proposal, implementation, or resumed project. Select the parts relevant to the current risk and evidence; this is not a mandatory checklist for every edit.

## Map the current promises

Start from the effective agreement. For each critical requirement, identify its responsible component, data or state boundary, implementation location when available, and verification evidence. Follow the relationship in reverse for a major component: what need or operational constraint justifies its existence?

Example only:

| Requirement | Responsibility | Boundary | Verification |
| --- | --- | --- | --- |
| R-003: The user adopts research conclusions | Adoption operation | Suggestion and official conclusion are distinct states | Generation cannot adopt; authorized adoption can |
| R-007: Work survives an interrupted session | Persistence and restart flow | Saved progress versus temporary work | Restart recovers the documented checkpoint |

Do not treat these example requirements as adopted. Do not demand a one-to-one relationship between features and modules: shared infrastructure may serve several explicit needs.

## Choose views that answer questions

| View | Question it should answer |
| --- | --- |
| System boundary | Who uses the system, what does it own, and what does it depend on? |
| Responsibility structure | Which component owns each important capability and interface? |
| Data and authority | Which information is raw evidence, a suggestion, or an official decision, and who may change it? |
| Critical flow or state model | What happens on success, failure, retry, cancellation, and human intervention? |
| Operation and recovery | Where does it run, how is failure diagnosed, how is data restored, and who maintains it? |

Create only views that remove a meaningful ambiguity. Label uncertain parts as assumptions. A diagram is useful when a reader can follow responsibility through it; visual completeness is not evidence of architectural completeness.

## Reason through one critical path

Follow the most important user scenario end to end. Where relevant, include:

- Entry conditions, inputs, validation, and ownership.
- State changes and the authority required for them.
- External effects and what can be observed afterward.
- Failure, cancellation, partial completion, and recovery.
- The acceptance observation and actual user outcome.

An external request timing out does not prove the action failed. If repeating it can create harm or duplication, represent the uncertain outcome and reconcile with the external state before choosing a retry. Do not claim “exactly once” merely because a retry loop exists.

Separate generating a candidate, recommending it, adopting it, and executing it whenever they carry different consequences. Reuse the user's existing authorization for the relevant scope; do not invent a human approval step for every state transition.

## Match complexity to the people who will maintain it

For a consequential design choice, explain the problem it solves, a credible simpler alternative, the operational cost, and what would make the choice worth revisiting. Record decisions whose reasons would otherwise be lost; skip ceremony for ordinary implementation details.

A single maintainer's limited time is a real constraint, but it does not universally mandate one process, one database, or local hosting. Likewise, scale is not a justification until there is a relevant need, credible expectation, or measurement.

Inspect applicable recovery, migration, observability, and dependency risks in proportion to the task. Do not add a service, governance system, or generic hardening program merely because this reference mentions it.

## Produce evidence-scoped findings

Read the actual artifact before claiming to review it. Separate inspection from execution, and planned verification from observed results. A passing unit test supports its tested behavior; it does not by itself prove the production workflow or the underlying product assumption.

Use a finding like this when a concrete conflict exists:

```text
Verdict: BLOCKER for automatic adoption in this change.
Evidence: [actual file, location, or inspected design statement]
Agreement: [current adopted requirement and source]
Consequence: Generated suggestions become official without the required decision.
Minimum remedy: Preserve the suggestion state; use the authorized adoption path.
Verification: Generation leaves official state unchanged; adoption changes it.
Alternative: If the user intends automatic adoption, record its scope and impacts
             as a deliberate change before implementing that changed promise.
```

This is a format example, not a prewritten finding to issue without evidence.

Use PASS, CONCERN, BLOCKER, and UNKNOWN as defined in `SKILL.md`. Name the inspected scope even when it passes. For UNKNOWN, specify the missing artifact, run, or decision and what it would establish. When only one action is affected, continue independent work.

Do not disguise personal taste as a hard constraint. “Best practice” requires an explanation of the concrete failure it prevents and when that advice applies. Reversibility, likelihood, consequence, and current maintenance capacity should shape the response.

## Handle drift and corrections

A mismatch can be an implementation defect, an outdated document, or an authorized change whose records have not caught up. Determine which before accusing anyone of violating the agreement.

For an authorized material change, preserve the old rationale, identify the replacement promise and consequences, and update related acceptance and design records. Do not quietly lower an acceptance bar to make failing work appear complete. A deliberately changed acceptance criterion is valid when it reflects the user's actual changed intent and its effects are explicit.

When evidence disproves your finding, retract it plainly, explain the corrected reading, and update affected advice. Do not preserve a false objection to remain “stubborn.”

## Resume and hand off

Before recommending the next action, establish which records are current and what implementation or revision was actually inspected. Keep planned, implemented, and verified states distinct. Reconcile contradictory status claims with evidence or mark them unknown.

A useful restart note identifies the current promise, important decisions, checked artifacts, outstanding work, unresolved risks, and next useful step. Link existing records where possible. Do not claim a project is ready to release solely because its requirements or architecture were reviewed.

End a substantial review with actionable next steps and enough evidence for another maintainer to reproduce the conclusion. The goal is a project that can continue without this particular reviewer.
