# First specification handoff and staged MVP route

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 06, 09, 13, 14

## Prerequisites

- [Evaluate and agree the database choice](13-database-selection.md)
- [Verify the PostgreSQL application and job-storage stack](14-postgresql-stack-evidence.md)
- [First learning workflow and shared API contracts](06-first-learning-api-contracts.md)
- [First learning workflow acceptance and verification](09-first-workflow-qa.md)

## Question

When are the shared architecture and first learning workflow decisions sufficient to produce its buildable specification, and what dependency order carries the team through the remaining approved MVP?

Identify the first to-spec input set, implementation prerequisites, unresolved assumptions, and engineering decisions that can safely wait until their dependent workflows. Sequence M1 architecture, M2 foundations, M3 protected learning, M4 the remaining complete MVP, M5 full acceptance/readiness, M6 controlled pilot, and M7 authorized expansion. Keep all day-one features while permitting later workflow design during earlier implementation.

Choose vertical workflow boundaries and review checkpoints; leave person-by-person development allocation to the team. Carry remaining map questions forward explicitly. The first workflow can graduate to to-spec/to-tickets without closing unrelated later-workflow decisions; any deployment or real-data prerequisite must still be satisfied before the governed activity.

Sources: PRD TE-016 and RD-006-013; approved user scope.
