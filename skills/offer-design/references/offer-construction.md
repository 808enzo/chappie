---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Constructing an offer: form, depth, condition, window

An offer is not a discount with a number attached. It is a promise with five decisions inside it:
what form the benefit takes, how deep it goes, what it is conditional on, how long it lives, and
what it does not apply to. Every one of the five is somebody's decision before the first
message goes out. Skip them and the number gets chosen by whoever is in the room, out of the
margin of a product nobody looked up.

This mechanic covers how you get from a neighbor saying "this person needs an incentive here" to
an offer you can price, issue, and read afterwards.

## Entry conditions

A neighboring mechanic has named the occasion for a monetary argument and has not named what it
is.

## Exit conditions

An offer specification: the job and the number that has to move; the benefit form; the depth with
its ceiling; the entry condition; the redemption window; the exclusion list; the audience; and the
way you will check that the offer did not simply pay people who were going to buy anyway.

## Steps

**1. Name the job, and check it is a job an offer can do.** The job names a number that has to
move, and that number is a property of an order or of frequency: order value, share of orders
containing a category, time to next purchase, units of stock cleared. Awareness, brand affinity,
and sentiment do not move this way, and trying to move them with an offer produces a discount with
no addressee: the money goes out and no number comes back that anyone can point at.

**2. Test the recipient for "would have bought anyway".** The more precisely a segment is selected
for readiness to buy, the higher the chance the offer is paying for a decision already made. The
warning sign is a segment selected by an action that is itself evidence of intent. **An exclusion
test is mandatory here**; designing it belongs to `experiments-and-holdouts`. What stays with this
skill is the obligation to demand one and the ability to read the answer: if the tested group and
the excluded group bought at the same rate, the benefit was a transfer, not an incentive, and the
right response is to narrow the audience rather than to deepen the offer.

**3. Choose the benefit form on three axes.** The axes are independent, and each one changes both
the cost and the failure mode.

- **When the business pays.** Immediately (a price reduction, a gift with purchase) or later
  (an accrual, cashback, early access). An immediate form takes margin off this order. A deferred
  form moves the cost to the next one and creates an obligation whose construction belongs to
  `loyalty-program-design`.
- **What the amount is computed from.** A share of the item price, a share of the basket, or a
  fixed amount. Percentage and fixed forms win in different price bands, and that fact comes back
  as a decision in `stacking-and-arbitration.md`.
- **Given or earned.** A given benefit goes to everyone in the audience. An earned benefit goes to
  whoever completes an action: a quiz, a game, a collection, a draw. The axis changes how the
  cost is counted (per recipient against a fund, step 4), how it is protected
  (`issuing-and-honoring.md`), and which legal regime applies (SKILL.md).

**4. Compute the depth ceiling.** This is arithmetic, not judgment. With gross margin `m` as a
share of price, a discount `d` as a share of price removes `d / m` of the profit on that sale; for
profit to stay level, volume has to rise by a factor of `1 / (1 - d/m)`; at `d = m` the profit is
zero no matter how much volume rises. **The number to say out loud is not the depth but the
required growth**, because required growth is comparable to something: the best growth this
mechanic has ever produced for you. A depth that demands more than that has already failed on
paper.

Where you have no response data of your own yet, start with a depth no greater than half the gross
margin, which keeps required growth at or under a doubling. That is a starting point rather than a
property of any market. It applies where unit cost is stable and the category has no established
price anchor; it does not apply where the cost of goods moves with volume, or where the category
has trained customers to wait. Replace it with the first depth test that shows a smaller depth
producing the same response, and run that test early, because until you do, the starting figure
is an assumption sitting where a finding belongs.

**5. Set the entry condition from the recipient's own behavior.** The threshold is computed from
the recipient's own average order value, not from the base average. Below their own average it is
a gift for what they would have done regardless; several times above it, it is a condition nobody
meets. The job decides the direction: "raise order value" needs a threshold above the recipient's
own average, while "bring the next purchase forward" is better with no threshold at all, because
there the threshold is just one more barrier in front of the thing you want.

**6. Set the redemption window from the purchase cycle, not from the calendar.** Take it as a
fraction of the median interpurchase interval of the category. Where people buy daily, a day is a
working window; where people buy once a season, a day guarantees the offer expires unused. Window
and depth are not independent decisions: a short window is itself an argument, and a short window
needs less depth to do the same work.

**7. Write the exclusion list before launch.** What the benefit does not apply to: items whose
margin is below the depth, items in short supply, items already marked down, items under a pricing
commitment to somebody else. A list written after launch is not a list, it is the withdrawal of a
promise people are already holding (`issuing-and-honoring.md`).

**8. Compare against the public offer that is already running.** A personal offer that is not
better than the public one is not a personal offer: there is no reason to use it, and the entire
cost of selecting the segment disappears, because nothing in the order data will ever show it was
selected.

**9. Check the promise is deliverable before you send it.** Three checks. **Stock:** enough of the
promised thing exists for the response you expect. **Path:** how many actions sit between
receiving and redeeming, where the carrier lives, whether it survives dismissing a notification,
whether it can be entered by hand, and whether it works in the sales channel the message points
to. **Condition:** whether it fits in one sentence. Each additional clause removes people who were
willing, so a condition that takes a paragraph is spending audience on precision nobody asked for;
the sentence test is what makes that visible before the send rather than in the response rate.

## Thresholds and timings

| Quantity | How it is derived |
|---|---|
| Profit removed by depth | `d / m` of the profit on the sale, arithmetic from margin and depth |
| Required volume growth | `1 / (1 - d/m)`, arithmetic, and the number to compare against your own history |
| Starting depth ceiling | no more than half the gross margin, until you hold your own response data (see step 4 for where it applies and how to replace it) |
| Entry threshold | a multiplier on the recipient's own average order value |
| Redemption window | a fraction of the category's median interpurchase interval |
| Recovery window after removing a benefit | two purchase cycles of the category as a starting figure, replaced by what your own first removal shows (see the failure modes for where it applies) |
| Prior price in a reduction announcement | the lowest price applied in the 30 days before, in the EU regime (see SKILL.md, including who it does not bind) |

## Edge cases

- **A recipient with no history of their own.** There is no personal average to set a threshold
  from. Substitute the average of the capture point's cohort rather than the base average: where
  someone was captured predicts their behavior better than the base as a whole does
  (`onsite-capture` reads capture quality by cohort for the same reason). Say which substitute you
  used, because the threshold will look wrong later to anyone who assumes it was personal.
- **A category where a price reduction is ruled out by positioning.** Change the form entirely
  rather than the depth: early access, delivery, a service, a gift. The depth still has to be
  computed: a gift has a unit cost, and "it isn't a discount" is not an argument about money.
- **A negative-margin item inside a bundle.** A bundle is priced on the margin of the bundle, not
  of its parts, and this has to be said out loud in the specification. Otherwise the exclusion
  list from step 7 removes exactly the item the bundle was built around.
- **The same depth offered to the same person twice.** The second one is not a promotion, it is a
  price. The sign is a recipient whose last two purchases both carried a benefit; at that point
  the decision is about the list price, not about the next campaign.
- **A segment too small to repay the setup.** An offer has a fixed cost that does not shrink with
  the audience: the specification, the build, the check. Below some size, doing nothing is
  cheaper than doing something personal, and the size where that flips is worth computing once
  rather than arguing about per campaign.

## Failure modes

- **Price anchoring.** The signature: the share of orders carrying a benefit rises while revenue
  per order **between** promotions falls. The mechanic has produced a new regular price. Removing
  the benefit causes a drop, and the drop passes on its own. The operational rule is about the
  decision, not the drop: **name the recovery window before you remove anything.** Two purchase
  cycles of the category is a starting figure and nothing more. It applies where the cycle is
  stable and where the benefit was the main reason a large part of the base was buying. It is not
  a property of your market, and your own first removal replaces it: you can read both the drop
  and the return in revenue per order between promotions. **Do not reverse the decision inside the
  window you named.** Reversing inside it makes the anchor permanent, because it confirms to the
  base that waiting works.
- **Cannibalization across products.** Sales of the promoted item rise and the category does not:
  the benefit moved demand off a neighboring item that serves the same purpose. The fix is to
  widen the offer to the line rather than to deepen it on the item.
- **Pull-forward in time.** After the promotion ends, sales fall below normal and then recover
  without intervention: the purchase happened earlier, not additionally. It is told apart from the
  case above by two signs: the whole category falls, and it falls only after the end.
