# Verify the approved SQL Server deployment baseline

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: research
Label: wayfinder:research
Status: resolved
Blocked by: none

## Question

What do current Microsoft primary sources establish about the PRD's SQL Server 2025 Express edition and proposed Linux/container deployment?

Verify supported edition/platform/image combinations, production-use terms, CPU/memory/database limits, SQL row-level security and recovery/backup capabilities, and relevant EF Core/Hangfire compatibility from their primary sources. Identify contradictions or unknowns; distinguish documentation support from measured suitability for the combined application, Hangfire, outbox, and history workload.

Preserve the approved baseline while reporting any amendment that may be needed. Do not silently substitute a different database, edition, operating system, or managed service. Document sources, retrieval date, remaining empirical checks, and implications for the infrastructure decision. This is evidence gathering, not capacity certification or a final hosting decision.

Write findings under docs/planning/research/. This workspace currently has no Git repository or remote: record the unavailable branch/push publication separately; retain a usable local evidence artifact.

Sources: PRD TE-006/009/018 and OP-009.

## Answer

Resolved the factual research question on 2026-10-30. See [SQL Server 2025 Express deployment evidence](../../../docs/planning/research/sql-server-baseline.md) for current primary-source citations, retrieval date, and remaining gates.

- Microsoft explicitly documents SQL Server 2025 Express for Linux and containers (`MSSQL_PID=Express`). Supported operation requires a verified x86-64 host/image/platform combination; image and host Linux distribution and major version must match under Microsoft's support policy.
- CPU and buffer-pool ceilings are the lesser of one socket/four cores and 1,410 MB. A material source contradiction remains: the Linux edition table says 10 GB per database; the general/Windows table says 50 GB. Do not certify Linux capacity above 10 GB from those conflicting sources.
- RLS and native backup/restore are available; Express lacks SQL Agent, backup compression/encryption, and Always On. Simple recovery is the default; point-in-time recovery requires a designed full-recovery/log-backup chain and tested restore process.
- Microsoft EF Core SQL Server provider and Hangfire SQL storage documentation support compatibility in principle; the exact pinned package/image combination and combined app/Hangfire/outbox/history capacity remain empirical gates.
- Express commercial hosting is permitted subject to published terms. A hosting clause mentioning e-commerce requires qualified applicability review against the exact EULA and intended behavior; recording external payments differs from executing transactions. This is not a finding that the PRD is incompatible.

The approved baseline is preserved. This resolves research only, not licensing clearance, capacity certification, a PRD amendment, or deployment approval. Branch/push publication was unavailable because this workspace has no Git repository or remote; evidence is retained locally, without initializing Git, provisioning, or running application code.
