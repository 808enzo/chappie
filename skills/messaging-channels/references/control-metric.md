---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Control metric: how to read the reached share

`SKILL.md` defines the reached share: who counts as addressed and as reached, the two populations kept out,
the rule that sorts the remainder into classes, the period and the cut, why people and not sends, why no
receipt stays out, why not the neighbors' metrics, how the share rises without better work, and the pool
kept out beside it. This file holds how to read it.

## The classes of the remainder

| Class | What it says | Where it goes |
|---|---|---|
| held | the send stopped on the state of your own channel: no approved template for the class, a template paused or disabled, the portfolio's limit, the person's marketing limit (code 131049), the origin paused after a drop. The reason sets the class, whether your gate caught it or the platform refused the send | the standing mechanic, steps 4 to 6; the send mechanic, steps 4, 7 and 9 |
| refused | the gatekeeper stopped it for the number or for the traffic: unregistered or filtered traffic, blocked by the person, an invalid or deactivated number, no account on the platform | the standing mechanic, steps 2 and 7; the send mechanic, step 3. A loss event for `contact-orchestration` only when the refusal is a property of the number (blocked, invalid, deactivated, no account); unregistered or filtered traffic is a property of the origin and never a loss event |
| expired | accepted, not delivered before the expiry: the handset was off, the platform dropped it at its time-to-live | the send mechanic, step 6 |
| no receipt | the route returns no delivery receipt, so the outcome is unknown | out of both halves of the share; its share of the addressed is read beside the metric as a property of the route |

## When a period's reading closes

- **The reading waits** until the longest expiry among the period's sends has passed.

## What moves it

**What moves it.** Up: templates approved before the campaign and kept alive, the limit raised by the
ramp, categories that match the content, numbers cleaned daily.
Down: a paused template, unregistered traffic, an import full of dead numbers, an expiry shorter than
the time a phone stays off.

## Read beside it

**Read beside it, and promote none of them.**

- **Cost per reached person**, per origin and class: what the gatekeeper billed for the period's
  sends divided by the people reached. It catches segment overflow, a recategorized template, SMS
  billed on submission and never delivered, and repeated attempts.
- **Stop and block events per thousand delivered**, per origin and template: the person's verdict,
  which the gatekeeper turns into standing. It feeds the loss events of `contact-orchestration`.
- **The standing register** (`references/origin-and-standing.md`, step 5): a state, not a metric.
- **The distribution lag of a STOP across systems** (`references/keywords-and-replies.md`, step 8).

## What it cannot see

It does not see the person's verdict or the price: those are the two lines above.
