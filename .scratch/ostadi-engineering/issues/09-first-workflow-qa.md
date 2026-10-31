# First learning workflow acceptance and verification

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 06

## Prerequisites

- [First learning workflow and shared API contracts](06-first-learning-api-contracts.md)

## Question

What observable acceptance scenarios and verification seams demonstrate that the first complete learning workflow works across React, API, persistence, workers/media, and Flutter?

Define synthetic/approved test data and the happy path plus role/tenant denial, unaccepted relationship, missing/future/expired/revoked grant, unready/failed media, duplicate/retried requests, and supported-device/network failures. Use the agreed contracts to decide appropriate domain, database, API integration, and end-to-end evidence. Specify what must run in CI versus device/environment checks.

Include QA from the start; retain separate qualified security, independent, and teacher/student user-check requirements. Choose tests for meaningful observable risks, without mirroring implementation or inventing product behavior.

Sources: PRD RD-007; Sections 18/21; OP-011/012/014.
