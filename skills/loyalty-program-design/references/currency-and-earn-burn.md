---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Currency, earning and redemption

This mechanic sets what the program pays in, what earns it, what it can be spent on, and how much
margin the whole arrangement consumes. Finance signs this part of the construction, and this is the
part that fails silently when it is wrong.

## Entry conditions

- The program has a named purpose and a named consumer for the data it will collect. Without the
  second, the construction is a permanent cost with no revenue side. `crm-program-design` holds
  the purpose, `loyalty-program-launch` holds the check that the consumer exists.
- You have gross margin by category, not a company average. You write redemption rules per
  category, and an average cannot write one.
- You know who carries the obligation: one legal entity, several, franchise partners. This is an
  entry condition rather than an implementation detail, because it can rule out a whole model.

## Exit conditions

A written rule stating what earns, on what event, at what rate, where earning is excluded, when
the balance becomes spendable, what it can be spent on and up to what share, and how long it
lives. The rule has passed the three launchability questions in `loyalty-program-launch` and
finance has signed the liability.

## Sequence

**1. Choose what the promise is made of.** Three families, and the choice is not a matter of taste.

- **Immediate discount**, fixed or growing with cumulative spend. Visible in the price, needs no
  arithmetic from the customer, creates no stored obligation. It pays for the purchase happening
  now and gives no reason to come back.
- **Deferred currency**: points, cashback, an internal unit. It creates a reason to come back,
  because the value lands on the next purchase. It also creates a stored obligation and requires
  processing, an expiry rule and redemption rules.
- **Paid access**: the customer buys the terms. The payment itself selects the audience and makes
  the benefit a decision the customer makes deliberately.

Choose on three tests. Is your category sensitive to price in the moment or to accumulation. Does
your pricing policy allow a direct discount at all: where a discount devalues the product in the
eyes of the buyer or the supplier, deferred currency does the same job by another route. And the
constraint that overrules the other two: **can your organization settle the obligation between the
entities that issue and accept it.** Currency earned in one legal entity and spent in another is a
settlement arrangement. Where that is not agreed, a points model is not available no matter what
the financial model says, and franchise networks are where this surfaces.

**2. Write the earning rule.** Four answers: which event earns (a purchase, a target action, a
date), what the rate is computed on (basket value, line item, the fact of the event), how much,
and where earning does not apply. Write the exclusion list in full at this step: clearance stock,
installment payments, gift cards, third party brands sold on your shelf. An exclusion you leave
out here arrives later as a complaint.

Earning for a non purchase action, a review, a completed profile, an answered survey, is buying
data, and you price it the same way you price a discount. The difference is that data is bought
once and a discount is paid every time.

**3. Set the availability delay.** What is earned must not become spendable before the return
window on the purchase that created it has closed. Otherwise a return of an item paid for with
currency produces a negative balance or an unrecoverable payout, and this is the one step in the
mechanic whose failure shows up as an argument at the till rather than as a line in a report.

The size of the delay is yours to compute: the return window plus the time it takes a return to
reach the system where the balance is calculated. The freshness class of that feed belongs to
`martech-stack`, and this rule is the reason to ask for it.

**4. Write the redemption rule and the depth ceiling.** Margin lives here. Three parameters: what
share of a basket can be paid in currency, what cannot be paid for at all, and how redemption
combines with discounts already applied. Write it so it can be said out loud. A depth that varies
with the discount on the individual item forces the customer to do arithmetic in front of the
shelf. The same depth attached to the customer's tier can be stated in one sentence.

You are allowed to vary depth by how fast stock moves: allow less redemption against items that
sell themselves, more against slow ones. It is the same lever as the earning exclusion list,
pulled from the other side and without a public promise attached.

**5. Check redemption against the promotional calendar.** The most expensive failure of this
construction starts here and makes no noise. If redemption is blocked on discounted items, and
the share of the catalog under discount grows year over year, at some point there is nothing left
to spend currency on. Membership keeps rising, the report looks healthy, and the program is dead.

Compute the check before launch and repeat it whenever promotional policy changes: the share of
turnover on which redemption is blocked, times the share of the calendar in which the discount is
running. You set the threshold at which the construction has to change. The alarm signal is
redemption share falling while the base grows.

**6. Set the expiry period and the reminder cascade.** Match expiry to the purchase cycle of the
category rather than to the calendar. Shorter than one cycle and the currency expires on people
who had no chance to return, which buys irritation instead of a visit. Longer than two cycles and
the obligation accumulates without moving anyone. Until you have your own data, start at one
typical purchase cycle for the category plus room for a season, and replace that as soon as you
can see the distribution of intervals in your own base. Where the cycle is long, that starting
point puts expiry so far out that the rule does almost nothing, which is itself the finding:
expiry is a lever in a category people buy from often and close to dead weight in one they do not.

Expiry is a working tool for flattening demand: currency granted with a short life moves a visit
into a low season. The reminder itself is a flow and belongs to `triggered-messages`. What stays
here is the reason for it and the timing.

**7. Price the promise.** Cost equals face value times the share that gets spent. Until
you have your own redemption coefficient, treat it as a starting estimate and replace it with fact
after one full currency lifetime has passed. This is the only way not to overpay in both
directions: costed at face value, the construction books an expense that will not occur and looks
more expensive than it is. Costed at zero, it pretends to be free.

**8. Send the construction for the launchability check.** `loyalty-program-launch` owns the three
questions: can the till compute it during payment, can a member of staff explain it in one
sentence, will finance carry the liability. Failing any of them returns the design here, and that
return is an entry condition of `changing-a-live-program.md`, not a reason to patch the rule at
the till.

## Thresholds and timings

Every line is a parameter you compute. None of them is a norm.

| What | Computed from |
|---|---|
| Earning rate | the share of category margin you will give up to buy a repeat purchase |
| Redemption depth ceiling | the same share, tested against your worst margin category rather than the average |
| Availability delay | the return window plus the lag before a return reaches the balance system |
| Currency lifetime | one typical purchase cycle for the category plus room for a season, as a starting point |
| Repricing the promise | after one full currency lifetime, then monthly |

## Edge cases

- **Balances too small to reach the ceiling.** Planned currency penetration into the basket and
  actual penetration diverge downward, because the ceiling permits more than people have saved.
  The margin loss forecast built on the ceiling is therefore too pessimistic, which is good news
  that is easy to mistake for a broken model. Measure it separately: average actual penetration
  against the ceiling.
- **A return on a basket paid partly in currency.** Step 3 covers the timing. The remaining case is
  a partial return: currency comes back in proportion, and the earning on the returned portion is
  reversed. Write the rule before launch, because after the first dispute it gets written by
  whoever is standing at the till.
- **Two currencies for two segments.** A legitimate construction: one group earns broadly and may
  spend only on a defined set, another earns only on high margin items and may spend on anything.
  The cost of it is explainability, and the rule that staff can explain it in one sentence now has
  to pass twice.
- **A category where quantity is fixed by something other than desire.** Fuel in a tank, a
  prescription, one set per season. A construction aimed at the average basket of the main product
  does not work here. A construction aimed at the adjacent part of the basket does.
- **Currency that can only be spent in one place**, such as an app or a single channel. A
  legitimate way to buy data, but it turns part of the promise into something a group of your
  customers cannot use. Size that group before you publish, not after.

## Failure modes

**Silent: the currency does not get spent.** Redemption share falls, membership rises, the
obligation accumulates, and the enrollment report reads as success. The repair is structural:
remove the redemption block, change the depth, change the unit of the promise. It is not a
communications problem, and reminding people about a balance they cannot spend makes it worse.

**Expensive: the currency gets spent exactly where the purchase would have happened anyway.**
Margin drains and behavior does not move. The tell is that redemption concentrates in groups whose
frequency and basket have not changed since they joined. Before and after is not evidence here.
Separating paid behavior from behavior that would have happened anyway needs a control group, and
that is `experiments-and-holdouts`.

**Organizational: there is nobody to settle the obligation with.** It surfaces during sign off and
cancels the model. Step 1 is where it costs least to discover.
