# Clarification: Find the Next Decision

Use this reference when vague intent or a consequential ambiguity prevents a useful next step. Its purpose is to close a real decision gap, not to conduct a complete interview for every task.

## Start with what is already known

Read the request, existing requirements, examples, and relevant prior decisions. Extract the user's own account of the problem before proposing a solution. Preserve the difference between the source statement and your interpretation.

For a consequential statement, a compact record is often enough:

| Statement | Status | Source or basis | What remains open |
| --- | --- | --- | --- |
| The user must adopt a research conclusion before it becomes official | User-confirmed, if explicitly stated | Relevant user message or approved requirement | Whether adoption applies to one item or a batch |
| A local store may be sufficient for the first version | Provisional assumption | Single-user, offline scenario | Sharing and recovery needs |

The rows above illustrate the format. They are not requirements for the user's project.

## Ask about work before implementation

A user asking for “an automatic research assistant” may mean finding material, suggesting a next action, recording decisions, or executing work. These are different products and different authority boundaries.

Useful questions include:

- “Which part should it take off your hands first?”
- “Which decisions do you still want to make yourself?”
- “After three days away, what must still be there for you to continue?”

Choose only the questions that change the next decision. Do not ask this whole list by default. If the answer is already supported by the context, use it.

Other decision-changing areas, when relevant:

| Area | Plain-language question | Engineering implication |
| --- | --- | --- |
| History | “If a conclusion changes, must the old conclusion and its evidence be recoverable?” | Versioning and provenance |
| Failure | “If the connection drops after you press Send, what would be worse: a duplicate or a delay?” | Reconciliation and retry behavior |
| Ownership | “Can two people change the same official result?” | Concurrent updates and conflict handling |
| Recovery | “How much work could you afford to lose?” | Backup and recovery objectives |
| Maintenance | “Who will fix this if it breaks six months from now?” | Operational complexity and dependencies |

Explain implications after understanding the answer. Do not make the user choose an architecture term they have no reason to know.

## Make uncertainty useful

When the user does not know, offer a reasonable recommendation, a concrete example, and the tradeoff. Label the recommendation as yours. For example:

> “For the first version, I suggest keeping every adopted conclusion's previous version. That lets you recover from a mistaken edit, at the cost of storing more history. We can decide the storage mechanism after confirming whether recovery matters.”

An assumption can support progress when it is bounded, reversible, and does not silently authorize a material commitment. Write down what would invalidate it. Use a small experiment when the uncertainty is empirical, such as whether a retrieval method finds useful material.

Ask for a decision when ambiguity changes an irreversible action, unacceptable loss, or commitment the user must own. Continue work that does not depend on that answer. Do not convert every unknown into a blocker.

## Turn a scenario into a verifiable requirement

Record enough to answer:

1. **Intent:** what problem or promise justifies it?
2. **Situation:** who acts, under what conditions?
3. **Behavior:** what must happen, and what must remain unchanged?
4. **Boundary:** what is excluded, disallowed, or undecided?
5. **Evidence:** what observation would demonstrate it works?
6. **Status:** confirmed, evidenced, assumed, or undecided?

Example only:

```text
R-003 — Draft; not a requirement until adopted for this project
Intent: The user retains final authority over research conclusions.
Situation: The assistant generates a proposed conclusion.
Behavior: Store it as a suggestion without changing the official conclusion.
Transition: An adoption decision covering that suggestion may promote it.
Acceptance: Generation alone leaves the official conclusion unchanged;
            authorized adoption updates it and preserves the decision context.
```

Avoid acceptance criteria that merely say “works correctly” or prescribe an implementation without a user or engineering reason. Include negative behavior when an important promise depends on something not happening.

## Stop clarifying when the next slice is clear

The next slice is ready when the current scenario, success condition, unacceptable losses, relevant constraints, and implementation boundary are sufficiently understood. Remaining uncertainty should have a named assumption, experiment, deferred decision, or isolated dependency.

A useful handoff is brief:

- What the user has confirmed.
- What you are assuming and why.
- What the next slice delivers and excludes.
- How it will be checked and, where relevant, undone or recovered.
- The one unresolved decision that actually matters next, if any.

Do not turn this into a mandatory form. For a small change, a paragraph may cover it. If another round of discussion would not produce evidence, propose the smallest informative experiment and proceed within the authorized scope.
