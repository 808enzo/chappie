---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Changing a program that is already live

This mechanic changes a rule you have already promised to the base, without losing either the
margin or the trust. It exists because there is no cheap way to change your mind about a public
promise, and because most readers of this skill already have a program.

## Entry conditions

- The construction is live: people hold balances, tiers and expectations.
- There is a signal that the construction, rather than its execution, has stopped working:
  redemption share falling while the base grows, margin leaking, a failed launchability check that
  sent the design back, or a change in promotional policy that has emptied the redemption rule.
- You know which part changes, and it is part of the construction: a rate, a boundary, a tier,
  an expiry period, an exclusion list.

## Exit conditions

The new rule is live for the whole base, the members of the old construction are in the new one
with their state intact, the metric that triggered the change has moved, and the forecast written
before the change has been compared with what happened.

## Sequence

**1. Separate construction from execution.** One question: is the mechanic doing what it was
designed to do. If it is, and the outcome is still bad, the design is wrong and the work is here.
If it is not, this is a monitoring problem and belongs to `program-audit-and-ops`. Changing a rule
that is currently misfiring means changing it blind, and you will not be able to attribute what
happens next.

**2. Read what the base is doing now.** Before you change anything: how each tier uses the
currency, which product groups it gets spent on, what balances are sitting on accounts and how
they are distributed. The median balance per tier is the number to write down, because step 5
needs it.

**3. Write the forecast and keep it.** What you expect to happen to margin, to redemption share,
to frequency. Write it before the change and keep it in writing, because without it there is
nothing to compare the result against and any movement gets declared a success. A forecast that
misses is material rather than an error. Check one explanation before the others, because this
construction produces it on its own: the ceiling permits more redemption than people have saved,
so the modeled margin loss comes out worse than the real one. The edge case in
`currency-and-earn-burn.md` gives the test: average actual penetration against the ceiling.

**4. Test on a slice.** A region, a channel, a city, a segment. Three criteria for choosing it: big
enough for the result to be readable, not so big that a failure costs you the year, and with enough
repeat purchase history to measure retention at all. Your largest market fails the second
criterion. Your newest one fails the third.

The length of the test is not a calendar choice. It is the period in which most repeat purchases
in your category happen, so that the test sees the behavior it is meant to change. Shorter and you
are reading noise, longer and you are spending time you do not need to spend.

**5. Decide what happens to the people already in the program.** Three separate questions, and none
of them has a safe default.

- **Status carries over.** Downgrading people during a migration is two changes at once, and the
  anger from the second one gets attributed to the first, which destroys your reading of both.
- **Balances are not zeroed silently.** If the accounting needs a clean start, zeroing is its own
  announced event with a window to spend. Announce that window in advance and make it no shorter
  than a typical interval between purchases in your category. Zeroing is also where compensation
  belongs: grant a starting balance sized near the median balance of the tier, computed in step 2,
  with a shorter life than ordinary currency, so that it gets spent instead of settling on the
  account as a fresh obligation.
- **A promise already made about the future** either runs out its term or is closed with
  compensation sized the same way. That sizing carries over from the case above: what a forward
  promise was worth to the person is not sitting on any account, so the median balance of their
  tier is a stand in, and you say so when you announce it.

**6. Announce it, to exactly the people it applies to.** In advance, with a window. Announcing a
change to the whole base when it is running on a slice creates anger among everyone it does not
reach, so announce a slice through direct channels, to that slice only. When the change rolls out
to everyone, the announcement becomes a broad one.

Announce improvements too, unless the improvement is discoverable at the moment it applies. A
better rate that the customer meets at the till, in the form they are filling in, or in the terms
they read before acting moves behavior without a message. An improvement they could only learn
about from a message you did not send changes nothing, and its whole cost lands on people who were
buying anyway.

**7. Decide the rollout in waves, and what each wave has to be taught.** `loyalty-program-launch`
runs the waves. You decide here that there are waves at all, and that no wave opens before the
people who explain the change to customers have been trained on it. A wave without that training
produces a queue at the till and the explanation that the program is broken, which is the version
customers remember.

**8. Compare with the forecast and write down the gap.** Read two metrics at once: the one that
triggered the change, and margin. Either one alone will mislead you, because redemption share can
be driven to any level you like by giving away more margin.

## Thresholds and timings

| What | Computed from |
|---|---|
| Length of the slice test | the period in which most repeat purchases in your category happen |
| Window to spend before a balance is zeroed | not shorter than a typical interval between purchases |
| Notice before terms get worse | that same window plus the time it takes a message to reach people on every channel |
| Scheduled review interval | published in the program terms in advance, before the first revision |

## Edge cases

- **The change lands in a peak season.** Postpone it. A peak is the worst moment to hand staff a
  rule they are explaining for the first time.
- **Part of the network does not take part.** Franchise and partner locations may decide for
  themselves. Then the rule states where it applies, and that statement is part of the public terms
  rather than an internal detail.
- **The change improves things for one group and worsens them for another.** Treat it as two
  changes and announce it separately by segment. A single "we have updated the program" raises more
  questions than it answers, and the group losing something finds out from the other group.
- **The slice gets rolled back.** Choose the name before you start: a temporary local promotion. A
  rolled back slice that was announced as new rules is your second change of rules this quarter.
- **Closing the program down.** There is no sequence here for it: this library covers launching
  and revising a program, not retiring one. What is certain is that the rule for this
  case goes into the terms before launch, because at the moment of closing you are no longer
  writing that rule, you are executing it.

## Failure modes

**Changed everywhere at once.** There is no part of the base left where the rule did not change, so
there is nothing to read the result against. All that remains is comparison with a previous period,
and that does not separate the season from the effect.

**Announced to everyone, applied to some.** The cheapest way to generate anger for nothing.

**The rule changed with no forecast written.** The metric moved and nobody can say whether it moved
enough. From there, the next change gets decided on impressions.
