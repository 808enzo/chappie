---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Moving demand between the peak and the trough

The unit here is **the shift**: a quantity of demand deliberately moved from one period to
another, with a direction, an instrument and a price.

This is the part of the work that is the calendar's alone. The lever is not what an offer costs,
it is **when demand lands**. What the instrument costs is `offer-design`'s; whether it should
arrive in March or in June is decided here, and the two are settled in that order.

## Entry conditions

The shape of the year is computed and the register exists (`seasonal-shape.md`). You know what
constrains the peak: capacity or demand. The purchase cycle is known, because the redemption
window is placed against the shoulder and the shoulder is measured in it.

## Exit conditions

Named: the constraint, the direction and why that one, the instrument, the redemption window, the
audience of the shift, what the shift costs and what makes it worth paying, and the pair of
periods the result will be read on.

## Steps

**1. Name the constraint before choosing a direction.** This is the step that decides whether any
of the rest applies.

| What is wrong | Direction |
|---|---|
| The peak is capacity bound: demand arrives and is turned away | move demand out of the peak, forward or backward, or extend the peak |
| The peak has room, the trough has too little revenue, and the trough responds to spending | bring an additional purchase into the trough; relocating one the peak would have served is the first failure mode below |
| The trough does not respond to spending | a possible answer is to do nothing and spend less |

The second row is the one that goes wrong. With room at the peak, moving a purchase out of it
loses a purchase the peak would have served at full price, so the only instrument worth paying for
is one whose trough purchase would not have happened at all, and only the pair reading in step 7
tells the two apart. The third row is a real answer and not a shrug, and it rests on a test rather
than on how flat the trough looks: a holdout in the trough shows whether spending there moves
anything. Where it does not, the cost per order climbs while revenue does not; hold the base with
what does not cost margin and stop paying for demand that is not there.

**2. Three directions, each with the rule that separates it from a plain discount.**

| Direction | Instrument | The rule without which it is only a discount |
|---|---|---|
| **Forward**: a peak purchase made earlier, in the trough before the peak | pre-order, booking, pre-sale | Pull forward **only when the peak is capacity bound**. If the peak has room, you paid a discount for a purchase that was already coming, and moved it to a cheaper price. |
| **Backward**: a purchase moved out of the peak, or an extra one added, in the trough after it | a balance earned at the peak but spendable only in the trough; a coupon dated into it | The redemption window opens **after the peak's shoulder**. Opened inside the window, it is redeemed during the peak; opened inside the shoulder, it lands in the weeks the peak's own verdict is read on and fills the gap that shows pull forward. Either way the instrument was a discount on demand you already had. With room at the peak, only the added purchase pays. |
| **Extension**: demand moved from the peak's edge into the weeks after it | the later slot offered at a lower price to whoever is choosing a date | Offered **at the moment of choosing**, and only to people trying to get into a span that is already full. Offered afterwards it reaches people who already chose. |

The forward rule is easy to break, because pulling demand forward is easy to sell internally: the
revenue arrives sooner and the quarter looks better. It only creates anything
when the peak was turning people away, and the vacated slot then has to be filled at full price
for the shift to have paid.

**3. Place the redemption window so it cannot land in the peak or its shoulder.** It opens after
the shoulder and closes before the next warm-up. Where the next window sits too close for both,
there is no room for a backward shift between them: the register opens the gap or the shift is
dropped. Issue the instrument during the peak, while the person is already
transacting, and name the redemption window in the same message. An instrument whose dates are
announced later is redeemed by whoever happens to read the second message, which is not a
population you chose.

**4. Keep the shift targeted. Never public.** A public reduction reaches everybody, including
everybody who would have bought at full price, and it cannot be measured the way the rest of this
library measures things: there is no group that did not get it, so there is nothing to compare
against. A targeted instrument goes to a segment you named, and it can be withdrawn next cycle
without breaking a public promise.

The cut is on responsiveness rather than on value: somebody who bought inside the last purchase
cycle without a promotion does not receive the shift. They are the people whose purchase you
would be buying back. An instrument issued at checkout reads that history before the order being
placed: the purchase in progress is always a recent one without a promotion, and counting it would
exclude every full-price buyer at the peak.

**5. Hold the trough with what costs no margin first.** An ordered ladder, and the order is the
content of the step: assortment and content that do not touch price, then the targeted instrument
that spends margin, then the public one. The public reduction is last, and only if the first two
were tried, because it is the only rung you cannot take back quietly. It is also no longer a
shift, since step 4 keeps shifts targeted. A public reduction in the trough is a window: it goes
into the register, passes the admission test, and counts against the promotional share of the
year like any other.

**6. Put the work the peak cannot carry into the trough.** Base hygiene (`list-building`,
`deliverability`), flow rework (`program-audit-and-ops`, `triggered-messages`), and tests
(`experiments-and-holdouts`) all belong in the trough, and the freeze window in `peak-run.md` is
what keeps them out of the peak.

What belongs here is the scheduling rule: these are rows in the register with dates and owners,
not things done when there is time. And one edge that is easy to miss: **a test run in the trough
answers a question about the trough.** The population and the intent are both different at a
peak, so a subject line or an offer that won in the trough has not been shown to win at the peak.

**7. Read the shift on the pair of periods, never on one.** The metric is peak plus trough. A
shift that lifted the trough and cost more in the peak is a loss recorded as a win, because the
trough has its own report and the peak's decline has many other candidate explanations.

## Thresholds and timings

| Quantity | Value |
|---|---|
| Redemption window opens | after the peak's shoulder |
| Redemption window closes | before the next warm-up |
| Instrument issued | inside the peak, while the person is transacting |
| Backward instrument prepared | before the peak opens, since it is issued inside it |
| Rest of the trough ladder prepared | while the peak is running, while revenue is still high |
| Result read on | the pair: peak plus trough, against the same pair last cycle |

Preparing during the peak rather than at the start of the trough is the difference between a
trough you planned and a trough you reacted to. The backward instrument has to exist before the
peak opens, and the rest of the ladder is built while the people it is meant for are still
buying.

## Edge cases

- **Perishable or expiring stock.** What moves forward is the commitment, not the goods: a
  pre-order paid in the trough and fulfilled at the season's start works, while any instrument
  that asks the person to take delivery early does not. A backward instrument has to be built on
  a part of the assortment that will still exist in the trough.
- **A trough with no demand at all**, an absence rather than a dip. There is nothing to move.
  Say so, give the trough to the maintenance work, and do not spend on a shift with no subject.
- **The deferred balance lands as one tranche.** A liability issued across a peak becomes a
  redemption cost concentrated on one window in the trough. The accounting, the expiry and the
  cost of the currency are `loyalty-program-design`'s; the obligation here is to tell that owner
  the size and the date of the tranche **before** it is issued, not when it lands.
- **The shift moves a cohort.** Buyers recruited inside a shifted window have a different second
  purchase window from an ordinary cohort, so they carry the occasion tag from the register
  (`repeat-purchase` reads it).
- **The extension offer reaches somebody with no flexibility.** Extension assumes the person can
  wait. Where the purchase is tied to a date of their own rather than to yours, the offer is
  noise at best, and at worst it reads as an attempt to move a customer off a commitment you
  made. Exclude the date-bound.

## Failure modes

**The trough was filled with demand that would have come at the peak.** The trough is up, the
peak is down by more, and the pair is flat or negative. Only reading the pair catches it: each
period on its own has a plausible story, and the trough's story is the one somebody is being
congratulated for.

**The instrument was redeemed inside the peak.** Redemptions concentrate in the days of the
window itself. Either the redemption window opened too early, or it was announced and not
enforced in the processing. The second is more common and looks identical in the report.

**The trough's work became the trough's product.** Every trough goes to audits, cleanups and
tests, no shift is ever built, and the trough's revenue is the same figure cycle after cycle. The
work is real and it has to happen somewhere. It is not a revenue instrument, and a trough that
reports only maintenance has not been worked.
