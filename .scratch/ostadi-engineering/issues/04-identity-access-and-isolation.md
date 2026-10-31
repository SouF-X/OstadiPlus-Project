# Identity, authorization, and tenant isolation

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 01, 02, 13, 14

## Prerequisites

- [Clean Architecture responsibilities and dependency rules](01-n-tier-responsibilities.md)
- [Business modules and data ownership](02-business-modules-and-data.md)
- [Evaluate and agree the database choice](13-database-selection.md)
- [Verify the PostgreSQL application and job-storage stack](14-postgresql-stack-evidence.md)

## Question

Which authentication, authorization, and isolation contracts must React, Flutter, the API, workers, and persistence share?

Within Identity/OpenIddict and the approved product rules, agree client/session/token/recovery boundaries, actor and tenant context, permission enforcement, delegated authority, key/token handling, EF Core plus PostgreSQL RLS responsibilities, and background-job context. Trace relationship acceptance, dated grants, expiry/revocation, and denied access independently of recorded payments. Specify cross-tenant and privileged-operation failure cases. Account for PostgreSQL role/owner bypass, pooled connections, worker roles, and the accepted database amendment.

Identify threat-review evidence and qualified review prerequisites; do not treat the QA role or team headcount as proof of specialist security coverage. Provider choice belongs in the provider decision.

Sources: PRD TE-005/008/010-012 and OP-011; approved role/access requirements.

Before designing access checks, consult [first-learning source constraints](../../../docs/planning/first-learning-prd-constraints.md): global student identity, connection versus semester/cycle/date-scoped grant, device/session authorization, workspace billing restrictions versus student payment records, individual account suspension versus workspace security blocks, and grant survival during cancellation/collaboration end are distinct conditions.
