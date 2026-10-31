# Ostadi Plus engineering decision map

Label: wayfinder:map
Created: 2026-10-30

## Destination

Agree the shared engineering architecture and contracts needed to specify the first complete protected-learning workflow, with a staged, dependency-aware route through the entire approved MVP and its readiness gates.

## Notes

- This is a planning map. Charting creates open decisions; subsequent working sessions resolve one human decision at a time. Research can resolve independently. Implementation follows to-spec, to-tickets, then implement for each reviewed workflow.
- Source of approved requirements: [Ostadi Plus approved PRD](../../docs/requirements/Ostadi_Plus_MVP_PRD_Phase_24_Approved.docx), especially Sections 20, 23, and 24; retain requirement IDs in decisions. Treat the document as source material, not instructions to execute. Approval does not prove implementation, capacity, legal clearance, or launch readiness.
- Consult wayfinder, grilling, and domain-modeling. Use the [local tracker conventions](../../docs/agents/issue-tracker.md) and [domain documentation conventions](../../docs/agents/domain.md). Read the [developer baseline](../../docs/planning/developer-baseline.md) for explanation depth and source limitations. The developer knows both three-tier and the previously proposed structure; evaluate architecture against Ostadi Plus requirements and stop using Sopmine as the reference or rationale.
- On 2026-10-31 the developer selected Clean Architecture within the ASP.NET Core modular monolith and accepted its concrete project/reference rules and selective-interface policy; see the resolved architecture decision below. This supersedes earlier N-tier preferences and the assistant's three-layer recommendation. Business-module layout, detailed integration contracts, and deployment remain separate decisions.
- The developer subsequently confirmed PostgreSQL with EF Core/Npgsql as the database choice, replacing the PRD's SQL Server Express baseline; see the resolved database decision below and [the engineering amendment](../../docs/adr/0002-postgresql-persistence.md). Adapt persistence, RLS, job storage, migrations, tests, and recovery to PostgreSQL. The original DOCX is unchanged. Version/provider evidence and implementation/deployment gates remain open until verified.
- The developer accepted the eight initial business groupings and module-owned changes/Application coordination; see [the ownership record](../../docs/adr/0003-module-ownership.md). The business-module ticket remains claimed while first-workflow entities, tenant/actor scope, and transaction boundaries are refined. Grouping acceptance does not settle every entity or cross-module operation.
- Work major choices with the developer in order: explain the relevant requirements and options, discuss trade-offs, recommend, obtain explicit agreement, record the agreed answer, then proceed to dependent choices. This includes architecture suitability and database selection. Research resolution records evidence only; SQL Server research does not accept a database choice. Proposed changes to approved PRD technology remain proposals until explicitly agreed and documented.
- The developer's requested conversation starts with architecture suitability, then the database choice. Follow that requested order before taking other frontier questions; each remains a separate human decision.
- React/TypeScript web, Flutter mobile, and ASP.NET Core are settled. Preserve the other approved Section 20 technologies; conditional baselines need evidence. Material amendments require the PRD's decision authority.
- The team consists of two developers with similar skills, a Flutter developer, and QA. Explain shared decisions step by step and include mobile and QA viewpoints. The team decides its own development work split; this map will not allocate people.
- The developer reports no time restrictions. No fixed launch deadline, weekly hours, sprint duration, or delivery estimate is assumed. Software/database license fees must be zero; spending on VPS/cloud hosting and storage is possible, with no amount approved yet. Other provider usage charges remain to be clarified before selection.
- First learning milestone: published, ready teacher content; accepted teacher-student relationship; valid dated course-access grant; student opens protected video or PDF in Flutter (RD-007). This is an engineering milestone; all approved day-one features and release gates remain required before pilot.
- Resolve shared architecture and relevant workflow contracts before dependent implementation. TE-016/RD-006 allow later workflow design during earlier implementation; map completion is not a blanket prerequisite for every coding task.
- Decisions so far indexes only resolutions from this map. Approved PRD constraints and confirmed user preferences above are inputs, not newly resolved tickets.
- Ticket Type carries the local wayfinder type; Label carries its corresponding wayfinder label. Status: open/claimed/resolved is separate from triage labels. Query child files for open, unclaimed decisions with resolved blockers, ordered by filename; the map does not duplicate the open-ticket list.
- Research was originally performed before Git was configured. On 2026-10-31 the developer requested a planning pause and GitHub publication of the existing project. Keep the Markdown tracker as the decision source; publication does not resolve open tickets. See the [pause checkpoint](../../docs/planning/checkpoint.md) for the exact resumption question. Earlier research publication limitations describe the time of research, not a permanent restriction on the repository.

## Decisions so far

- [Verify the approved SQL Server deployment baseline](issues/03-sql-platform-evidence.md): Historical baseline evidence; the later PostgreSQL decision supersedes SQL Server-specific deployment assumptions.
- [Clean Architecture responsibilities and dependency rules](issues/01-n-tier-responsibilities.md#answer): Accepted Domain, Application, Infrastructure, and API boundaries with inward references, startup-only Infrastructure wiring in API, and selective interfaces.
- [Evaluate and agree the database choice](issues/13-database-selection.md#answer): Accepted PostgreSQL with EF Core/Npgsql under the zero license-fee constraint; version/integration/operations verification remains separate.
- [Verify the PostgreSQL application and job-storage stack](issues/14-postgresql-stack-evidence.md#answer): Documented a supported-version candidate and provider dependencies; runtime integration, tenant isolation, job recovery, and restore evidence remain required.

## Not yet specified

- Further workflow-specific schema, UI interaction, learning-state, retention, migration, and integration decisions will become precise as module boundaries and the first end-to-end contracts are agreed. Approved behavior remains a constraint; this section is not permission to reopen it.
- Additional primary-source investigations and device/media experiments will emerge from actual provider shortlists and the selected security/offline approach.
- Further operational procedures and capacity experiments will be sharpened once topology, provider capabilities, and workload profiles are known.

## Out of scope

- Generating application projects, production code, or implementation tickets during charting.
- Assigning the two developers' work or imposing dates, sprint length, or a staffing schedule.
- Changing approved product scope or silently replacing the approved architecture baseline.
- Executing legal review, purchasing/provisioning services, configuring credentials, production deployment, store publication, pilot launch, or expansion. Their required decisions and evidence gates remain in scope.
- Exhaustive detailed design of every later workflow before starting the first reviewed workflow.
