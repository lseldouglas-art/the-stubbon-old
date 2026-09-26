# Architecture and responsibility

Adapt only the sections needed for the current slice. A complete architecture explains current responsibilities and important failures; it does not predict every future feature.

## Scope and evidence

- Contract version and requirement IDs:
- Current implementation inspected:
- Proposed design versus observed implementation:
- Unverified assumptions:

## System boundary

Name users, external systems, internal responsibilities, and what is outside the system. Draw the smallest useful diagram with labeled boundaries and arrows. Do not invent services to fill a diagram.

## Responsibility and traceability

| Requirement / operational constraint | Responsible component | Data owner and allowed changes | Implementation location | Verification evidence |
| --- | --- | --- | --- | --- |

Trace in both directions: each critical requirement has an owner and evidence; each significant component has a requirement or justified operational purpose.

## Critical flow

Describe normal behavior and relevant states for failure, retry, cancellation, human confirmation, and uncertain external outcomes. State which transitions need authorization and how it is recorded. If an external operation times out, distinguish unknown completion from confirmed failure before retrying.

## Decisions and maintenance cost

For each consequential choice, link a decision record containing alternatives, tradeoffs, reversibility, and a revisit trigger. Explain why the maintainer can operate the chosen dependencies.

## Running and recovering

- Runtime and deployment location:
- Failure signals and diagnosis:
- Backup and restoration needs:
- Migration and rollback path:
- Maintainer and handoff requirements:
- What has actually been tested:

## Next verifiable slice

- Smallest end-to-end behavior:
- Required evidence before starting:
- Acceptance checks:
- Reversal or containment plan:
