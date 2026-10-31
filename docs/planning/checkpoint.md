# Planning checkpoint — 2026-10-31

Planning is paused at the developer's request. Publishing the existing planning project to GitHub does not approve any pending design choice or start application implementation.

## Accepted decisions

- [Clean Architecture](../adr/0001-clean-architecture.md): Domain, Application, Infrastructure, and API, with inward dependencies and interfaces only for actual capabilities.
- [PostgreSQL persistence](../adr/0002-postgresql-persistence.md): EF Core/Npgsql; the original PRD is unchanged. Exact versions and runtime/operational verification remain separate gates.
- [Module ownership](../adr/0003-module-ownership.md): Identity and organizations, Relationships and access, Content, Media and offline, Learning, Student finances, Teacher billing, and Operations. These are logical groupings inside one backend, initially sharing PostgreSQL.
- React/TypeScript web, Flutter mobile, and ASP.NET Core backend.

## Exact stopping point

Active decision: [02 — Business modules and data ownership](../../.scratch/ostadi-engineering/issues/02-business-modules-and-data.md), still **claimed**, not resolved.

The initial module groupings and ownership rule are accepted. The first-workflow records, relationships, tenant/actor scope, transactions, and concurrency rules are still being discussed.

The developer requested a simpler explanation. We explained the difference between a Connection and a Course-access grant, then stopped before receiving an answer to the next question.

## Resume with this question

**Do you agree to store the Connection and Course-access grant as separate records?**

Recommendation: yes. A student can have an accepted Connection before any course is assigned. A Course-access grant has its own course/semester scope, academic cycle, dates, and history. The PRD requires the distinction; separate records are the proposed implementation.

**No acceptance has been recorded.**

## Following question, also unanswered

Should lesson edits use draft revisions with an explicit published revision reference, while uploaded files have separately tracked Media versions?

Recommendation: yes, so students keep seeing the published lesson while a teacher prepares changes. The PRD requires this visibility behavior; the exact revision representation is still a proposal.

## How to continue

Discuss one choice at a time in plain language. Get the developer's agreement before treating a proposal as decided. Preserve the approved PRD requirements. Do not use Sopmine as the teaching reference, assign team members' work, or infer deadlines.

After these representation choices, refine the first-workflow relationships, actor/workspace scope, transaction boundaries, duplicate prevention, and concurrency behavior. Keep ticket 02 claimed until its scope is sufficiently covered. Then follow dependencies in the [engineering map](../../.scratch/ostadi-engineering/map.md) for identity/access, media, API contracts, and QA scenarios before dependent implementation.

No application code, solution skeleton, services, infrastructure, or deployment has been created. Research notes are evidence, not runtime validation or production-readiness approval.
