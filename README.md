# Integration and Security Reference for Solution Architects

Vendor-neutral working notes for the part of a technical sale that decides whether a deal closes: **how this connects to their systems, and whether it passes their security review.**

**Author:** Alberto Escalante · [LinkedIn](https://www.linkedin.com/in/albertoantonioescalante/)
Generic by design. No vendor, employer, or customer material, and nothing here describes any specific product's security posture.

## What's in here
| File | Use it when |
|---|---|
| [`discovery/integration-discovery-checklist.md`](discovery/integration-discovery-checklist.md) | You're scoping an integration and need the questions that surface cost and risk early |
| [`security/questionnaire-answer-guide.md`](security/questionnaire-answer-guide.md) | A security questionnaire lands and you need answers that are accurate, scoped, and fast |
| [`architecture/integration-patterns.md`](architecture/integration-patterns.md) | You're choosing between webhooks, polling, streaming, and batch, and need a reliability checklist |

A working example of the webhook pattern, with HMAC signing and tests: [call-coaching-webhook-demo](https://github.com/aescalante84/call-coaching-webhook-demo).

## Principles behind the three documents
1. **Ask about failure before success.** The happy path always works in a demo. Cost and risk live in retries, ordering, ownership, and what happens at 3 a.m.
2. **Answer the question that was asked, then stop.** Scope every security answer: what it covers, what it doesn't, and where the evidence is.
3. **Never claim what you haven't confirmed.** A wrong answer in a questionnaire is a contractual statement. "I'll confirm with Security and revert by Friday" is a good answer.
4. **Write down who owns what.** Most integrations stall on an unowned step, not a technical one.
