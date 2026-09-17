---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Referral rewards

This mechanic sets what you pay an existing customer for bringing a new one, for which event, to
whom, and how to avoid paying someone who brought nobody.

## Entry conditions

- There are enough people to recommend you. The channel works on reach, so the floor is a
  calculation rather than a base size, and the calculation has four terms: your base, the share of
  it that will send an invitation, the number of invitations each of them sends, and the
  conversion of an invitation into a first paid order. Multiply them and you have the orders the
  channel can produce in a period, and that number is what has to be worth building for. Two of
  the four terms are guesses until the channel runs, so write them down as guesses: before launch
  this is a go or no go on stated assumptions rather than a measurement. As a starting point, a
  base that clears the floor lands in the tens of thousands of customers for a consumer business
  and in the hundreds for business to business, where one customer is worth enough that far fewer
  new ones repay the build. Replace the guessed terms with measured ones after the first quarter
  of running it, and if your base is below the floor, the honest answer is to wait rather than to
  raise the reward.
- People are willing to recommend you. A referral mechanic scales the relationship that already
  exists, including a bad one. Take the signal from `voice-of-customer`, not from the wish to open
  a channel.
- You know the margin on an order. Without it there is no ceiling, and a channel without a ceiling
  goes into loss quietly.

## Exit conditions

Written down: the event that triggers payment, the amount to each side, the form of the reward,
the abuse limits, the payment timing, and the metric against which the channel is compared with
your other acquisition sources.

## Sequence

**1. Name what the channel has to deliver.** Lower acquisition cost, reach into an audience you
cannot buy, a base for a new product. Different goals take different rewards. The goal of having
one produces a construction with nothing to judge it by.

**2. Choose the event you pay for.** Pay for a first paid order, and put a floor on its value. The
floor screens out people who came for the reward and left, and it sets the bottom of the channel's
economics. Pay for a registration and accounts are what you buy. The
exception is a product whose target action legitimately comes before any payment, a free trial or
an account that is worth something in use: there the payment event moves earlier by design, and
the whole abuse load moves onto validation and the invitation cap, because a floor on order value
now screens nobody.

**3. Decide who gets paid.** A one sided reward, to the referrer only, is cheaper and slower: the
invited person arrives with no reason of their own. A two sided reward costs more and raises the
invited person's conversion into a first purchase, because they now have one. Choose against step
1: cheaper points at one sided, faster points at two sided.

The second axis is how deep you pay: only the person who invited, or also the people they invited
in turn. Depth multiplies what one acquisition costs, so carry it into the ceiling in step 4, and
it pays people to recruit inviters rather than customers, so set the limits in step 7 before you
set a rate.

**4. Compute the ceiling from margin.** In order: margin on an order, then the share of that margin
you will spend on acquisition, then the requirement that the total paid to both sides stays inside
it. If you pay in program currency, apply the redemption coefficient: when part of what you issue
is never spent, you can raise the face value and stay inside the same real limit. Anchor the share
of margin to what acquisition costs you in your other channels, not to somebody else's practice.

**5. Choose the form for the customer you want.** The form selects the audience even when the cost
does not change. A free first period brings people who leave when it ends. The same money offered
as extended value on a paid period brings people who pay. A cumulative reward selects for
frequency, a reward unlocked above an order value selects for basket size, trial access selects
for people who do not know the product yet. Pick from the profile of your valuable customer, not
from what is easiest to calculate.

**6. Set the payment timing.** After the return window closes, not at the moment of the order. It
is the same rule as the availability delay in `currency-and-earn-burn.md`, and it sits under
standing pressure: the referrer asks for the reward, and the request arrives before the return
window has told you whether there was an acquisition.

**7. Put the limits in.** Three, closing different holes:

- **Validate the invited account**, by a confirmed contact channel or a payment method, against
  accounts created only to collect a reward;
- **Cap invitations per period**, against mass distribution of links to strangers;
- **Require the target action above a floor**, against people who came for the reward rather than
  the product.

Add one rule about distribution: the referral link is not allowed in paid channels or on your own
brand search terms. Without it you buy your own traffic from your own customer. Put it in the
terms of the channel, because after a payout you cannot apply it.

**8. Compare against your other channels, not against zero.** Judge the channel on acquisition cost
and on the quality of who arrives, against what the rest of acquisition delivers. Someone who
arrives on a recommendation comes with trust already in place, so compare their behavior over a
horizon rather than on the first order. Take the horizon as two purchase cycles for the category,
and state which one you used.

## Thresholds and timings

| What | Computed from |
|---|---|
| Base size to start | base, times the share who share, times invitations each of them sends, times conversion of an invitation into a first paid order, against the orders worth building for |
| Reward ceiling | order margin times the share you spend on acquisition, adjusted by the redemption coefficient |
| Target action floor | the order value below which the order does not repay the reward |
| Invitation cap | your own observed distribution: mass inviting is a tail, not the norm |
| Payment timing | close of the return window |

## Edge cases

- **Business to business.** The base is smaller by orders of magnitude, each customer is worth
  more, and the deal cycle is longer. A one time payment for a first order works badly here: the
  referred customer keeps paying long after the deal closes, and a single payout at the start
  prices a relationship at its first order. What works is a recurring share of what that customer
  pays, which spreads the reward across the relationship rather than paying it for an event.
- **The invited person was already in your base.** That is not acquisition, and rewarding it is
  paying for your own customer. Check against existing records before payout, using the matching
  keys held by `list-building`.
- **Self referral.** A special case of the above and the main abuse route. Validation and the
  action floor close it.
- **A referrer who has become a channel.** A few participants bring disproportionately many. This
  is not always fraud: sometimes it is a partner, and then the construction changes for them,
  moving from a promo code to an agreement with terms.
- **The tax treatment of the reward.** Payments and gifts can carry a threshold above which
  someone owes tax, and who owes it varies. Check before you publish a rate, because a reward the
  recipient is taxed on is a different reward from the one you announced. This skill does not
  answer which regime applies to you.

## Failure modes

**Paying for registrations.** The channel fills with accounts, the acquisition number rises, orders
do not follow. The tell is that the share of invited people reaching a first order is far below
what your other channels produce.

**A reward above the margin.** The channel works and loses money on every order it brings. The tell
is acquisition cost through the referral channel exceeding your paid sources, when the channel was
built to do the opposite.

**Running it on an unhappy base.** Invitations do not circulate, and the ones that do carry the
opinion of the product with them. Diagnose it before launch. It is not repaired here.
