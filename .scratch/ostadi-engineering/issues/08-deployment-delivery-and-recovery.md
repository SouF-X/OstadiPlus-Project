# Deployment, delivery, capacity, and recovery boundaries

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 05, 07, 13, 14

## Prerequisites

- [Verify the PostgreSQL application and job-storage stack](14-postgresql-stack-evidence.md)
- [Protected media and offline lifecycle](05-media-and-offline-contracts.md)
- [Provider integration, costs, and processing prerequisites](07-provider-and-cost-decisions.md)
- [Evaluate and agree the database choice](13-database-selection.md)

## Question

Which deployable components, environments, and operating controls make the conditional hosting baseline acceptable for this MVP?

Use the PostgreSQL version/provider evidence and workload/media decisions to assess reverse proxy, API, PostgreSQL-backed Hangfire worker/outbox, private persistent PostgreSQL database, S3/CloudFront, and environment/secrets/network boundaries. Define migrations, GitHub Actions checks, staging/manual production approval, observability, backup/restore, incident/runbook requirements, and empirical capacity/cost acceptance. Preserve the accepted database amendment; the historical SQL Server Express edition/OS/image restrictions do not govern PostgreSQL.

Keep the single Linux VM/Docker Compose and provisional Spain/Paris placement conditional. Plan evidence for 1,500 simultaneous video viewers across the complete system, one-hour database RPO, and four-hour service RTO. Documentation research is not a load/recovery test. Identify any founder-approved baseline amendment needed.

Sources: PRD TE-006/009/018/019, OP-008/009/014.
