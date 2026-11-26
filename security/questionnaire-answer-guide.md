# Security questionnaire answer guide

How to answer security questionnaires so the answers are accurate, scoped, and quick to produce. This is a method, not a source of facts: **every answer must come from your own product's verified documentation or your Security team.** Bracketed items are placeholders to fill from those sources.

## The method
1. **Answer the exact question.** If asked about encryption at rest, don't volunteer your whole security program.
2. **Say what it covers, and what it doesn't.** Scope is where mismatches hide.
3. **Point to evidence.** A report, a policy section, a documentation page. Not "we take security seriously."
4. **Never guess.** If you can't confirm, write: "To be confirmed with [owner]; response by [date]." Then follow through.
5. **Have Security sign off** before submission. Questionnaire answers can become contractual representations.
6. **Keep an answer library.** Reuse approved wording, and date it so stale answers get retired.

## Weak versus strong, by example
| Pattern | Weak answer | Strong answer shape |
|---|---|---|
| Overclaiming | "Fully compliant with all standards." | "[Standard] certified/attested as of [date], scope: [systems]. Report available under NDA." |
| Vague | "Data is encrypted." | "Data at rest uses [algorithm]; in transit uses [protocol/version]. Key management: [approach]. Scope: [production data stores]." |
| Dodging a gap | "N/A" | "Not currently supported. Planned: [yes/no, date if committed]. Compensating control: [control]." |
| Roadmap as fact | "We support SCIM." (it's planned) | "SCIM provisioning is on the roadmap and not yet generally available. Today: [manual or SSO-based JIT provisioning]." |

## Common questions, and how to structure the answer
For each, fill the brackets from verified sources.

**1. How is customer data encrypted at rest and in transit?**
State the algorithms and protocol versions, the scope (databases, backups, object storage), and who manages keys. Say whether customer-managed keys are offered, and if not, say so.

**2. Do you support SSO and automated user provisioning?**
Name the protocols supported (SAML 2.0, OIDC), whether SCIM is available, and which plans include them. Distinguish "supported" from "generally available."

**3. What audit logs are available, and how long are they retained?**
Which events are logged, whether customers can export them, retention period, and whether logs are tamper-evident.

**4. Where is customer data stored and processed? Can we choose the region?**
List regions, whether the customer can select one, and whether support access or backups cross regions.

**5. Who are your sub-processors?**
Link the current list and the change-notification process. Don't paste a list from memory.

**6. What certifications or audits do you hold?**
Name each, its date and scope, and whether the full report is shareable under NDA. If one is in progress, say "in progress," with the expected date only if it is committed.

**7. How do you handle a security incident and customer notification?**
State the notification commitment and timeframe from your contract or policy, and the contact path. Never quote a number you haven't verified.

**8. How is access to customer data controlled internally?**
Least privilege, who can access production data, approval and logging of that access, and background checks if applicable.

**9. How do you handle data deletion and retention at contract end?**
Deletion timeline, what happens to backups, and how deletion is confirmed to the customer.

**10. Is customer data used to train AI models?**
Answer directly, in one sentence, then give detail. State what is and is not used, under which plans, and whether customers can opt out. This question is now common, and vague answers lose trust.

**11. What are your backup, recovery, and availability commitments (RPO, RTO, uptime)?**
Give contractual SLAs only, not internal targets. Separate "design target" from "contractual commitment."

**12. When was your last penetration test, and can we see the summary?**
Date, who performed it (internal or third party), scope, and whether a summary is shareable under NDA. Don't claim findings were "all resolved" unless you've confirmed it.

## Before you submit: a short checklist
- [ ] Every factual claim traced to a document or named owner
- [ ] Roadmap items labelled as such, with no dates unless committed
- [ ] Scope stated for each control
- [ ] Security (or the equivalent owner) has reviewed
- [ ] Answers saved to the library with a review date
