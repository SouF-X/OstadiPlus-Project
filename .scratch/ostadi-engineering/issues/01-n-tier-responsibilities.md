# Clean Architecture responsibilities and dependency rules

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: resolved
Blocked by: none

## Question

Given the accepted Clean Architecture direction, what concrete responsibilities, project references, DTO boundaries, and integration contracts should the developer agree before solution scaffolding?

The architecture family is already accepted in ADR 0001. Work the remaining concrete boundaries with the developer, preserving the PRD's presentation, application, domain, and infrastructure responsibilities inside the modular monolith. Present the remaining recommendations and wait for agreement; surface proposed departures from the baseline explicitly.

Agree responsibility and allowed-reference diagrams, business-rule placement, persistence boundaries, DTO/domain separation, dependency injection/composition, and the criteria for choosing projects versus folders. Explain request flow and source-code dependencies separately from deployment. Evaluate the alternatives against Ostadi Plus requirements; the developer knows both three-tier and the previously proposed structure and asks to stop using Sopmine as the reference or rationale.

Clean Architecture is accepted. Exact project names, dependency rules, repository abstractions, CQRS/MediatR use, and deployment boundaries remain open. Record rationale before proposing the solution skeleton. Earlier alternatives and recommendations below are discussion history, superseded by the explicit architecture choice.

Sources: PRD Section 20, TE-003/005/008/023; map Notes.

## Comments

2026-10-30: The developer clarified that architecture and database choices must be evaluated and agreed together before proceeding to their dependent design. This ticket is claimed for that conversation; no architecture answer is recorded yet.

### Architecture proposal for discussion — 2026-10-30

Recommend a layered ASP.NET Core modular monolith, keeping React and Flutter as clients of the shared API. Separate API/presentation, application workflows, domain rules, and infrastructure responsibilities, consistent with the PRD. Group business capabilities into internal modules; module boundaries and physical project layout remain to be designed.

The business core should avoid dependencies on EF Core, storage SDKs, and provider-specific implementations. Infrastructure implements the required integration contracts. Logical code layers do not each require a separately deployed service; API and worker hosting will be discussed separately.

The intended rationale is isolating access, billing, and content rules from workflow orchestration and integration details. Familiarity with another project is withdrawn as an architecture justification. Compared with a conventional Business layer directly depending on Data implementation, inward dependencies can help isolate business behavior, but a three-layer design can also use interfaces and dependency inversion. Four separate projects have not been justified by a concrete requirement. Extra abstractions should be justified by actual use cases. Independently deployed business services remain outside the approved PRD baseline.

Primary-source context: [Microsoft .NET application architecture](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures) distinguishes logical layering, traditional data dependencies, dependency inversion, and monolithic deployment; [Microsoft N-tier architecture](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/n-tier) distinguishes logical layers from physical tiers. The recommendation for this team is a project-specific judgment, not a claim that one structure is universally best.

Status of proposal: awaiting the developer's response. The earlier motivation question need not block progress; the existing requirements and baseline suffice to present this recommendation. No architecture resolution or database selection is recorded.

### Three-tier comparison requested — 2026-10-30

The developer explicitly confirms knowing both structures and requests a requirements-based explanation of why three-tier was not proposed. Three-tier deployment, three-layer code organization, and internal business modularity are different design dimensions. Three broad code layers can retain the PRD responsibilities: API/presentation; Business containing application workflows and domain rules; Infrastructure containing persistence and external integrations. Separate responsibilities need not mean four projects. Assess the dependency rules and test seams before selecting physical project count. This is an alternative for discussion, not a resolved architecture decision.

### Current recommendation and testing trade-offs — 2026-10-31

The developer asks for a recommendation given the team's experience, challenges unnecessary Clean Architecture interfaces, expects one database, and reasonably wants to test a layered design. Recommend a simple layered modular monolith using API, Business, and Data/Infrastructure responsibilities. Preserve separate application-workflow and domain-rule responsibilities within Business, plus internal business modules; this does not prescribe three physical deployment tiers or settle every project reference. The recommendation remains pending agreement.

Clean Architecture's useful distinction is dependency direction and isolating the business core, not an interface for every class or merely hypothetical database replacement. Its benefits can exist even with one permanent database. However, a layered design can use plain business-rule types, selective interfaces, and meaningful integration tests without adopting a large template or generic repository/handler patterns by default. Explicitly choose any infrastructure coupling and its test consequences when defining project references; do not accidentally introduce circular project dependencies.

Proposed tests: pure rule tests for access dates and financial calculations; integration tests against an isolated instance of the actual chosen database engine for EF queries, tenant/RLS enforcement, constraints, transactions, and concurrency; API/workflow tests for actor/access behavior; and subsequent real-device/media checks for offline guarantees. An interface is justified where it supports a concrete boundary or needed failure simulation, such as preventing real SMS delivery during retry/error tests. Test doubles do not replace database isolation or device evidence.

Current primary sources: [Microsoft's architecture guidance](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures) explains dependency inversion and logical versus physical boundaries; [EF Core testing strategy](https://learn.microsoft.com/en-us/ef/core/testing/choosing-a-testing-strategy) recommends coverage against the actual database system and describes the additional implementation/maintenance cost of repository-based test doubles. Actual database system here means an isolated test database, not live production data.

Next exchange: ask whether to adopt this layered-modular approach with selective abstractions as the architecture direction. Keep the ticket claimed, without an Answer or resolution, until agreement and the relevant dependency rules have been worked through.

### Architecture direction accepted — 2026-10-31

The developer explicitly stated: "we will use clean architecture". This selects Clean Architecture within the approved modular monolith and supersedes the earlier three-layer recommendation. Recorded in [Use Clean Architecture inside the modular monolith](../../../docs/adr/0001-clean-architecture.md).

Keep this ticket claimed while agreeing the remaining concrete project/dependency rules, composition boundaries, DTO/domain placement, and necessary integration contracts. The architecture family is accepted; reopening the N-tier-versus-Clean comparison is no longer needed. Do not infer approval of CQRS/MediatR, generic repositories, exact project layout, or a database selection from the architecture choice. Next, work through the concrete dependency rules, then proceed to the database discussion in the requested order.

### Concrete boundary proposal — awaiting agreement

Recommend four projects: OstadiPlus.Domain (entities, value objects, domain rules; no dependencies on the other application projects); OstadiPlus.Application (use cases, transport-independent input/output types, and narrow integration contracts; references Domain); OstadiPlus.Infrastructure (EF Core mappings/context/migrations, persistence and provider implementations; references Application and Domain); OstadiPlus.Api (HTTP endpoints, transport contracts, middleware, composition root; references Application plus Infrastructure for dependency-injection registration only).

These arrows describe source-code references, not request flow or four separately deployed services. API endpoint code calls Application behavior, not concrete infrastructure implementations. Domain/Application avoid EF Core, ASP.NET request types, and storage/provider SDKs. API transport contracts stay in Api; use-case types stay in Application; domain entities are not the public API contract. The future worker host uses the same Application and Infrastructure boundaries; its hosting details and internal business-module layout remain separate decisions.

Recommend narrow interfaces for persistence/integration capabilities actually required by use cases. Concrete internal services and pure rules do not each require matching interfaces. Generic repositories, MediatR, separate CQRS dispatch, and extra architectural packages need their own concrete justification and are not implied by this proposal. This separates project structure from pattern/library selection.

User review round: agree the four responsibilities/project-reference rules, and agree the selective-interface policy. No Answer or ticket resolution until the developer responds; this is a proposed project shape, not generated application code.

## Answer

Resolved on 2026-10-31. The developer answered "yes and yes" to the concrete project/reference proposal and the selective-interface policy. Clean Architecture within the modular monolith was already selected; this completes the shared project-boundary decision.

- OstadiPlus.Domain contains entities, value objects, and domain rules; it references no other application project.
- OstadiPlus.Application contains use cases, transport-independent input/output types, and the narrow persistence/integration contracts those use cases need; it references Domain.
- OstadiPlus.Infrastructure contains EF Core context/mappings/migrations and persistence/provider implementations; it references Application and Domain.
- OstadiPlus.Api contains HTTP endpoints, transport contracts, middleware, and the composition root; it references Application and Infrastructure, with concrete Infrastructure usage limited to dependency registration at startup. Endpoints call Application behavior.
- Domain/Application remain independent of EF Core, ASP.NET HTTP types, and provider SDKs. Domain entities are not the public API contract. API transport contracts stay in Api; use-case input/output types stay in Application.
- Interfaces are justified by actual capabilities and boundaries. Internal services and pure business-rule classes may remain concrete. Generic repositories, MediatR, CQRS dispatch, and additional architectural packages are not automatically selected.

These are code/project boundaries. Business-module layout, the eventual worker host, physical deployment, and the database engine/edition remain separate decisions. See [the accepted architecture record](../../../docs/adr/0001-clean-architecture.md); proceed next to [Evaluate and agree the database choice](13-database-selection.md).
