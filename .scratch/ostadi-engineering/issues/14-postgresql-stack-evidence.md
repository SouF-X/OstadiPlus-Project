# Verify the PostgreSQL application and job-storage stack

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: research
Label: wayfinder:research
Status: resolved
Blocked by: 13

## Prerequisites

- [Evaluate and agree the database choice](13-database-selection.md)

## Question

Which currently supported .NET/EF Core/Npgsql/PostgreSQL version combination and PostgreSQL-backed Identity/OpenIddict/Hangfire integrations are documented as compatible with the chosen stack and zero license-fee constraint?

Use current primary sources to identify one viable candidate combination, any package-major-version conflicts, maintenance/support and free-versus-paid distinctions, and practical pre-implementation checks. Verify the Hangfire.PostgreSql community provider and its requirements rather than treating the SQL Server storage package as reusable. Distinguish documented compatibility from a measured or executed integration. Preserve Identity/OpenIddict, durable jobs/outbox, and database RLS requirements; do not silently substitute technologies or select a production host.

Capture PostgreSQL RLS role/owner bypass and pooled tenant-context hazards plus backup/PITR support as design/test gates, not solved behavior. Write a concise cited note under docs/planning/research/. No application code, package installs, provisioning, or runtime tests are authorized by this research ticket. The workspace has no Git repository/remote; retain local evidence and record the unavailable branch/push publication.

## Answer

Resolved 2026-10-31: [PostgreSQL application and job-storage evidence](../../../docs/planning/research/postgresql-stack.md) captures current primary-source version/dependency and fee/support evidence. The viable application candidate uses stable .NET/ASP.NET Core 10, EF Core 10, Npgsql EF provider/driver 10, and PostgreSQL 18. Identity EF 10 and OpenIddict EF 7.7.2 declare intersecting EF requirements. Source-dated package patches are recorded as provisional evidence; exact deployment pinning and PostgreSQL minor release-date verification remain future checks.

Hangfire.PostgreSql 1.21.1 is the separate LGPLv3 community storage candidate with Hangfire 1.8 integration. Its Npgsql >=6.0.11 range admits the driver 10 candidate but does not prove runtime compatibility across driver majors. Official Hangfire community-extension support excludes a provider guarantee; paid Pro/Ace features are outside the zero-fee candidate. The note retains real-PostgreSQL integration, migrations/authentication, job failure/recovery/outbox, RLS runtime-role/owner bypass, pooled tenant-context isolation, and backup/PITR restore drills as implementation/release gates.

This resolves the factual research scope only. No code, installs, runtime tests, provisioning, performance comparison, host selection, legal conclusion, or production readiness claim was made. Evidence is local-only because no Git repository/remote exists; branch/push publication was unavailable and not attempted.
