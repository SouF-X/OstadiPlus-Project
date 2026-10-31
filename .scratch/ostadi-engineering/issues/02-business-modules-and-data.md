# Business modules and data ownership

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: claimed
Blocked by: none

## Question

What business-module boundaries, data ownership, and cross-module rules preserve the approved workflows within the layered monolith?

Cover identity, relationships/access, content, media/offline, assessments/discussions, student financial records, teacher billing, and operations. Distinguish module ownership of data from assignment of developers. Define tenant/actor scope, shared identifiers, transaction boundaries, concurrency/idempotency, module interfaces, and where outbox events are justified. Establish enough model detail for the first learning workflow and a method for refining later workflows.

Keep an accepted teacher-student relationship, a dated course-access grant, and a recorded external student payment distinct. Assistants have no content, quiz, Q&A, or learning-progress management authority. Capture domain terms in the glossary as they are actually resolved.

Sources: PRD TE-003/005/008/023; RD-007; developer baseline.

## Comments

### Proposed business boundaries — awaiting agreement

The architecture and database decisions are resolved. Start this conversation with eight logical business areas, preserving the PRD responsibilities: Identity and organizations (accounts, roles, organizational memberships); Relationships and access (relationship acceptance and dated course-access grants); Content (course structure, lesson metadata, publication); Media and offline (asset upload/scanning/readiness, protected delivery, offline lifecycle); Learning (quizzes/attempts, progress, Q&A/discussions, learning history); Student finances (records of externally handled student payments and related balances/documents); Teacher billing (the teacher's Ostadi Plus subscription, usage/invoices/exports); Operations (administration, audit/support workflows).

These are proposed responsibility groupings across the accepted Clean Architecture projects, not new services or one project/database per module. Exact organization/center/delegation boundaries, entity names, tenant scope, and cross-module workflows need further review. Required academic reset and lifecycle behavior remains in scope even when it spans areas.

Recommend that each module owns its business rules and mutations of its records; other modules request changes through explicit application contracts rather than modifying its tables directly. Shared persistence does not imply unrestricted cross-module writes. Reporting and cross-module read projections must be reviewed separately; no blanket ban on joins or forced event bus is proposed.

For the first learning workflow, distinguish Content publication, Media readiness/delivery, and Relationships/access authorization. A relationship, a course grant, and an external-payment record remain separate approved concepts. Center/assistant permissions remain the approved limited permissions and must be retained when refining these boundaries.

Review round: agree or revise the eight responsibility groupings, and agree or revise module-owned writes/application-contract coordination. Do not resolve this ticket from those answers alone: tenant/actor scope, first-workflow data boundaries, transactions, concurrency/idempotency, and cross-module contracts remain to be worked through incrementally.

### Recommendation rationale requested by the developer

The developer asks whether these choices are recommended given the PRD and team, without yet accepting them. Recommend both as a provisional responsibility map and an ownership rule: distinguish student financial records from access authorization and teacher subscription billing; distinguish lesson/course metadata from media asset readiness/delivery; and keep assessment/progress/discussion concerns together initially, refining only when actual workflows justify it. These distinctions protect approved behavior and give each change an understandable home.

Keep implementation proportional: feature folders within the four agreed Clean Architecture projects, direct in-process application coordination where appropriate, and a shared PostgreSQL database as the initial topology proposal. Explicit ownership does not require a project, DbContext, database, service, or bespoke framework per module. Use durable outbox/job mechanisms where the PRD requires reliable asynchronous work. Review cross-module reads/projections and transactional workflows case by case. Add no abstraction merely to make module calls appear distributed.

The trade-off is maintaining explicit boundaries and coordinating multi-module transactions. Eight names are an initial whole-MVP responsibility map, not a requirement to build all eight areas before the first workflow. Implement the identity/access/content/media path first while retaining full-MVP launch gates. The developer's team description informs explanation and implementation simplicity; code inspection does not establish a verified seniority level or production security capability.

The two earlier grouping/ownership questions remain awaiting agreement. This rationale is a recommendation, not an Answer or acceptance on the user's behalf.

### Initial grouping and ownership accepted — 2026-10-31

The developer replied "ok good" to the recommendation and the question asking to accept both proposals on the stated lightweight basis. Record the eight initial areas, feature grouping within the four Clean Architecture projects, shared PostgreSQL starting point, and module-owned changes/Application coordination as accepted in [Keep business ownership explicit inside the monolith](../../../docs/adr/0003-module-ownership.md).

This acceptance does not finish this ticket's data/transaction design. Keep Status: claimed while tracing the protected-learning workflow, checking its model against the PRD, and agreeing the first entities/relationships, owner/actor scope, and transaction/failure boundaries. Later module refinements remain allowed without changing approved product behavior. Next conversation: propose a source-grounded first-workflow model and discuss engineering boundaries rather than asking the developer to restate settled PRD rules.

### First-workflow source check and representation proposal

Read [approved first-learning constraints](../../../docs/planning/first-learning-prd-constraints.md) and the [domain glossary](../../../GLOSSARY.md). The source fixes teacher-owned courses, ordered chapters/lessons, zero/one primary video plus multiple PDFs, global student identity, accepted connections separate from course/semester/cycle/date-scoped grants, published-versus-draft visibility, and independent media readiness. No Unit or student class/group entity should be invented for this MVP.

Propose distinct Connection and CourseAccessGrant entities/records linked to the same student/teacher context, retaining optional center context on grants rather than duplicating the student identity per teacher. Propose separate lesson content/revision data and lesson-asset/media-version data so file processing and draft editing cannot overwrite the currently published student view. Immutable lesson revisions with an explicit published-revision reference are a candidate representation; the source requires the visibility behavior, not this particular schema.

The next review round asks whether to use separate connection/grant records and whether to use versioned lesson revisions plus separately tracked media versions. Exact revision/asset reference cardinalities, transaction boundaries, duplicate-active-grant constraints, concurrency safeguards, and publication/access races remain to be designed after that representation choice. Do not treat teacher billing restrictions as the same rule as an unpaid student financial record.

### Planning paused — 2026-10-31

The developer requested a simpler explanation, then asked to stop planning and publish the project to GitHub. Neither representation proposal above has been accepted. Keep Status: claimed. Resume with the separate Connection/Course-access grant question, one choice at a time; see the [pause checkpoint](../../../docs/planning/checkpoint.md). GitHub publication is project preservation, not resolution of this decision.
