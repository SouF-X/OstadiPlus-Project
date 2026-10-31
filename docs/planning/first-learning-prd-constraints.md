# First protected-learning workflow: approved source constraints

Source: [approved Ostadi Plus PRD](../requirements/Ostadi_Plus_MVP_PRD_Phase_24_Approved.docx), checked read-only on 2026-10-31. These are source requirements, not a physical schema or new architecture approval.

## Identity, ownership, and authorization records

- FN-001/002, DT-003, TE-005: a global student identity has a unique phone number and a permanent public StudentGUID/QR distinct from the internal database identifier. Students can connect separately to multiple teachers/centers; those connections do not merge teacher workspaces or financial/discussion contexts.
- FN-013 and DT-002: a course has exactly one owning teacher and belongs to that teacher's workspace. A center's collaboration permissions do not transfer course ownership.
- FN-008/009: connection acceptance is separate from course assignment; an accepted connection may have no assigned courses. Subsequent assignments do not require another student acceptance.
- FN-009/010, DT-004: grants cover the whole course for a course without semesters, or S1, S2, or both for a semester course. Qualifying grants must cover the requested resource/semester. Overlapping authorized grants are permitted; exact duplicate active grants in one authorizing context must be prevented.
- BR-001-004: grant dates use Africa/Casablanca, with an inclusive end date. Past/current/future periods are supported; historical dates do not invent activity or alter recording timestamps.
- Section 12.2 identifies logical grant information: student, teacher, optional center, course, semester scope, academic cycle, dates, status, assigning actor, and associated agreed fee. Physical table/class layout remains an engineering decision (TE-023/OP-010).
- BR-007/008: recording or refunding an external student payment does not automatically create, extend, suspend, or revoke a grant. The agreed financial terms and the payment record are distinct from access authorization.

## Content, publication, and media

- FN-013/014: the course model is immutable and is either S1/S2 or without semesters. Teachers manage ordered chapters and lessons. A lesson supports zero or one primary video and multiple PDFs; publication has no minimum resource count. No separate Unit concept is specified; student classes/groups are outside MVP (Section 6.4).
- FN-015/016: the owning teacher explicitly publishes. Edits to a published lesson remain drafts while students see the previous published version until explicit republication. There is no administrator publication approval; assistants have no content-management rights.
- FN-018/019, SEC-018, INT-014: media progresses through uploading, processing, ready, or rejected states. Integrity/format/malware validation precedes availability. Scanner failure keeps files quarantined. Media readiness and teacher publication are separate gates.
- UI-026 and Section 12.2: resource download settings, processing/publication state, retention state, and media version are distinct concerns. The logical asset record links the lesson, asset type, storage reference, version, and these states/settings; this does not prescribe one physical table.
- FN-017: archival blocks new assignments while existing valid grants finish their periods. Broken lessons can be withdrawn; permanent deletion is restricted to unused drafts without dependent history.

## Access gates that a grant alone does not settle

- FN-005: one active server-authorized student phone; a new phone invalidates the earlier online session. Previously issued offline permissions have their separately approved disconnected-device limits.
- SB-021-025: teacher SaaS nonpayment can restrict the workspace and dependent student online access after the approved seven-calendar-day grace period. This differs from a student's unpaid external financial record. Restoration still requires all other access conditions.
- SB-029-031: pending teacher cancellation blocks new assignments/renewals/extensions while existing grants can continue to expiry unless explicitly revoked.
- SEC-029-032: suspending an individual teacher account does not itself remove otherwise-valid student access; a justified workspace-wide security block is a separate measure.
- FN-044/BR-037: ending center collaboration removes its management/historical-financial access but does not itself cancel already issued student grants.
- DT-024: lessons with deleted files return as drafts for review/republication; replacement uploads do not renew grants or erase archived results.

## Refinement still needed

Use these rules to design entity/reference boundaries, revision/publication representation, transactions, duplicate protection, actor/tenant scope, and cross-module contracts. Full schema, exact enums, concurrency mechanisms, and the complete connection/disconnection state machine are not determined by this note. The first engineering milestone remains RD-007; full MVP acceptance is still required before pilot.
