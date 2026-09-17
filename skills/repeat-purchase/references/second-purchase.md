---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# The second purchase: the cohort that has no interval of its own

The unit here is **the first purchase cohort for a period**: everybody whose first order closed in
that period, together with everything that happened to them before the window ran out. People
nobody sent anything to are inside it, which makes this denominator wider than any campaign report.

This population has no interval by construction, because an interval needs two points and they
have one. So the mechanic does not run on the consumption of a product. It runs on **the clock of
the relationship**: on how fast a brand is forgotten.

## Entry conditions

The first order is closed, paid and received. The welcome series was cut short by that same event:
`welcome-and-activation` hands somebody over at the moment of the first purchase rather than at the
end of its own window, so there is no gap between the two mechanics and no day on which both write.

## Exit conditions

Named: the window, the number of touches and their spacing, the order of the argument, the channel
cascade, the declared end, and an outcome for everybody who entered the cohort. Nobody in the
cohort is left without one.

## Steps

**1. Measure your own time to second purchase on the cohort, not on the base.** Compute it over
people whose first order closed in a period, including the ones who never came back. A median over
people who bought twice will not do: that is a survivor sample, and it is shorter than the truth by
exactly the people this mechanic exists to reach.

**2. Check that the median exists at all, and take something else when it does not.** If fewer than
half the cohort ever makes a second purchase in any horizon you can observe, the median time to
second purchase is undefined. That is arithmetic, not a property of your market. Take the window
one of two other ways: a percentile your data reaches, or the point at which the return curve
flattens. The second gives you the end of the window as well as its length, since past the
flattening more touches add no more returns.

**3. Name the window and declare what happens after it.** The window is a finite span, not "until
they come back". Past it this mechanic stops working on the person directly and hands them on by the outcome
table in step 10. For somebody with one purchase, the end of this window is also the absence
threshold in `lapse-and-winback`: the neighbor's attempt starts where this mechanic stops and never
runs inside the window. If the two land in the wrong order, somebody computed one of them on the
wrong population.

**4. Leave the start of the window empty and say how long the pause is.** The first days after
delivery carry no touches. The order is still being unpacked and used, there is no reason to write,
and a message competes with the person's own first impression of the purchase. The length of the
pause is a parameter: delivery time plus the time to first use, from your own data.

**5. Split the window into independent stretches instead of chaining a series.** Each stretch fires
on time elapsed since the order closed and evaluates its own condition. A chained series fails
whole when one link does not fire, and it fails quietly: the person never receives the rest,
and nothing in the reporting says so. The sign is in the counts: a later stretch reaches fewer
people than the one before it by more than the people who bought or opted out in between.

**6. Run one route for everybody rather than a route per segment.** Segmenting inside the window
cuts the cohort into pieces that get treated identically under different names, and the overlaps
between them deliver several messages in a day, at which point the performance of any single
message stops being readable. Difference belongs in the content of the touch, which is
`personalization`, not in the number of branches.

**7. Order the argument by what it costs you, cheapest first.** Service first, a rating of the
order or help with using it. Then product, what goes with what they bought and what else exists.
Money last. The reason is not manners: a monetary argument placed first buys the purchases that
were coming anyway and teaches the cohort to wait for a discount. What each rung costs and how deep
it may go is `offer-design`.

**8. One offer per touch.** A discount, a review request, a product selection, a referral scheme
and a loyalty balance in the same message do not add up. They divide attention. One action per
touch, two at the outside.

**9. Build the cascade on reachability and cost.** Channel order follows what the person
has and what a touch costs, free and available first, paid after. Permission is checked separately
in each channel. The overall frequency cap is `contact-orchestration`, applied at send time rather
than when the cohort is assembled.

**10. Stop on the target action, and close every member of the cohort with an outcome.** The target
action is a second closed order, not an open and not a click. The stop is checked immediately
before each send, because somebody may have bought in a store since the stretch was assembled. A
send time check sees that purchase only if the store's data reaches you before the send
(`martech-stack`).

There are five outcomes and each has an address.

| Outcome | Sign | Where it goes |
|---|---|---|
| Bought again | a second order closed inside the window | the interval model: there are two points now, so rung 1 applies |
| Did not buy, still reads | the window ended, there is response in a channel | `lapse-and-winback`, whose absence threshold for a single purchase is the end of this window; on the channel axis the standing program in `email-program` keeps them |
| Did not buy, does not read | the window ended, no response to the touches they got | `lapse-and-winback`, on the same threshold; the tier and its cadence are `email-program` |
| Received nothing | no second order, and no touch reached them: no permission in any channel, unreachable, suppressed by the cap, or held in the control group | `list-building` and `martech-stack` for reachability, `contact-orchestration` for suppression, `experiments-and-holdouts` for the control group. **This is not the mechanic failing to persuade**: they never saw it, so nobody reads them on the channel axis, with no tier move and no step toward leaving the active base. Past the window the `lapse-and-winback` threshold applies to them as to everybody, because the absence of a purchase is real |
| The first order was returned | a return inside the return window | they leave the cohort, because there was no first purchase, and sit with the people who have never bought (`rfm-segments`) until a new closed order puts them in a new cohort |

The last outcome is not a technicality. The whole mechanic rests on a closed order, and a returned
order stops meeting that definition after the fact. What follows for the metric is in `SKILL.md`:
the figure is final only once the return windows on first and second orders and the window itself
have run out for the whole cohort.

## Thresholds and timings

| Quantity | Class | What sits beside it |
|---|---|---|
| The cohort window | 4 | from your own return curve: a percentile you reach, or the point of flattening |
| The pause at the start | 4 | delivery time plus time to first use, from your own data |
| Length of a stretch | 5 | start with stretches of a quarter of the window and one touch each; it applies to windows longer than a month, and below that the stretches collapse into single touches; revise it when the response to a stretch's second touch is indistinguishable from noise |
| Number of touches | 4 | derived from the window and the length of a stretch, never assigned |
| The absence threshold after the window | not here | `lapse-and-winback` |

## Edge cases

- **A second order inside the pause.** Somebody buys again on the third day. The mechanic never
  starts and they move to rung 1 of the interval model. What gets checked is not whether the series
  finished but whether a second closed order exists, and it is checked before every send.
- **The first order is a gift card.** The order is closed, nothing has been used yet, and the person
  who uses it may be somebody else. The buyer's clock runs from the closed order like anybody's;
  whoever redeems the card, once you can identify them, enters a cohort on that order as their own
  first purchase. A pre order needs no edge case: it is not closed until the person receives it.
- **The first purchase was made in a large promotion.** A cohort recruited in a sale behaves
  differently and distorts a window computed on ordinary periods. Compute the window for such a
  cohort separately. Tell the entries that came out of a sale by the occasion tag in the register
  `promo-calendar` publishes; how the windows overlap is that neighbor's.
- **The person is already in the loyalty program.** Enrolling is not a second purchase and does not
  remove anybody from the cohort. Membership of the cohort follows from the order, not from the
  registration.
- **The first order is returned after the window closed.** The cohort is recomputed after the fact
  and what was sent is not recalled. So the outcome is fixed at the end of the window while the
  membership of the cohort is fixed at the end of the return window.

## Failure modes

**The cohort is too small to read a result from.** The sign is that the share coming back swings
between periods by more than the whole effect you are looking for. Read a rolling window of several
periods rather than one period, and do not run message variants on a cohort of that size at all: a
test on it shows nothing (`experiments-and-holdouts`).

**Touches go out and the stop does not work.** The sign is complaints from people who bought
recently. Two causes produce it, and one question tells them apart: was the second order visible
in your system at the moment of the send? If it was, the stop is evaluated when the stretch is
assembled rather than before the send, the same defect as step 6 of the interval model with the
same fix. If it was not, the purchase reached you after the send, a store purchase in an overnight
export, and no send time check can see it; the fix is the freshness of that source
(`martech-stack`).

**Several messages arrive on the same day from different systems.** Service notifications, the
loyalty program, a referral scheme and a call from the contact center do not see each other. This
is not a defect of the series and it cannot be fixed inside the mechanic: the subject belongs to
`contact-orchestration`. It is named here because the first order is an event several of those
systems start on, service notifications among them, so this cohort is where the missing shared
count shows up early.
