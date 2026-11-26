# Integration discovery checklist

Use in the technical discovery call, ideally with someone who owns the systems on the other end. Each row is a question, why it matters, and what a worrying answer sounds like.

## 1. Goal and trigger
| Ask | Why it matters | Red flag |
|---|---|---|
| What business event should cause data to move? | Defines the trigger and the latency you actually need | "Everything, all the time" |
| What breaks for the business if this is an hour late? A day late? | Separates real-time needs from habit | "Real time" with no consequence behind it |

## 2. Systems and data flow
| Ask | Why it matters | Red flag |
|---|---|---|
| Which system is the source of truth for each object? | Prevents two-way sync conflicts | Both systems "own" the record |
| Which direction does data flow, and is any of it two-way? | Two-way multiplies conflict handling and testing | Two-way requested "just in case" |
| Roughly how many records or events per day, and what's the peak? | Drives rate-limit, queueing, and cost decisions | Nobody knows the volume |
| Is there a middle layer today (iPaaS, ESB, ETL tool)? Who runs it? | Decides whether to plug in or build alongside | A tool nobody on the call can describe |

## 3. Interfaces
| Ask | Why it matters | Red flag |
|---|---|---|
| What APIs or events does each side expose? Versioning and deprecation policy? | Predicts breakage and maintenance | No documented API, or screen-scraping |
| Rate limits and quotas on both sides? | A bulk load that works in test can throttle in production | Limits unknown or "unlimited" |
| Webhooks, polling, or bulk files? | Determines architecture and failure handling | A batch window that is already tight |
| Is there a sandbox with realistic data? | You can't test auth, volume, or edge cases without one | Production-only access |

## 4. Identity and access
| Ask | Why it matters | Red flag |
|---|---|---|
| How will users sign in (SAML, OIDC)? Which identity provider? | SSO is often a gating requirement, not a nice-to-have | SSO "required" but the IdP team hasn't been involved |
| How are accounts created and removed (SCIM, manual, HR feed)? | Offboarding gaps are an audit finding | Manual deprovisioning |
| What service accounts or API keys will the integration use, and who rotates them? | Long-lived shared secrets are the usual weak point | A personal account used as the integration identity |
| What is the least-privilege scope the integration needs? | Keeps the security review short | "Admin, to be safe" |

## 5. Data handling
| Ask | Why it matters | Red flag |
|---|---|---|
| What classes of data will flow (PII, financial, health, IP)? | Sets the security and legal review path | Unknown, or discovered late |
| Residency or sovereignty requirements? | May rule out options outright | Raised after the architecture is agreed |
| Retention, deletion, and export obligations? | Needs a design answer, not a policy PDF | No owner for deletion requests |
| Will any data be sent to a third-party model or sub-processor? | Triggers additional review and contract terms | Not yet considered |

## 6. Reliability and operations
| Ask | Why it matters | Red flag |
|---|---|---|
| What should happen when a delivery fails? Retry, queue, alert, drop? | The most under-specified requirement in most projects | "It shouldn't fail" |
| Does the receiver need events in order? Can it tolerate duplicates? | Decides whether you need idempotency keys and sequencing | Ordering required, duplicates intolerable, no key available |
| Who is paged when it breaks, and what do they see? | Unowned alerts mean silent outages | No named owner |
| What does "working" look like on a dashboard? | Gives you a success metric and a support runbook | No monitoring in place |

## 7. Environments and change
| Ask | Why it matters | Red flag |
|---|---|---|
| Dev, test, and production: what exists and who can deploy? | Estimates timeline and dependency risk | A single shared environment |
| Change-freeze windows and release cadence? | Real go-live dates depend on it | Freeze overlaps the target date |

## 8. Security review and procurement path
| Ask | Why it matters | Red flag |
|---|---|---|
| Who reviews new vendors and integrations? How long does it take? | The review is often longer than the build | First contact with Security happens at contract stage |
| Which artifacts will they ask for (questionnaire, architecture diagram, pen test summary, DPA)? | Lets you prepare in parallel | Unknown |
| Is there an approved-vendor list or pre-existing review? | May shorten the path | Starting from scratch with a hard deadline |

## 9. Ownership
| Ask | Why it matters | Red flag |
|---|---|---|
| Who builds it, who runs it, who supports it afterward? | Prevents the "we assumed you would" gap | Three different answers from three people |
| What's the first thing you'd want working in 30 days? | Defines a minimal, provable first slice | A big-bang cutover |

## After the call
Write one page: systems, direction, volume, identity approach, data classes, review path, and **three unresolved questions with owners and dates**. Send it the same day. It becomes the spine of the architecture diagram and the security response.
