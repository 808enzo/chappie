---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# The interval model: where the date of the next purchase comes from

The unit here is **one person against one subject**. A subject is a product, a product variant or
a category, and which of the three you picked is decided in step 1 and never changes quietly. The
same person can be due on cat food and early on shampoo, and that is not a contradiction: those
are two subjects.

This file computes a date. It does not fire on it. Firing, the delay, branching and the
cancellation of a running flow are `triggered-messages`, which knows what to do on a date and has
no way to work out which date.

## Entry conditions

Order history is stitched across every sales channel (`list-building`, `martech-stack`), and the
event that closes an order is known: paid and received, not placed. The catalog supplies at least
one of two things, either how long one unit of the product lasts or a category on which an interval
can be computed.

## Exit conditions

Named: the level of the subject, the source of the interval and the substitution ladder, the
advance, the events that recompute or retract a date, and the categories where the
mechanic does not get built at all. The date is reproducible: two people computing independently
get the same one.

## Steps

**1. Name the level of the subject, and name one.** The level decides what counts as the same
purchase again. The same brand in the same pack size is a variant; any brand of that food is a
category.

The default mistake is to compute the interval on the whole receipt. Somebody shops weekly and
buys this particular product once a quarter, so a receipt level interval sends the reminder weeks
early, every time.

**2. Take the interval from the highest rung whose condition is met.** There are four sources and
they form a ladder from measured to estimated. Step down only when the rung above fails the
condition in the middle column: too few observations on rungs 1 and 3, an empty field on rung 2.

| Rung | Source | What the rung needs | What it yields |
|---:|---|---|---|
| 1 | This person's own history of this subject | at least two closed purchases of it | this person's interval |
| 2 | A catalog field: how many days one unit lasts | the field populated, and the quantity on the order | this purchase's interval |
| 3 | The median across your own base for the subject or category | enough people who bought it twice | the subject's interval |
| 4 | The person's own answer, or published research on how long a unit lasts in use | a question asked, or a study found | an estimate, labeled as one |

**Everybody below rung 1 has exactly one purchase of the subject.** Two purchases put a person on
rung 1, and with none there is nothing to remind them about. So rungs 2 to 4 serve one population,
and what separates them is how each goes wrong on it.

- **Rung 2 comes first because it counts consumption rather than people**, so it carries no bias
  from who came back. That, rather than rung 3, is the answer to where a single purchase gets its
  date.
- **Rung 3 errs in one known direction.** It takes a median over people who bought the subject
  **twice**, which is to say over people who already came back, and hands a single buyer the
  interval of the survivors, which hurries them. Use it only with a reminder worded as a question
  and with the deferral in step 5, and store which rung the date came from.
- **Rung 4 is an estimate.** Label it as one wherever you show it internally, because the next
  person to read the field will otherwise treat it as measured. A published purchase cycle for a
  category is not rung 4: the Limits in `SKILL.md` rule it out.

**3. Put the interval on the quantity bought, then subtract the advance.** Rung 2 yields days per
unit, so multiply it by the quantity on this order. Rungs 1 and 3 yield days per purchase, and
each gap already carries the quantity of the purchase that opened it: divide the gap by that
quantity first, then multiply by the quantity on this order. Multiplying a per purchase interval
straight away counts the quantity twice. Where the level is a category whose items come in
different sizes, a unit is not comparable across them, so keep the per purchase interval and do not
multiply.

The reminder date is not the order date plus the interval. Two quantities come off it, and both are
parameters you compute from your own data:

- **room to decide**: how many days somebody needs to place the order before the product runs out.
  Compute it as the time from message to order among the people who have responded to this kind of
  message. Before this mechanic has run there is no such message, so take the same measure on the
  nearest message you already send, a back in stock notice or a cart reminder, and replace it once
  the mechanic has run for a full interval;
- **delivery time to this address**: as many days as the goods take to arrive. It varies by
  location, and it is the only quantity in this mechanic that depends on where the order is going
  rather than on what was in it.

Two people who bought the same thing on the same day get different dates. That is the mechanic
working, not two systems disagreeing.

**4. Recompute on an event, never on a schedule.** Three events move a date: an order containing
the subject closes; the order that produced the date is canceled or returned, which retracts it;
and the value behind the date changes, a corrected catalog field for a rung 2 date or a refreshed
median for a rung 3 one. A scheduled sweep over the base is the wrong shape: it recomputes
everybody to catch the few whose inputs moved, and it reaches them only at the next sweep.

**5. Let the person move the date, and store what they said.** The message carries a way to push
the reminder back. That answer outranks the model: it comes from somebody looking at what is left
in the cupboard, and the model is looking at a catalog field. Store the shift against the pair of
person and subject, and carry it through the next recompute.

**6. Check the date at send time, not only at compute time.** A whole interval passes between the
two. In that gap the subject can go out of stock, the price can change and the person can
unsubscribe. Three conditions get rechecked immediately before sending: permission in the channel,
availability of the subject, and that the order which produced the date has not been canceled or
returned.

## Thresholds and timings

| Quantity | Class | What sits beside it |
|---|---|---|
| Two closed purchases before rung 1 applies | 3 | an interval is a gap between two points and is undefined on one |
| Room to decide | 4 | time from message to order among people who responded to this kind of message, over a period in which the mechanic was already running; before launch, the same measure on the nearest message you already send |
| Delivery time to the address | 4 | from your own delivery data, cut by location |
| Observation threshold for rung 3 | 5 | start with no fewer than thirty people who bought the subject twice; it applies where the category is bought more often than once a quarter; replace it once the spread of the median across subsamples is smaller than the advance, because at that point the median is stable enough to use on a narrower cut |
| Two to three median intervals after launch before you read the signed miss | 5 | start there; until then only the fastest buyers have a next purchase to compare, so the miss reads early; it applies where the cycle is stable, and in a category bought once a year it means two to three years of waiting; revise it whenever the interval itself is revised |

## Edge cases

- **A gift.** Somebody bought what they will not use themselves. That order's interval is not
  theirs and a reminder on it means nothing. The signs are a different delivery address, gift
  packaging, or a one off purchase in a category where this person has no history. Do not compute a
  date, and do not go silent either: the subject moves to the add on mechanic, where the reason to
  write is not consumption.
- **Quantity above one.** Two packs last twice as long as one. Putting the interval on the quantity
  (step 3) is not optional, or the mechanic writes to somebody on the day they open the second pack.
  Doing it to an interval that already carries the quantity sends the reminder late.
- **The same thing bought somewhere else.** Your own order history cannot show it, so no rung of
  the ladder accounts for it. The fix is in the wording of the reminder: one written as a question
  survives being wrong, and one written as a statement about what is in somebody's house does not.
- **The subject is discontinued.** The date arrives and there is nothing to sell. Substitute at the
  same level, and where there is no substitute send nothing. A reminder pointing at a dead page is
  worse than silence.
- **The order is canceled or returned.** The date computed from that order is retracted. If the
  return lands after the reminder went out there is nothing to retract, which is a second reason to
  hang the computation on the order closing rather than on the order being placed.
- **A category with no consumption cycle.** Furniture, large appliances, a service with a one time
  result. The mechanic does not get built: no rung of the ladder yields an interval, and an
  invented one produces a date that means nothing.

## Failure modes

**No rung of the ladder yields an interval.** History is not stitched, the catalog field is empty,
too few people bought the subject twice, and no study exists. Say that there is no interval rather
than assigning a number out of an article. Where this was the person's first order, the work does
not stop: they are already in `references/second-purchase.md`, which runs on the clock of the
relationship rather than on the consumption of a product and needs no interval at all. Where they
have bought other things before, that mechanic does not take them, because its cohort is defined by
the first order and not by the first purchase of a subject. This subject gets no reminder, and the
person stays with the standing program.

**The interval outlives the basis for sending.** Where a category's interval is longer than the
term of the permission you are sending on, the model produces a date by which that permission has
lapsed. The model is not what failed here: the date is right and sending on it is not allowed. Ask
for express permission while the basis still stands rather than sending on an expired one. The
terms, which of them expire at all, and the edges of each regime are in `SKILL.md`.

**History is stitched only partly.** Some purchases sit in another system and the interval is
computed over a subset. This one has a distinctive signature: the interval comes out **longer**
than the true one, because the invisible purchases stretch the gaps between the visible ones. The
reminders therefore run late rather than early, which is why nobody complains and why this failure
is invisible in feedback. It is caught by reconciling the order count in the system against the
order count at the till. The signed miss described under the control metric in `SKILL.md` does not
catch it: it reads the next purchase from the same partial history and finds the interval on
time.
