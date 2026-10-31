# Protected media and offline lifecycle

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 02, 04

## Prerequisites

- [Business modules and data ownership](02-business-modules-and-data.md)
- [Identity, authorization, and tenant isolation](04-identity-access-and-isolation.md)

## Question

What state transitions and security boundaries govern upload, scanning, publication, protected delivery, permitted offline use, and replacement?

Define multipart upload and validation, media readiness/publication, S3/CloudFront signed access, worker/outbox responsibilities, failure/retry behavior, supported device/media test profiles, offline encryption/key/expiry/synchronization behavior, and how access changes affect connected and disconnected devices. Preserve the PRD's actual offline limits; immediate disconnected revocation must not be promised.

State first-workflow requirements for a protected video or PDF, and the dependencies required before later offline implementation. Preserve exclusions for HLS/transcoding and studio DRM. Identify provider evidence needed by the provider decision.

Sources: PRD TE-007/022/023 and OP-012; RD-007.

Consult [first-learning source constraints](../../../docs/planning/first-learning-prd-constraints.md) for course/lesson publication, zero/one primary video and multiple PDFs, exact media lifecycle names, scanner-failure quarantine, and preservation of the prior published lesson while edits remain drafts. Publication has no minimum resource count; the protected-media milestone nevertheless needs an eligible video or PDF fixture.
