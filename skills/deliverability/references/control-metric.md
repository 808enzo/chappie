---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Control metric: how to read the provider response index

`SKILL.md` defines the index: its numerator and denominator, the division, reading it over time against
the provider's own median, why it divides, why not inbox placement rate or the delivered share, why
both halves count accepted messages, and how it rises when the work gets worse. This file holds how to
read it.

## The unit: a provider, not a domain

- **Group addresses by provider, not by the domain after the @.** The provider is whoever runs
  the mailbox, and a company domain running on somebody else's mail service belongs to that
  service: read it off the domain's MX record rather than off the address. Skip this and a base
  made of company addresses is cut into hundreds of domain-sized groups, each too small to read,
  while the provider-wide event you are looking for is spread evenly across all of them. Refresh
  the mapping on the same rhythm as the metric, because a company can move mail service without
  telling you, and remember that postmaster tools report only the provider's own consumer domains,
  so the tool covers less of your base than the index does.

## The index on invented numbers

**Take a worked example.** A send is accepted for 100,000 addresses across all providers and 2,000
people click, so the whole send's rate is 2%. Provider A accepted 40,000 and 900 clicked: a rate of
2.25% and an index of 1.13. Provider B accepted 30,000 and 300 clicked: a rate of 1% and an index
of 0.5. If B's median index across recent sends was 0.95, that is an event, it belongs to B, and
the campaign itself performed normally.

## Every class of the denominator

**Read every class of the denominator and who owns it.**

| What happened to the address | In the index | Where it is read |
|---|---|---|
| accepted by the provider | yes | the index itself |
| deferred and still being retried | not yet: it joins the denominator if a retry is accepted and the refusal share if the retries run out | `references/placement-recovery.md`; read the index only once the retry queue for that send has emptied |
| refused permanently | no | the refusal share, `references/placement-recovery.md`; the record is `list-building`'s |
| refused temporarily | no | the refusal share, `references/placement-recovery.md` |
| not sent because the address is unreachable | no, and this is the gap the held back share below closes | `references/placement-recovery.md`, step 8 |
| not sent by a decision of the program | no | `contact-orchestration`, `email-program` |

## What counts as held back

`SKILL.md` says why a narrowed audience lifts the index and names the two numbers read beside it.

- **The share of the base held back for delivery reasons** in the period: addresses the program
  sent nothing to because they were unreachable, suppressed after a complaint, or outside the
  narrowed audience of a warmup, against the addresses it would otherwise have sent to.

## When a send is old enough to read

**Read the index late enough that its denominator has stopped moving.** Acceptance is not final at
the moment of sending: deferrals resolve over the retry window, and asynchronous refusals arrive
after you have already counted a message as accepted. Both land in the denominator, and both arrive
faster than usual during the incidents you are looking for. Read a send no earlier than the
longer of your reading window and your platform's retry ceiling, and recompute rather than compare
two sends read at different ages.
