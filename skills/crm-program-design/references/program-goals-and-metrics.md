---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# The goal, the one number, and the metrics around it

A program that has not named what it is for still produces work. Campaigns go out, reports come
back, everyone is busy, and at the end of the cycle the honest answer to "what did this change" is
a list of activities. The cause is upstream of every mechanic: nobody chose the number.

This mechanic covers whether a program is worth running at all right now, where its goal comes
from, how you choose one target metric and test it before you commit to it, what sits around that
metric so nobody can buy it too expensively, and how often you read and re-cut the whole set.

## Entry conditions

A business intends to work with people who have already been in contact with it, and nobody has
said out loud which number that work is for.

## Exit conditions

One target metric. Under it, key results each of which a named person moves directly. Balancing
metrics that show what the target costs. Leading metrics per lifecycle stage. A read cycle and a
separate revision cycle. A written list of what the program is **not** judged on this cycle.

## Steps

**1. Establish that a program is worth running now.** Four conditions, each checked against your
own data rather than against a category average.

- People in this category come back at all.
- You hold records you may write to, on a basis that still holds.
- You can read the result: a population exists on which the target metric is legible.
- Somebody will run this regularly rather than once.

Each failure has its own answer, and none of them is "start anyway". The first failing means the
program is not measured by repeat purchase, and the edge cases below say what replaces it. The
second means intake and basis come first: that is `list-building` and `consent-and-preferences`,
and you do not have a program yet. The third means the base is small for the cut you had in mind,
so either the cut gets coarser or you wait; the readable floor belongs to `segmentation`.
On the fourth, say it plainly: this will be an occasional send, not a program, and program metrics
will not describe it.

**2. Take the goal from the level above and write it down verbatim.** Derive the program goal from
a business or marketing goal, not from a channel. Where no goal exists above you, that is the first
thing to go and get. Until it arrives, mark the target metric provisional and give it the date you
will revisit it.

**3. Choose one target metric.** It has to satisfy three conditions at once: it moves in response
to what the program does, it converts into money through arithmetic you can show, and it is legible
on the population the program controls. The construction of the metric itself, its numerator,
denominator, window and attribution, belongs to `metric-definitions`. What you decide here is
which of them the program is judged on.

**4. Test the choice against a link model.** A link model is a table where metrics are joined by
formulas, so that changing one shows what happens to revenue and profit. Move the candidate by an
amount you could plausibly achieve and look at the money. If the money barely moves, the candidate
is a reporting metric, not a target, and it does not go into the goal.

**5. Decompose the goal into key results.** Each one is a smaller metric that a specific person
moves directly. The signature of a bad decomposition is a key result whose lever sits with product,
price or logistics. Such a result either gets the lever or leaves the decomposition.

**6. Add balancing metrics: what gets worse when the target is bought too expensively.** At least
two. The cost of one incremental result, and the load the program puts on a person: complaints,
unsubscribes, messages per period. The cap on that load is `contact-orchestration`. A target metric
with nothing balancing it gets delivered by discount and frequency, and both bills arrive later.

**7. Add leading metrics per lifecycle stage.** These move before the target does, which is what
makes them usable for steering inside a cycle. The owner of that stage holds each one, not whoever
runs the program.

**8. Set a read cycle and a revision cycle, and keep them apart.** Read often, so a break is
noticed. Revise rarely and on the calendar, so that a bad month does not rewrite the goals.
Separating them is the decision: the read cycle comes from how fast your own numbers can change,
the revision cycle from how long a change needs to show up.

**9. Write down what the program is not judged on this cycle.** The rejected metrics, each with the
reason it was rejected. Without that list the rejected metric returns in the first argument, and
the argument runs from the beginning.

## Thresholds and timings

- **Exactly one target metric.** This is a construction, not a preference. Two of them means every
  conflict between them gets resolved fresh each time, by whoever is senior rather than by whoever
  is answerable.
- **As many key results as there are owners** (see `ownership-and-resource.md`). A result nobody
  owns is a wish.
- **Read cycle:** no less often than the reporting period of the business, and no more often than
  the target metric can change for a typical person. The second bound comes from your own purchase
  cycle.
- **First honest read of a new program:** start with the point where the target metric has had two
  chances to update for a typical person, computed from your own purchase cycle. Before that date,
  leading metrics are what you read. That starting point holds where the cycle is stable; where it
  is not, take the date from the point at which your own history shows the metric settling, and say
  which of the two you used.
- **Revision cycle:** fixed. Until you have your own history, start with once a quarter. That
  holds where the purchase cycle is shorter than a quarter. Once your own cycle is measured, tie
  revision to it rather than to the calendar quarter, and say what you tied it to.
- **Self-baseline** for any metric with no citable benchmark: start with eight to twelve of your own
  stable periods, median and spread. This works where the period is stable; in a category where
  people buy once a year it asks for eight years of history, so take the longest run you hold and
  say so. Replace the starting figure once you hold two full cycles of your own data.

## Edge cases

- **A category without repeat purchase.** One large purchase and nothing after it. The target
  cannot be frequency. The program is judged on referral, on a second product, on a service
  outcome, or on attached revenue, and that gets said out loud rather than forced into the
  familiar metric.
- **A long purchase cycle.** The target metric cannot be read inside the cycle. The program runs on
  leading metrics for the first periods, and the date of the first honest read of the target is
  named in advance and written down.
- **Seasonality.** The target moves for reasons the program did not cause. Read it against your own
  period a year earlier or against a control group; the construction of the comparison belongs to
  `experiments-and-holdouts`.
- **The goal above you changes mid cycle.** Program goals are re-cut immediately rather than left
  to sit out the quarter. Retired goals are marked retired with a date, so that nobody reports
  against them next cycle.
- **Two brands or two markets under one program.** One target metric, read separately for each.
  A pooled figure hides the side where things are going badly, and it hides it until fixing it is
  expensive.
- **A metric whose lever belongs to another department.** Assortment, price, delivery. Either the
  program gets the lever or the metric moves out of the goals and into the observed.
- **The program is already running and goals were never set.** Do not reconstruct them backwards.
  Take the current cut as a zero point, call it a zero point, and measure movement from there.

## Failure modes

**The program has more than one target metric.** The signature: two owners are both right at once,
the argument between them is settled by rank or volume, and the money is flat. What to do: choose
one, demote the rest to balancing and leading, and record the choice with a date and a reason.
Until that choice is made, the queue in `launch-queue.md` cannot be cut, because build order is
derived from a single goal.

**The target metric was chosen from the channel rather than from the business.** The signature:
the metric improves cycle after cycle and nobody outside the team can say what it changed for the
company. What to do: run step 4 on it. A metric that moves nothing in the link model is a reporting
metric that got promoted, and it goes back where it came from.
