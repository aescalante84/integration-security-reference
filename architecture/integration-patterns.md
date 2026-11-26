# Choosing an integration pattern

## The five common patterns
| Pattern | Use it when | Watch for |
|---|---|---|
| **Webhook (push)** | An event on one side should trigger action on the other within seconds | The receiver must be reachable, verify signatures, and tolerate duplicates and retries |
| **Polling (pull)** | The source has no push mechanism, or the receiver can't expose an endpoint | Wasted calls, added latency, rate limits, and missed changes between polls |
| **Event streaming** | High volume, multiple consumers, or ordered replay is needed | Operational weight: brokers, schemas, consumer lag. Overkill for small flows |
| **Batch / file (ETL)** | Latency of hours is fine and volumes are large | Failure at 3 a.m. with a partial load; how do you rerun safely? |
| **iPaaS / middleware** | The customer already runs it and owns the skill | Hidden cost in connector licensing; who maintains flows after the project |

**Default to the simplest pattern that meets the real latency requirement.** Ask what a one-hour delay actually costs before designing for seconds.

## Reliability checklist (any push-based pattern)
- [ ] **Authenticate the sender.** Signature (for example HMAC over the raw body) or mutual TLS. Compare signatures in constant time.
- [ ] **Stop replays.** Include a timestamp in the signed payload and reject old ones.
- [ ] **Be idempotent.** Every event carries a unique ID. Processing the same ID twice has the same effect as once.
- [ ] **Acknowledge fast, process later.** Return a quick success and hand off to a queue, so a slow downstream never causes sender retries.
- [ ] **Retry with backoff and jitter.** Cap attempts, then dead-letter. A dead-letter store with an owner and an alert is part of the design.
- [ ] **Decide on ordering.** If order matters, carry a sequence or version number. If it doesn't, say so explicitly.
- [ ] **Isolate failures.** A broken callback must not fail the primary operation. Report it and move on.
- [ ] **Make it observable.** Count received, processed, failed, retried, and dead-lettered. Alert on age of the oldest unprocessed item.
- [ ] **Version the contract.** Additive changes only inside a version; announce breaking changes with a sunset date.

## Questions to settle before building
1. What is the maximum acceptable delay, and who decided?
2. What happens to an event that can't be delivered after all retries?
3. How will anyone know it stopped working?
4. Who owns the on-call for this?

## Worked example
[`call-coaching-webhook-demo`](https://github.com/aescalante84/call-coaching-webhook-demo) implements signed inbound and outbound webhooks, isolates callback failure from scoring, and tests the auth paths. Its README lists what it deliberately omits (queue, retries, replay protection), which is the checklist above applied honestly.
