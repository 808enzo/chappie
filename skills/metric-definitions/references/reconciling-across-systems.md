---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Reconciling one metric across two systems

Two systems will disagree about the same metric, sometimes by a wide margin, and the disagreement
is almost never a bug. Each system counts a population it can see, an event it can recognize and
a touch it can attribute, and no two systems see the same three things. The work is not finding
the honest system. It is naming which layer the difference lives in and deciding which number the
company acts on.

## Entry conditions

- Two systems report different values for one metric, and a decision has stopped on it.
- You can extract both numbers for the same period and the same segment.

## Exit conditions

The difference is attributed to a named layer: population, event definition, attribution,
identity, or timing. A system of record is named for this metric. A tolerance band is agreed,
along with what happens when the difference exceeds it, and the reconciliation has an owner and a
cadence.

## Sequence

**1. Freeze the comparison.** One metric, one period, one segment, one extract date. A comparison
made live never converges, because each side is looking at a different slice of time while
talking.

**2. Compare populations before values.** Who got into each denominator. Start here: it is the
cheapest layer to check, and a filter one side applies and the other does not explains a difference
in one line, with no modeling. How often that closes the question, this library has not measured, so
treat it as the first place to look and not as a share of cases.

**3. Compare the event definition.** Order placed against order paid. All opens against unique
opens. A click on any link against a click on the tracked one.

**4. Compare attribution: model, window, time zone.** Web analytics recognizes a device and a
browser rather than a person, so one human buying from a phone and a laptop is two customers;
cookie lifetime cuts histories short; offline purchases are invisible to it entirely. None of
that is a defect. It is what the tool is, and it is why its channel numbers cannot be reconciled
line by line with an order system.

**5. Compare identity and deduplication.** Device identifier against customer identifier, one
person in two profiles, duplicated orders.

**6. Compare when the data lands.** Late orders, returns, overnight exports, a platform and an
order system on different time zones.

**7. Name the system of record for this metric, and write down that the other number is not
wrong.** It measures something else. Different metrics can have different systems of record: the
sending platform owns sends, the order system owns money. Naming one system for everything is how
you get a system of record nobody trusts.

**8. Agree the tolerance and the routine.** What size of difference is normal, who looks, what
happens when it is exceeded. Reconciliation becomes a recurring task with an owner rather than an
investigation someone runs once.

## Thresholds and timings

- **The tolerance band comes from your own data.** Run the comparison for several periods, take
  the spread you observe, and make that the band. A round percentage picked in advance is
  a guess wearing a threshold's clothes.
- **Reconcile on the reporting cycle.** Reconciling more often than you decide anything is
  expensive and changes nothing.
- **Give an investigation a deadline of one cycle, as a starting point.** A difference not
  resolved by the next cycle stops being a difference and becomes background nobody believes,
  which is more expensive than either number being wrong. Where one cycle is shorter than the time
  the late data takes to land (step 6), the deadline is that time instead.

## Edge cases

- **The channel's share of revenue rises while total revenue is flat.** The rise came out of the
  other channels. Whether the channel took business from them or only took credit for it, the
  share cannot say: the attribution method decides the credit, and only a control group
  (`experiments-and-holdouts`) shows whether any business moved. Read a share next to the absolute
  figure, always.
- **Last-click attribution credits a channel for what would have happened anyway.** Someone
  registers on their own, receives a welcome message, clicks it, and buys. Reconciling systems
  cannot settle that, because both systems are attributing rather than measuring cause. Say so
  and hand the question to `experiments-and-holdouts`, which answers it with a control group.
- **The platform changed how it counts.** A step change with no change in the work. Check the
  release notes before building a theory about customer behavior.
- **The sending platform's revenue against the order system's revenue.** The first usually
  counts placed orders, the second fulfilled ones. Unfulfilled orders are the first layer to name,
  because the order system knows each one and so explains its part of the gap exactly. How large
  that part is, measure rather than assume. It does not close the gap on its own: the two systems can also differ on window, attribution and identity, and those
  are checked in steps 4 to 6 before anyone calls the reconciliation done.
- **One of the two systems is the one the executive reads.** The system of record is a decision
  about which number the company acts on, so it has to be made with whoever reads the number, not
  behind them.

## Failure modes

- **The reconciliation happened once.** A quarter later the difference is back, because its cause
  came back.
- **The argument moved to which tool is right.** The tell: both sides are talking about systems
  and neither is talking about denominators.
- **One system of record was named for every metric.** It is right for some of them, and the rest
  quietly drift.
- **The difference was explained by seasonality.** Seasonality does not create a difference
  between two measurements of the same period.
- **Nobody wrote down what was concluded.** The next person repeats the whole investigation, and
  the routine that would have prevented it never gets built.
