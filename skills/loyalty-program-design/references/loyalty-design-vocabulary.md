---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Loyalty design vocabulary

The terms the four mechanics assume. Three of them name something different one skill over, and
those three are written into both vocabularies.

## The construction

**Construction of the program.** The set of rules announced to the base: what earns, what can be
spent, which tiers exist, what a referral pays. Not the launch, which is a project, and not the
running of it, which is a duty. The construction is what you would have to hold a project to
change.

**Program currency.** The unit of a deferred promise: points, cashback, an internal token. An
immediate discount has no currency, which is why it also has no obligation attached.

**Earning.** The event in which the promise comes into existence. Defined by the source event, the
rate, and the exclusion list.

**Redemption.** The event in which the promise is honored. Defined by the depth ceiling, the list
of what can be paid for, and the rule for combining with discounts already applied.

**Redemption depth.** The share of a basket that may be paid in currency. A ceiling of the
construction rather than a fact: actual penetration is almost always lower, because balances are
smaller than the ceiling allows. *Penetration* here means the share of a basket paid in currency.
`loyalty-program-launch` uses the same word for three other shares, all of them about recognizing
people rather than spending points; its vocabulary carries the split.

**Currency lifetime.** The period after which an unused promise ends. A tool for flattening demand
and, at the same time, the largest single source of customer irritation the construction contains.

**Liability.** The outstanding currency sitting on the accounts of your base. It grows with
earning and is discharged by redemption and by expiry. This is the side of the construction that
finance owns.

**Redemption coefficient.** The share of what you issue that gets spent. It converts the
face value of a promise into its cost, and until you have measured your own you are estimating it.

## Tiers

**Tier.** A group of members with a raised rate or a separate privilege. Defined by qualification
basis, boundary, and confirmation window.

**Qualification basis.** The attribute that grants a tier: spend within a window, number of
purchases, or lifetime spend. The three move different behavior and fail in different ways.

**Confirmation window.** The period within which a member has to qualify again or lose the tier. No
window means a lifetime tier.

**Tier value.** What a tier costs you: rate times the turnover of the group, plus the cost of any
privilege that is delivered by systems work rather than by margin.

## Referral

**Referrer and referee.** The person inviting and the person invited. They are named separately
because the reward to each differs in size, in form and in when it is paid.

**Payment event.** What the referral reward is granted for. A registration is not one.

## Revision

**Revision.** Changing an announced rule through a forecast, a slice test and a member migration.
Not the same as repairing execution: if the mechanic is not doing what it was designed to do, that
is monitoring work and belongs to `program-audit-and-ops`.

## Three words this skill shares with a neighbor

**Reward, shared with `offer-design`.** Here a reward is a property of the construction: the
earning rate, the value of a tier, the referral payout. There it is the depth of a single discount
on a single order and the economics of a promo code. What separates them is how long the decision
lives: what this skill sets gets published to the base and changes only through a revision, and
what that skill sets lives for one promotion. Size has nothing to do with which is which. "How much do we give to close this
order" is theirs. "What do we pay, permanently, for people coming back" is ours.

**Redemption, shared with `program-audit-and-ops`.** Here redemption is a side of the construction:
the rule, the ceiling, the share. There a consumable resource, a stock of promo codes or a
remaining budget, is an object of standing watch whose sign of life is its level. The same word
names a rule here and a remaining quantity there.

**Program, shared with `crm-program-design`.** There the program is the whole of your CRM work, its
purpose and its budget. Here the program is the loyalty construction inside it. That skill has
already written this seam from its side. It is repeated here because a reader arriving from there
is looking for a different word in this file.
