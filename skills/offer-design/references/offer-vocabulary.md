---
claim_type: definition
source_type: internal
source: "internal synthesis"
checked: 2026-09-07
---

# The vocabulary of offers

The three mechanics assume these terms. Four of them (*reward*, *precedence*, *consumable
resource*, and *threshold*) mean something else in a neighboring skill, and one,
*cannibalization*, names two different phenomena inside this one. Settle them before the
discussion, not during it.

## The unit

**Offer.** One promise, of one form, at one depth, to one audience, with one entry condition and
one redemption window. Not a campaign and not a message: one offer lives across several messages,
and one message carries one offer.

**Issued promise.** The instance of an offer that reached a particular person. The unit of
`issuing-and-honoring.md`. It exists independently of whether the promised thing still does, which
is the whole point of holding it as a separate object.

**Redemption attempt and its outcome.** An attempt is a code entered, or an order placed by the
holder of an issued promise inside the redemption window; on a shared carrier, only a code entered.
It has one of three outcomes: applied in full, reduced by the floor, or not applied, with the reason
named after the rule that refused (an issuing limit, the window, the entry condition, an exclusion,
the stock, a carrier that no longer works, an offer that outranked this one). The share not applied
is read beside realized depth, because depth itself cannot see a benefit that never applied.

**Order.** The unit of `stacking-and-arbitration.md`. Several promises meet here, at checkout, and
this is the only place where what was actually given can be observed.

## The construction

**Benefit form.** Three independent axes: when the business pays (immediately or later), what the
amount is computed from (item price, basket, fixed), and whether the benefit is given or earned.

**Depth.** The size of the benefit as a share of price. **Designed depth** is what the
specification says. **Realized depth** is what actually left with the order after arbitration. The
gap between them is the subject of the third mechanic and the skill's control metric.

**Entry condition.** What has to be true of the order for the benefit to apply: minimum value,
basket composition, channel. Not to be confused with the entry condition of a mechanic, which is
about when you run the work at all.

**Redemption window.** How long a person can use an issued promise. `promo-calendar` places one on
the calendar with a start later than issuance, for an instrument earned at a peak and spendable
only after it; the length is still defined here.

**Stock.** How much of the promised thing remains: codes in the pool, units on the shelf, money in
the fund. A quantity, where the redemption window is a length of time, and the two are exhausted at
different moments. They also drain differently, which decides the level at which issuing stops: a
pool of codes goes down as you issue, a shelf and a fund go down as people redeem. The rule for
what happens when the two disagree is the central rule of the second mechanic: the promise lives by
the window.

**Carrier.** Whatever presents the promise: a code, an automatic rule on a segment, an accrual to
an account, a physical object. A unique carrier belongs to a person; a shared one belongs to
nobody, and every difference between the two rows in the carrier table follows from that.
**`loyalty-program-launch` uses the word for something else**, the form in which a member presents
an identifier at the till, and `messaging-channels` uses it for the telecom operator. The shared
and unique distinction does carry across: a household loyalty card is a shared carrier and belongs
to nobody in the same way.

**Exclusions.** Items the benefit does not apply to. Written before the first issue; added
afterwards, they are a narrowing of a promise somebody already holds.

**Given and earned benefit.** A given benefit reaches everyone in the audience. An earned benefit
reaches whoever completed an action. The cost of an earned benefit is counted as a fund rather
than per recipient, and it is protected by limiting attempts rather than redemptions.

**Prize fund.** The ceiling on what an earned benefit can cost, set before launch. A ticket-based
draw is the way to fix the fund when the number of winners cannot be forecast.

## The collision

**Stack.** The set of offers applicable to one order at the same time.

**Offer group.** The unit relations are set on. Relations between groups survive new offers;
relations between individual offers do not.

**Floor.** The limit arbitration does not cross. You can set it from either end, as a cap on total
benefit per order or as a minimum margin per order; once you know the margin on the order, those
are one limit written two ways. Reaching the floor recomputes the remaining allowance rather than
canceling the second benefit.

**Reward.** Shared with `loyalty-program-design`, and the two meanings are told apart by how long
the decision lives, not by size. Here a reward is the depth of a single discount on a single order
and the economics of the promo code carrying it, all of it alive for one promotion. There it is a
property of the construction: the earning rate, the value of a tier, the referral payout, all
published to the base and changed only by a revision. A one-off discount is often larger than a
year of earning, so size decides nothing. "How much do we give to close this order" is ours; "what
do we pay, permanently, for people coming back" is theirs. Where a game pays out in program
points, the split runs the same way: the cost of running the game is ours, the accrual model is
theirs.

**Precedence.** Which offer applies to one order when several qualify. Not to be confused with
**message precedence**, which decides which message reaches one person in a period when several
compete. That one belongs to `contact-orchestration`, and its vocabulary states the same split
from the other side. The two share a word and nothing else: different unit (order against person),
different moment (checkout against send), different consequence (an offer does not apply at all,
whereas a message is suppressed or deferred). Ask which one somebody means before agreeing to
anything about "priority".

**Consumable resource.** Here, the stock behind an offer. In `program-audit-and-ops` it is a class
of monitored object, one that reports a level rather than an event. The split: that skill owns
watching the level and raising the signal, this one owns the stopping level it watches for and the
fate of promises already issued.

**Threshold.** Here, the entry condition of an offer, and a property of the order. In
`segmentation` a threshold is a boundary on an attribute that defines a cut, or the size below
which a segment cannot be read. Both skills use the word constantly, and confusing them produces
one specific mistake: a threshold set from the base average, which is the segmentation habit,
instead of from the recipient's own average order value. That turns the offer into either a gift
or an impossible condition, depending on which way the recipient sits relative to the base.

## The failures, named

**Cannibalization across products.** A benefit on one item took sales from a neighboring item
serving the same purpose. Signature: the item rose, the category did not.

**Pull-forward in time.** The purchase happened earlier rather than additionally. Signature: the
whole category falls after the promotion ends and recovers without intervention. The two share a
name in ordinary speech and have different fixes, so keep them apart.

**Price anchor.** The state of a base in which the price without a benefit has stopped reading as
a price. Signature: the share of orders carrying a benefit rises while revenue per order between
promotions falls.
