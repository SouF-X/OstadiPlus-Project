# Ostadi Plus

Planning repository for the Ostadi Plus MVP, a teacher-first learning platform.

**Current stage:** engineering planning. No application projects, production code, or deployment have been created.

## Where we stopped

Planning paused at the developer's request on **2026-10-31**, during the discussion of business modules and the first protected-learning workflow.

Read the [pause checkpoint](docs/planning/checkpoint.md) to resume. The next question is whether to store the **Connection** and **Course-access grant** as separate records. This proposal has **not** been accepted yet.

## Agreed direction

- ASP.NET Core modular monolith with Clean Architecture: Domain, Application, Infrastructure, and API.
- React/TypeScript for web and Flutter for mobile.
- PostgreSQL with EF Core and Npgsql, replacing the approved PRD's SQL Server baseline through a recorded engineering decision.
- Eight initial business areas within the same backend, with explicit ownership of data changes and a shared PostgreSQL starting point.
- No paid software/database licenses. Hosting and storage spending can be considered; no amount has been agreed.
- The team chooses its own work assignments. No delivery dates have been imposed.

## Project documents

- [Approved PRD](docs/requirements/Ostadi_Plus_MVP_PRD_Phase_24_Approved.docx): unchanged source document; recorded engineering amendments are separate.
- [Engineering decision map](.scratch/ostadi-engineering/map.md) and its linked decision tickets.
- [Architecture decisions](docs/adr/).
- [Domain glossary](GLOSSARY.md).
- [First-learning PRD constraints](docs/planning/first-learning-prd-constraints.md).
- [Developer baseline](docs/planning/developer-baseline.md).
- [Research notes](docs/planning/research/).

The local Markdown tracker remains the source for decision status. Installed guidance skills are under `.agents/skills/`, with their sources recorded in `skills-lock.json`.

The first protected-learning workflow is an implementation milestone. The full approved MVP and release gates remain required before the pilot.
