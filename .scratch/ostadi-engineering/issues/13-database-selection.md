# Evaluate and agree the database choice

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: resolved
Blocked by: 01, 03

## Prerequisites

- [Clean Architecture responsibilities and dependency rules](01-n-tier-responsibilities.md)
- [Verify the approved SQL Server deployment baseline](03-sql-platform-evidence.md)

## Question

Which database engine, edition, and deployment assumptions should the developer accept for Ostadi Plus after architecture suitability is agreed?

Use the PRD's SQL Server 2025 Express proposal as the documented baseline, not automatic approval. Explain fit, relevant alternatives, team experience, isolation, transactions, edition/platform limits, licensing applicability, operational burden, and cost. Use the research evidence while distinguishing documented facts from remaining unknowns. Recommend an option, discuss it with the developer, and record explicit agreement before dependent database-specific design. Document any agreed departure from the PRD as an amendment; no database is selected by this ticket's creation.

## Comments

Architecture boundaries and selective interfaces were accepted on 2026-10-31. Both blockers are resolved; this ticket is claimed for the next conversation. Distinguish engine/provider choice from production edition, platform configuration, and capacity validation. The existing SQL research is evidence, not database approval. Production license/hosting budget remains unspecified.

### Zero license-fee constraint and revised recommendation — 2026-10-31

The developer states that paid software/database licenses cannot be funded. Hosting/cloud/VPS and storage spending is possible, with no approved amount. They want strong performance within that constraint. They answered the licensing question only; the earlier SQL Server engine proposal has not been accepted.

Recommend evaluating PostgreSQL with EF Core/Npgsql as the preferred engine under this constraint, subject to explicit agreement to amend the SQL Server baseline and verification of the selected package/provider/operations configuration. This recommendation is about license-free growth and viable resource use, not an unmeasured claim that PostgreSQL is faster. SQL Server Express remains a valid license-free candidate with edition resource caps; do not certify its combined-workload suitability without evidence.

Current primary-source evidence:

- [PostgreSQL license](https://www.postgresql.org/about/licence/) permits use without a license fee under its terms. [PostgreSQL limits](https://www.postgresql.org/docs/current/limits.html) and [resource configuration](https://www.postgresql.org/docs/current/runtime-config-resource.html) distinguish technical/hardware limits and tuning from a paid-edition upgrade. Hosting, operations, and backups still have costs.
- [Npgsql's EF Core provider](https://www.npgsql.org/efcore/) supplies EF Core integration. [PostgreSQL row security](https://www.postgresql.org/docs/current/ddl-rowsecurity.html) supplies database RLS; its owner/superuser bypass rules, tenant context, pooling, and worker behavior need explicit design and real-database tests.
- [SQL Server 2025 Linux edition limits](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-editions-and-components-2025?view=sql-server-ver17) document Express CPU and buffer-pool caps. The earlier SQL evidence records the conflicting database-size documentation and other gates; it remains valid evidence if SQL Server is retained.
- [Hangfire.PostgreSql](https://github.com/hangfire-postgres/Hangfire.PostgreSql) offers a PostgreSQL storage implementation. [Hangfire's extension policy](https://www.hangfire.io/extensions.html) distinguishes community extensions from officially supported storage. A move from the PRD's SQL Server-backed Hangfire requires reviewing this provider's compatibility, maintenance, license obligations, and failure/recovery behavior. Its existence is not an integration-test result.

Trade-offs for discussion: PostgreSQL SQL/administration and RLS design need to be learned or verified; EF migrations/provider-specific behavior, Hangfire storage, backup/recovery, and CI database tests must be adapted from the documented SQL Server baseline. No application schema exists yet, so this is an early architecture amendment proposal, not a request to migrate an existing production database. Preserve the approved authorization, job/outbox, recovery, and release requirements.

Status: recommendation awaiting the developer's agreement. No database engine is accepted and no PRD amendment is enacted by this note.

### Conditional agreement and Npgsql explanation

The developer answered that they agree under the condition of first understanding what Npgsql is. Keep this ticket claimed and the PostgreSQL amendment conditional while answering that question; no final database Answer or accepted ADR is recorded yet.

Clarification: [Npgsql](https://www.npgsql.org/doc/index.html) is the .NET PostgreSQL database driver. [Npgsql.EntityFrameworkCore.PostgreSQL](https://www.npgsql.org/efcore/) is the EF Core provider built on that driver, configured with UseNpgsql. These are application libraries used by Infrastructure, not an extra hosted service or a replacement for EF Core.

## Answer

Resolved on 2026-10-31. After conditionally agreeing and asking what Npgsql is, the developer received the driver/provider/cost explanation and replied "done next ?" to the confirmation question. PostgreSQL with EF Core and the Npgsql provider is accepted as the database direction, replacing the PRD's SQL Server 2025 Express baseline. The reason is zero available software/database license budget and room for resource growth through hosting investment; no comparative performance benchmark has been claimed.

Record: [Use PostgreSQL with EF Core and Npgsql](../../../docs/adr/0002-postgresql-persistence.md). PostgreSQL/EF/Npgsql package versions, hosting configuration/sizing, tenant/RLS implementation, Hangfire storage integration, migrations, and backup/recovery remain subject to supporting verification and their relevant design decisions. The product authorization and full release requirements remain unchanged. The original DOCX has not been edited.

Follow-up: [Verify the PostgreSQL application and job-storage stack](14-postgresql-stack-evidence.md) supplies version/provider evidence; infrastructure and isolation tickets carry the applicable implementation/recovery gates. Earlier SQL Server evidence remains historical comparison material and does not impose SQL Server-specific production constraints on the chosen PostgreSQL deployment.
