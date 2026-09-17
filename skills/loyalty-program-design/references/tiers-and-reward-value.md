---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Tiers and reward value

This mechanic sets who the program pays more than everyone else, on what basis, and what that
costs. It also settles how you tell whether a tier is changing behavior or paying for behavior
that already happened.

## Entry conditions

- The earning and redemption rules exist (`currency-and-earn-burn.md`). Tiers modulate the rate,
  so without a rate there is nothing to hang them on.
- Your base has enough history to show a distribution: how much people spend, how often they come
  back. You set tier boundaries from your own distribution, never from someone else's ladder.
- You know what the program is trying to move: frequency, basket size or retention. You choose the
  qualification basis for that, and it differs for each of the three.

## Exit conditions

The ladder is written: qualification basis, boundaries, confirmation window, what each tier gives,
what each tier costs. For every privilege you have written down what pays for it, margin or
systems work.

## Sequence

**1. Decide whether to have tiers at all.** Tiers work where the base contains distinguishable
groups by value and there is somewhere to move people: the person one step below a boundary is the
addressee of the whole mechanic. Tiers do not work where the purchase is rare and singular,
because nobody survives to the second tier, and a ladder nobody climbs is a shop window that costs
money. Deciding against tiers is a normal outcome of this step.

**2. Choose the qualification basis.** Three options, each with its own behavior.

- **Spend within a window.** Moves frequency and basket size together, penalizes the seasonal
  buyer, and requires a confirmation window.
- **Number of purchases.** Moves frequency and splits baskets: people break one order into two to
  reach the next tier. If splitting damages your fulfillment economics, this basis is wrong for you.
- **Lifetime spend.** The tier is never taken away, communication is simpler, and there is no
  downgrade to explain. But once someone reaches the top the basis stops moving anything, and the
  top of the ladder accumulates people the program has nothing left to offer.

**3. Put the boundaries on your own distribution.** A boundary belongs where there is mass behind
it that one step could move, not where the number looks tidy. Before you fix a boundary, count how
many people sit one step below it and what moving them would cost. If nobody is standing one step
below, the boundary is decorative.

**4. Set the confirmation window.** A lifetime tier is cheaper to communicate and more expensive
in margin: it pays forever for behavior that happened once. A tier that has to be re confirmed
moves behavior, and it creates the one event in a loyalty program guaranteed to generate anger,
which is the downgrade. Announce a downgrade before it happens, with a window long enough to avoid
it. Terms that permit a downgrade are not the same thing as a customer expecting
one: the customer discovers an unannounced downgrade at the till, in front of someone who cannot
reverse it.

**5. Price each tier.** Start from the cheapest form that changes behavior, not the most visible
one. Test two reward sizes against one metric. If the difference is not there, take the smaller
one: direct cost falls and the effect stays. It is the cheapest test in this skill, and it is the
only one that answers whether a tier is worth the rate attached to it.

**6. Separate paid privileges from operational ones.** Early access, a longer hold on reserved
items, priority service, a dedicated support route cost systems work and cost no margin. Put them
at the top of the ladder, where cash generosity is most expensive and price sensitivity is lowest.
A cash privilege at the top is the most expensive line in the construction and the one most likely
to be paying for behavior that would have happened anyway.

**7. Check who you are paying.** The top tier consists, by construction, of people who buy a lot.
The question is not whether they buy a lot. It is whether they buy more because of the tier. Only a
control group answers it: a share of the people who qualified do not receive the raised rate for a
period. This is a control group defined on an attribute that is itself an outcome of behavior, so
build it with `experiments-and-holdouts` rather than by hand. A construction in which that
measurement is impossible bills you forever with no way to check the invoice.

**8. Write down what the whole ladder costs.** Sum across tiers: share of the base on the tier,
times the tier rate, times the expected turnover of that tier. Do it before you publish, because
after publication the ladder changes only through `changing-a-live-program.md`.

## Thresholds and timings

| What | Computed from |
|---|---|
| Tier boundaries | the distribution of spend or frequency in your own base, and the mass sitting one step below |
| Confirmation window | the purchase cycle of the category times the number of purchases the tier requires |
| Downgrade notice | not shorter than the time in which someone could realistically make a purchase in your category |
| Tier rate | the share of margin you will give that group, at the turnover that group produces |

## Edge cases

- **One tier is worth different amounts in different brands.** A shared program across brands with
  different average baskets: an identical rate means a different sum and a different share of
  margin. Vary the rate by brand and keep the tier name common, because a customer who compares
  the two reads a common rate on different prices as the deal being worse in one of them.
- **A customer on the boundary.** Publish the rounding rule and the moment of assignment: is the
  tier granted at the moment of purchase or at the nightly recompute. The customer is doing this
  arithmetic themselves, so any gap between your answer and theirs is visible immediately.
- **A tier granted as a one off.** A promotion that gifts status creates a cohort whose behavior
  does not match its tier. Count them separately or they distort the reading of the whole ladder.
- **Cannibalization between brands under a shared program.** Measure the overlap between the brand
  bases before launch and after, and keep measuring it. A shared program makes the second brand
  reachable, so some of the growth in the overlap is the program working. You are moving customers
  rather than attracting them when the overlap grows while the combined count of new customers
  across the brands does not.
- **The seasonal buyer.** A spend within a window basis downgrades them every off season. Either
  make the window a multiple of the season, or change the basis.

## Failure modes

**The ladder as a shop window.** Tiers exist because a competitor has more of them. The tell is
that the share of members moving between tiers in a period is close to zero while the base is
active. The ladder is paying for a distribution that existed without it.

**Everyone at the top.** With lifetime spend as the basis and no confirmation window, the top tier
can only grow, because nobody ever leaves it. Once it holds a large enough share of the active
base, the raised rate stops being a privilege and becomes a general discount that costs more to
explain. The tell is the share of the active base at the top tier rising year over year with no
change to the terms. Fix it through a revision, not by adding a tier above: a new top tier starts with almost
nobody on it and repeats the same history.

**A downgrade nobody was warned about.** The only failure in this mechanic measured in complaints
rather than margin. Restoring the tier does not undo it: the promise was already broken once, and
the customer now knows it can be. Prevention is step 4, not customer service afterward.
