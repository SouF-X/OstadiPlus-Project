# Developer baseline for guided implementation

Assessed on 30 October 2026 through representative source inspection. This is a provisional guide for choosing explanations and exercises, not a verified professional seniority rating. No builds, tests, migrations, deployments, or changes were performed in the inspected projects.

## Goal and working approach

The developer wants guidance from architecture through completion of the Ostadi Plus MVP, adapted to their experience. Evaluate architecture against Ostadi Plus requirements and work through design and implementation incrementally. The developer explicitly asks to stop using Sopmine as the comparison or justification and confirms knowing both three-tier and the previously proposed structure. There is enough context to begin architecture planning; refine explanation depth through actual design work rather than requiring a separate proficiency interview first.

The PRD covers product, business, legal, operational, and engineering requirements. Focus development sessions on engineering while tracking the other prerequisites before the activities they govern. Preserve approved product decisions and the Section 20 architecture baseline unless an explicit amendment is agreed.

## Evidence inspected

- [Learning archive](https://github.com/SouF-X/learning-archive): repository organization and README; recursive file inventories for selected learning groups; representative DVLD business-layer code, ASP.NET authentication configuration, and MechanicShopWorkshop domain, command-handler, API-test, and frontend-learning files.
- `C:/Users/ACER/Desktop/FreelanceProjects/SopmineShopManagementSystem`: README, client controller, client service, and EF Core repository. This project has API, Business, and Data responsibilities and implemented client CRUD.
- `C:/Users/ACER/Desktop/FreelanceProjects/SopmineShopManagement`: README, invoice controller and command handlers, payment entity and tests, persistence-test code, frontend form code, Dockerfile, CI workflow, and recovered-release documentation. It contains API, Application, Domain, Infrastructure, and Contracts projects, a vanilla JavaScript frontend, and automated checks.

Course material and project code demonstrate available examples and technical exposure. They do not establish authorship, independent understanding, successful current execution, or production readiness. Deployment statements in project documentation were not independently verified.

## Developer confirmations

- The developer confirms that the completed Sopmine project is finished and hosted. Hosting is developer-reported; no live deployment inspection was performed. This remains historical assessment evidence; the developer subsequently asked to stop using it as the architecture reference or justification.
- React for web and Flutter for mobile are confirmed choices for Ostadi Plus, consistent with the PRD baseline. Treat these as settled technology choices. Experience with these frameworks remains a separate question from their selection.
- The team has four people: the developer, another developer described as having similar skills, a Flutter developer, and a QA developer. Similarity of the second developer's skills is developer-reported; individual responsibilities and availability have not yet been assigned or confirmed.
- During wayfinder charting, the developer confirmed a preference for API, business-logic, and data-access separation while preserving the PRD modular monolith. Exact project structure, dependency direction, and deployment boundaries remain open decisions in the [engineering map](../../.scratch/ostadi-engineering/map.md).
- The developer reports no time restrictions. Do not infer weekly hours, a fixed deadline, or unlimited availability. Hosting/provider budget remains unspecified.
- The developer explicitly leaves the two developers' work split to the team. Architecture guidance should establish shared contracts without allocating their implementation work.
- The developer subsequently clarified that N-tier is a candidate to evaluate, not an accepted design. Explain and discuss major architecture/database options, obtain their agreement, and record each decision before proceeding to dependent design. The engineering map's questions and research findings are not approved architecture or API contracts.
- On 2026-10-31 the developer explicitly chose Clean Architecture within the modular monolith and then accepted the Domain/Application/Infrastructure/API project-reference rules and selective-interface policy. This supersedes earlier architecture preferences and the assistant's three-layer proposal; see [the accepted direction](../adr/0001-clean-architecture.md). They subsequently confirmed [PostgreSQL with EF Core/Npgsql](../adr/0002-postgresql-persistence.md) after the Npgsql explanation, under the zero license-fee constraint. Continue to justify abstractions with actual responsibilities and verification needs.

## Team planning implications

- Establish shared backend/web contracts and review boundaries; leave individual assignments and React ownership to the team.
- Include the Flutter developer in API, authentication, media, and offline-contract design before dependent mobile implementation.
- Include QA in acceptance scenarios, edge cases, test data, and verification planning from the first workflow onward.
- Review shared contracts before splitting implementation work. Build complete workflows in coordinated increments.
- Do not infer delivery dates, full-time availability, or specialist security/operations coverage from the team size or titles.

## Provisional teaching baseline

| Area | Evidence and implication |
| --- | --- |
| C# and ASP.NET Core | Multiple application examples, async operations, controllers, dependency injection, DTOs, and command handlers. Start with an applied request walkthrough; calibrate understanding before assigning a proficiency level. |
| Persistence | EF Core queries, relationship loading, migrations, financial mappings, and concurrency handling are present. Check understanding of transaction boundaries and concurrent writes using concrete scenarios. |
| Business rules and structure | Both API/Business/Data and Domain/Application/Infrastructure structures exist. Use these to explain responsibilities, dependency direction, and the distinction between layers and business modules. |
| Testing | Domain and database-persistence tests exist in Sopmine; API tests also exist in the learning archive. Confirm which tests the developer authored and can extend independently. |
| Delivery | Docker packaging and GitHub Actions configuration exist. The developer confirms that the completed Sopmine project is hosted. Clarify their role in deployment and experience with troubleshooting, backups, and restoration as those topics arise. |
| Frontend and mobile | React for web and Flutter for mobile are confirmed Ostadi Plus choices. Inspected Sopmine frontend code uses vanilla JavaScript; the mechanic project contains Blazor learning guidance. Framework proficiency is not established by this sample. |
| SaaS-specific concerns | Independent experience with tenant isolation, delegated permissions, protected offline content, OAuth/OIDC configuration, durable background work, and production capacity remains unverified. |

## First architecture session

1. Sketch Ostadi Plus's system boundaries within the approved React, Flutter, and ASP.NET Core modular-monolith baseline.
2. Compare business-module boundaries, logical layers, and deployment tiers directly against Ostadi Plus requirements. Treat the developer as familiar with both three-tier and the previously proposed structure; explain project-specific trade-offs.
3. Trace Ostadi Plus's first protected-learning workflow through those boundaries and identify its data, permission, API, mobile, and verification dependencies.
4. Plan the team's shared contracts, workflow responsibilities, and acceptance evidence; teach missing concepts as they arise.
5. Record agreed terminology and consequential decisions through the configured glossary and ADR conventions.

Do not copy an existing project's architecture or dependencies without evaluating the Ostadi Plus requirements.

## Information still needed

- Which parts of each project were independently designed and implemented, course-derived, AI-assisted, or built with others.
- Any React/TypeScript or Flutter experience outside the inspected material.
- Actual hosting/storage budget amount, other provider usage-cost constraints, and operational decision owners when needed by dependent decisions. Paid software/database licenses cannot be funded; hosting/cloud/VPS/storage costs can be considered. Individual development assignments remain outside this guidance scope.
- Demonstrated understanding from the first request walkthrough.
