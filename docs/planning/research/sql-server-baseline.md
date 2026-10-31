# SQL Server 2025 Express deployment evidence

Retrieved: **2026-10-30**. Scope: the approved SQL Server 2025 Express baseline and proposed Linux/container deployment, including RLS, recovery, EF Core, and Hangfire. This answers [Verify the approved SQL Server deployment baseline](../../../.scratch/ostadi-engineering/issues/03-sql-platform-evidence.md); it does not approve deployment or amend the PRD.

## Findings

**Express exists and is documented for Linux and containers.** Microsoft's version-specific Linux edition table explicitly includes Express with `MSSQL_PID=Express`. It also lists Enterprise, Standard, Enterprise Developer, Standard Developer, and Evaluation; the latter three must not be treated as interchangeable production editions. A claim that SQL Server 2025 Express is Windows-only is contradicted by this source. [Microsoft: Linux 2025 editions](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-editions-and-components-2025?view=sql-server-ver17).

**The exact deployment combination remains a decision.** The SQL Server 2025 supported-platform list includes RHEL 9/10 and Ubuntu 22.04/24.04 and Linux containers; SUSE support ends with SQL Server 2025. Linux minimums are 2 GB memory, two x64 cores, 2 GHz, 6 GB disk, and XFS/ext4. These are startup/platform requirements, not workload sizing. [Microsoft: Linux installation requirements](https://learn.microsoft.com/en-us/sql/linux/install-upgrade/setup?view=sql-server-ver17). RHEL 10 and Ubuntu 24.04 require CU1 or later. [Microsoft: Linux release history](https://support.microsoft.com/en-us/servicing/sql/linux/kb5122767-download-and-install-latest-updates-linux).

Microsoft's container support policy requires the image and host to match Linux distribution **and major version**; merely running successfully does not establish support. Windows containers are unsupported. [Microsoft: technical support policy](https://learn.microsoft.com/en-us/troubleshoot/sql/database-engine/install/windows/support-policy-sql-server). The quickstart documents `mcr.microsoft.com/mssql/server:2025-latest`, with specific tags such as `2025-GA-ubuntu`; images require Intel/AMD x86-64 Linux hosts, and emulation is unsupported. Its default container uses Developer edition. The eventual configuration must explicitly select Express and record the image digest, base OS, host OS, CU/build, and runtime. No image was pulled or executed here. [Microsoft: Docker quickstart](https://learn.microsoft.com/en-us/sql/linux/install-upgrade/quickstart-install-docker?view=sql-server-ver17).

### Edition limits and a material documentation contradiction

| Limit | Express evidence | Infrastructure implication |
| --- | --- | --- |
| Compute per instance | Lesser of one socket or four cores | Additional host cores do not remove this ceiling. |
| Buffer pool per instance | 1,410 MB | This is not a 1,410 MB cap on all SQL process/container memory. |
| Columnstore cache / memory-optimized data | 352 MB per instance / 352 MB per database | Specialized limits, not extra general buffer-pool capacity. |
| Relational database size | Linux-specific 2025 table: **10 GB**; general/Windows 2025 table: **50 GB** | Do not certify 50 GB for the Linux image from these conflicting documents. |

Both edition tables agree on CPU and memory but disagree on database size. The general table is identified by the Linux article as the Windows comparison. The cause could be documentation lag or a platform distinction; neither explanation is established. Confirm the intended Linux build's enforced ceiling and obtain authoritative clarification before depending on capacity above 10 GB. This is an evidence conflict, not proof that Express/Linux is unsupported. [Microsoft: Linux edition limits](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-editions-and-components-2025?view=sql-server-ver17), [Microsoft: general edition limits](https://learn.microsoft.com/en-us/sql/sql-server/editions-and-components-of-sql-server-2025?view=sql-server-ver17).

### Production-use terms

Microsoft's published 2025 Developer/Express/Evaluation license distinguishes Express installation/use rights (§1.b) from Developer/Evaluation's explicit non-production restrictions (§1.a/§1.c). Express commercial hosting is expressly permitted subject to §2.b.iv. That hosting section's “No High Risk Use” clause includes “conducting e-commerce transactions” and refers to monetary/banking transactions (PDF printed page 3; hosting section starts on page 2). **Applicability remains a question for qualified licensing review**, including verification of the exact selected image's accepted EULA. The PRD's recording of external student payments is distinct from executing payment transactions; this research establishes neither incompatibility nor clearance for that behavior. [Microsoft: SQL Server 2025 license terms, §§1 and 2.b.iv](https://www.microsoft.com/content/dam/microsoft/usetm/documents/sql-server/sql-server-2025-developer%2C-express%2C-evaluation/retail/SQL_Server_2025_Developer_Express_and_Evaluation_Edition_English.pdf).

### Isolation and recoverability

- **RLS is available in Linux Express.** The edition table marks it supported, but marks TDE and native backup encryption unavailable. Express also lacks Always On availability groups/FCIs, log shipping, and backup compression. [Microsoft: Linux edition capabilities](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-editions-and-components-2025?view=sql-server-ver17).
- RLS uses security policies and inline table-valued predicates: filters restrict visible rows; block predicates reject prohibited writes. Microsoft's middle-tier example sets `SESSION_CONTEXT` after opening a connection. Consequently tenant/user context, pooled connections, worker connections, raw SQL, write predicates, and privileged maintenance need explicit isolation verification; an EF query filter alone does not establish database RLS. [Microsoft: RLS design and middle-tier example](https://learn.microsoft.com/en-us/sql/relational-databases/security/row-level-security?view=sql-server-ver17).
- Linux supports native database backup/restore using `sqlcmd`; Microsoft describes backup functionality as the same across platforms, subject to edition limits. [Microsoft: Linux backup/restore](https://learn.microsoft.com/en-us/sql/linux/business-continuity/backup-restore/database-backup-restore?view=sql-server-ver17). Express supports full, differential, and transaction-log backups but has **no SQL Server Agent**; backup scheduling requires another scheduler. Microsoft's example uses Windows Task Scheduler and does not itself specify a Linux scheduler. [Microsoft: Express backup automation](https://learn.microsoft.com/en-us/troubleshoot/sql/admin/schedule-automate-backup-database).
- Express defaults to **simple** recovery, which has no transaction-log backups or point-in-time restore. Full recovery requires log backups; backup chains, retention, log growth, and restore procedures must implement the chosen RPO/RTO. Backups do not confer automatic failover. [Microsoft: recovery models](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/recovery-models-sql-server?view=sql-server-ver17). Container removal can discard non-persisted data, so durable volumes and independently retained backups are required. [Microsoft: Docker persistence warning](https://learn.microsoft.com/en-us/sql/linux/install-upgrade/quickstart-install-docker?view=sql-server-ver17).

### EF Core and Hangfire compatibility

- Microsoft's provider list covers SQL Server 2012 onward for `Microsoft.EntityFrameworkCore.SqlServer` (EF Core 8/9/10) and warns that provider major versions generally must match EF Core. [Microsoft: provider compatibility](https://learn.microsoft.com/en-us/ef/core/providers/). The provider uses `Microsoft.Data.SqlClient`. Its `UseCompatibilityLevel` affects generated SQL, not the database's actual compatibility level; configure and verify both for the selected package/build. This is documentation compatibility, not a tested project package combination. [Microsoft: SQL Server EF provider](https://learn.microsoft.com/en-us/ef/core/providers/sql-server/).
- Hangfire's own SQL storage documentation supports SQL Server 2008 R2 and later, any edition, and shows an Express connection. Hangfire.SqlServer 1.8 prefers `Microsoft.Data.SqlClient` when installed and supports explicit factory selection. This supports feasibility with Express 2025, but is not a separate 2025/Linux certification or workload benchmark. Pin versions and verify schema installation/upgrade permissions, SQL client/TLS behavior, job execution, retries, polling, and shutdown recovery. [Hangfire: SQL Server storage](https://docs.hangfire.io/en/latest/configuration/using-sql-server.html).

## Gates for the infrastructure decision

Keep the approved database/version/edition baseline while closing these gates; no replacement architecture is selected:

1. Confirm the Linux database-size contradiction and applicable hosting/payment terms. Retain the exact image EULA and written clarification where needed.
2. Select and verify the supported host/image/CU/CPU/runtime combination and explicit Express edition. Technical feasibility and Microsoft support are separate checks.
3. Measure the **combined application, Hangfire, outbox, and history** workload on that configuration: database/index growth and retention, buffer pressure, CPU, locks/deadlocks, job throughput, request latency, I/O, and backup interference. Decide shared versus separate database placement explicitly; instance CPU/memory limits remain shared. No capacity measurements were performed in this research.
4. Prove tenant isolation across requests and workers and rehearse full/log restore, container replacement, off-host recovery, and alerts against agreed RPO/RTO. Choose backup protection compatible with Express's absent native encryption; define the scheduler and operator ownership.

If a gate contradicts a PRD promise, an explicit amendment may be needed. Research resolution means the documented facts and unknowns are captured, not that those gates passed.

## Publication limitation

This workspace has no Git repository or remote. The wayfinder research branch/push workflow is unavailable; findings are preserved in this local Markdown artifact and linked from the research ticket. No repository was initialized, no remote added, no branch pushed, and no provisioning or application execution occurred.
