# Provider integration, costs, and processing prerequisites

Parent: [Ostadi Plus engineering decision map](../map.md)
Type: grilling
Label: wayfinder:grilling
Status: open
Blocked by: 04, 05

## Prerequisites

- [Identity, authorization, and tenant isolation](04-identity-access-and-isolation.md)
- [Protected media and offline lifecycle](05-media-and-offline-contracts.md)

## Question

Which SMS, email, push, scanning, monitoring, and related integration choices can be accepted, on what evidence and budget, before their dependent activities?

Identify required provider capabilities from the identity and media decisions, compare actual shortlisted options using primary-source research tickets when needed, and agree credentials/quotas, failure behavior, cost assumptions/alerts, and decision gates. The developer requires zero software/database license fees and can consider VPS/cloud hosting and storage costs, with no amount approved. Other usage charges, including SMS/email/media delivery, remain to be clarified; do not assume they are approved or free. FCM remains unselected; avoid inventing backup SMS/email providers.

Track qualified privacy/CNDP/minors/processing-transfer review and purpose-specific record/financial-document decisions before the activities they govern. Preserve the approved media-only 24-month policy and provisional nature of region placement. Record decision authority and actual owner only when supplied; developer work allocation remains the team's choice.

Sources: PRD OP-002/005-008/014, TE-002/019.
