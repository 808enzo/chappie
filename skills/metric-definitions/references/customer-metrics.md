---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Customer and money metrics

Formulas and denominators for the metrics a lifecycle program is judged by. Each entry names the
population, the window and the traps. No ranges appear here: a market figure is only usable
alongside the definition its source used, and this library states a number only with that source
attached.

Several metrics on this page circulate in more than one formula. Where that is true it is said
outright, because picking one and recording the other as a known variant is the entire job.

## Active customer

Not a flag on a record. A definition through a window: someone who made a qualifying purchase
inside a stated period. Everything below depends on it, and it is the definition people assume
instead of writing.

State three things: what qualifies as a purchase, how long the window is, and whether the window
is rolling or aligned to the calendar. In a category people buy from quarterly, a monthly window
makes most of the base look inactive and the metrics built on it move on nothing.

The category's purchase cycle, wherever these files use it, is its median interpurchase interval,
and the interval is `repeat-purchase`'s term: the time between two closed purchases by one person.

## Repeat purchase rate

- **Numerator:** customers with more than one qualifying purchase in the period.
- **Denominator:** customers with at least one in the same period.
- **Window:** stated, and long enough for a second purchase to be physically plausible in the
  category.

Used where a repeat requires a decision and an action: retail, ecommerce, most services.

**It moves with acquisition.** When new customers stop arriving, fewer one-purchase customers sit in
the denominator and the rate climbs with no change in repeat behavior; a period too short for a
late first buyer to buy again pulls it down the same way. `crm-reporting` keeps this construction
on its register of vanity metrics. For a decision, read the second purchase rate of first purchase
cohorts at equal age, with new customers in the period beside it.

## Retention rate

Retention answers one question: of the customers you already had, how many are still here at the
end. You fix the population before the period opens, and the numerator can only be a subset of
it.

- **Numerator:** customers from the starting cohort who still meet the retention condition at the
  end of the period.
- **Denominator:** the size of that starting cohort, counted at the moment the period opens.
- **Window:** stated, and taken from the category's purchase cycle rather than from the reporting
  calendar.

The retention condition is what "still here" means, and it changes with the business model. In a
contractual business it is a live subscription on the end date. In a non-contractual one nobody
announces a departure, so it is a qualifying purchase made after the period opens and by its end.
Do not borrow the active customer window for it: where that window is longer than the period, a
customer whose last purchase came before the period opened is still active at the end and reads as
retained without buying. Say which condition you used; the two answer different questions and both
get called retention.

**A subscription in recovery on the end date is live.** A failed charge opens a recovery case with
a deadline written on the day it opens. Until that deadline the subscription counts as retained,
and its departure date is the day the case closes, by decision or by deadline, never the day a bank
refused the charge. `subscription-retention` owns the case. The rule raises retention by
construction, because a longer recovery window keeps more unpaid subscriptions live across the end
date, so publish the count of subscriptions in recovery on the end date, by access class, beside
the retention line.

**A contract stays live past a missed date in three states, each with a ceiling.** In collection,
it is live until the end of the cure period; in a holdover, only under a written extension and
until that extension's end date; in its notice period, until the termination takes effect. The
departure date is the date the termination takes effect, not the day a payment was missed, and not
the end date when the signature came later. If a departure in your contract retention carries
either of those dates, take its date from the record that closes the case. Where two states are
open at once, the earliest ending holds: past the end of the contract term, a collection case runs
on a debt, not on a live contract. `b2b-retention` owns the dates. Publish the count and the
revenue of contracts in collection and in holdover on the end date beside the retention line.

**A shortcut circulates that breaks on its own arithmetic.** "(customers at end of period minus
new customers acquired in period) / customers at start" subtracts every acquisition from the
closing count, including the acquisitions that already left. Start with 100 customers and keep 20
of them; acquire 200 during the period, of which 80 are still there at the end. The closing count
is 100. The shortcut computes (100 - 200) / 100 and returns a negative number, while the starting
cohort kept one customer in five. Retention cannot be negative, and that one is.

The shortcut equals cohort retention only under two constraints: `new` counts new customers still
present at the end, and reactivated customers sit outside both terms. Write both into the
definition if you keep it. If your query cannot enforce them, use the cohort form.

A third formula, **returning customers in period / customers at start**, is a different metric
wearing the same name: it counts a purchase inside the window rather than presence at the end of
it. Pick one form, write which, and record the others as known variants you do not use.

**An empty starting cohort leaves the metric undefined.** Publish `not defined` with the cohort
size beside it; a zero in that slot reads as everybody leaving.

Retention is the mirror of churn only when both are computed on the same population, the same
window and the same definition of activity. "Churn equals one minus retention" is a true statement
about matched definitions and a false one about two numbers from two reports.

## Churn rate

- **Numerator:** customers from the starting population who left during the period. A customer
  acquired and lost inside the same period is in neither half; count those on a line of their own.
- **Denominator:** customers at the start of the period. New customers acquired during the period
  do not enter it.

Four variants worth keeping apart:

- **Gross churn:** every starting customer who left.
- **Net churn:** starting customers who left, minus those of them who came back before the period
  closed. A returning customer who left in an earlier period was never in the denominator; count
  them on a reactivation line, or net churn falls on people the period never started with.
- **Customer churn:** counted in people.
- **Revenue churn:** counted in money, so one large departure outweighs many small ones. The
  numerator is recurring revenue the starting customers lost through departures and through
  contraction; the denominator is their recurring revenue at the start of the period. **Net
  revenue churn** subtracts the expansion of the remaining starting customers, which is why it can
  be negative.

**Gross and net revenue retention** are the complements: one minus revenue churn, which cannot
exceed one hundred percent, and one minus net revenue churn, which can. The net forms rise with
price increases and hide contraction inside expansion, so for subscription and B2B read them
beside the gross forms, never alone.

In a business without subscriptions nobody announces they are leaving, so "left" has to be
defined as an absence: no qualifying purchase within a stated window, expressed relative to the
category's median interpurchase interval rather than as a fixed number of days. That definition is a decision
about money, and the skill that acts on it is `lapse-and-winback`.

Three rules that prevent most churn arguments: write down what "customer at the start of the
period" means, count reactivations separately and publish gross and net side by side, and account
for returns and refunds in any revenue-based version.

## Average order value (AOV)

- **Numerator:** revenue in the period.
- **Denominator:** orders in the same period.

Say whether shipping and tax are inside the numerator and how refunds are treated. Read it next
to order count: AOV rises on its own when small orders stop happening, which reads as success
whether or not anything improved.

## ARPU, average revenue per user

- **Numerator:** revenue in the period.
- **Denominator:** active customers in the same period, under the active definition above.

The denominator is the whole story. ARPU over the whole base and ARPU over buyers are different
metrics, and both get called ARPU.

## Lifetime value (LTV)

**No single method is agreed across the industry.** Four families are in use, and they answer
different questions:

- **Gross formula:** averages over the whole base, extrapolating margin and retention forward. Fast,
  and blind to how unlike each other your customers are.
- **Cohort:** value accumulated by customers acquired in one period, followed forward. Slower,
  comparable between cohorts, and the honest way to see acquisition quality.
- **Statistical:** per-customer probability of a next purchase from transaction history.
- **Modeled:** the same, using behavioral data as well; the most demanding, and worth it only where
  you can check its predictions against what earlier cohorts went on to do.

Whichever you use, four things belong in the definition:

- **Revenue or margin.** Both are called LTV. Margin is the useful one and the harder one; say
  which you took.
- **The period and the horizon.** Period is the unit, horizon is how many periods forward. A
  practical horizon stops where roughly the last few percent of value would accumulate; beyond
  that the arithmetic keeps going and the assumptions do not.
- **Matching periods.** Margin and retention must be computed over the same period length, or the
  formula multiplies two different things.
- **A discount rate, if you use one**, and where it came from.

An LTV computed on the whole base is an average over people who behave nothing alike. It is
useful for a strategic total and misleading for a decision about a segment.

## Customer acquisition cost (CAC)

- **Numerator:** the cost of acquiring customers in the period. State what is inside it: media,
  agency, tooling, salaries, discounts given to acquire.
- **Denominator:** new customers acquired in the same period, under a stated definition of new.

Most CAC disagreements are about the numerator, and most CAC comparisons across companies are
worthless for that reason.

## LTV to CAC

The ratio the two metrics above exist to produce, and the one figure on this page with a widely
repeated rule of thumb attached to it. **This library does not carry that rule: it carries no
market benchmarks.** Treat the ratio as a comparison you make against your own history, and if you quote an
outside threshold, quote the source with it or do not quote it.

Both sides have to use matched definitions: LTV on margin against CAC including everything spent
to acquire, or LTV on revenue against media cost alone, but never one of each.

## Incremental revenue

Revenue that would not have occurred without the activity, measured as the difference against a
control group.

Defined here so the word means one thing in this library; measuring it belongs to
`experiments-and-holdouts`. Note the common substitution: "incrementality" gets used to mean
revenue minus cost, which is payback, not incrementality. Payback tells you whether an activity
was worth its cost; incrementality tells you whether the activity caused anything. A program can
be profitable on paper and incrementally worthless, and only the second measurement will say so.

## NPS and CSAT

- **NPS:** on a zero to ten scale, the share of respondents scoring nine or ten minus the share
  scoring six or below. Reported as a number on a scale running from minus one hundred to one
  hundred, not as a percentage. The denominator is respondents, not
  people surveyed, which makes response rate part of the definition rather than a footnote.
- **CSAT:** the share of respondents choosing the satisfied options on the scale you used. Since
  scales differ, the scale is part of the metric. The denominator is respondents here too, so the
  response share goes beside it every time.

The formulas live here. Who to ask, when, how often, and what happens after a low score belong to
`voice-of-customer`.
