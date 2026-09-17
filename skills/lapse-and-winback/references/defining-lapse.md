---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-09
---

# Defining lapse: the qualifying action, the threshold, and who is out of scope

The unit here is **one person against one qualifying action**. The same person can be lapsed on
one action and active on another, and that is not a contradiction: it is two different subjects.
Mixing them produces the message that tells somebody you have not seen them in a while, sent on
the day they walked out of your store.

## Entry conditions

The history of the qualifying action is stitched across every sales channel (`list-building`,
`martech-stack`), and you know your own interpurchase interval for the category, at least the
median (`repeat-purchase` defines the interval, `rfm-segments` computes it on the base).

## Exit conditions

Named: the action, the threshold, the threshold steps, the part of the population that is out of
scope, and the rule for rechecking recency at selection. The list of lapsed people is
reproducible: two people building it independently get the same set.

## Steps

**1. Name the qualifying action, and name one.** Lapse is the absence of the action the business
keeps people on the list for: a purchase, an order, a login to the product, a use of it. The
answer follows from the business model rather than from the channel you happen to run.

The default mistake is to define lapse by the absence of email response when the business sells
purchases. That measures the state of the channel, not the state of the relationship.

**2. Separate the two axes of absence, and never mix them in one segment.** The two produce
different populations with different target actions:

- **commercial silence**: the qualifying action stopped. The target action of an attempt is that
  same action;
- **channel silence**: opens and clicks stopped. The target action is a response, and the outcome
  is different: not revenue, but a decision about whether the address stays in the active base.

Somebody can sit in one axis and not the other. Whoever buys in the store and never reads email
has not lapsed. The channel has.

**Neither axis outranks the other, because they answer different questions.** The commercial axis
decides whether the person is gone. The channel axis decides which route can still reach them and
what happens to the address.

People ask this as a question about which silence threshold wins. The answer lands differently on
each of the two thresholds, so take them one at a time.

- **The engagement tier in `email-program` sits on the channel axis.** It is computed from recency
  of response inside one channel, so it does not answer "has this person lapsed" at all. Different
  axis, different question, and no contest to settle.
- **The silence threshold in `list-building` sits on this same commercial axis**, which is where a
  seniority contest looks real. It requires no reaction *and* no purchase across two of the
  person's own intervals, and the no purchase half of it is commercial silence. It is not a rival
  answer to the same question: it is the same axis read at a later point, a threshold of **ending**
  against the one computed here, which is a threshold of **starting**.

That leaves an ordering check rather than a ranking. **The entry threshold you compute here has to
fall earlier than the deletion threshold in `list-building`**, and one median interval plus a
tolerance against two median intervals leaves the attempt room to run between them. If the two land
on top of each other, one of them sits on the wrong population, and you can schedule neither the
attempt nor the cleanup until you find out which.

**3. Derive the threshold from your own distribution rather than assigning it.** The threshold is
a multiple of your own median interpurchase interval for the category, not a number of days
borrowed from somebody else.

The recipe: pull the intervals between consecutive purchases over a period covering at least two
typical cycles; take the median rather than the mean, because a tail of long intervals drags the
mean upward and pushes the threshold past the point where an attempt is still worth making; the
entry threshold is one median interval plus a tolerance.

The deletion threshold is a different number on the same axis, read later: two of the person's own
intervals with no reaction and no purchase (step 2). Everything this skill does happens between the
two, and the ordering check is what protects that room.

**4. Have as many threshold steps as you have distinguishable routes, and no more.** One step is
one attempt with one set of content. Running four steps is worth it exactly when each has its own
argument or its own channel cascade. Otherwise they are four names for one message, and the extra
names cost a segment each.

Steps are computed **per segment, not per base**. Where categories have different purchase cycles,
a single threshold for everybody means the attempt fires before the person intended to return in
the slow category and two of their cycles too late in the fast one.

**5. Subtract the part of the population that is out of scope before you size anything.** Four
classes, each derived from a state rather than from a guess about mood:

- **out of the category by fact**: the product no longer fits, or the need was met once and does
  not recur. Children's clothing and a child who grew is the clean case;
- **said so out loud**: unsubscribed, refused, asked you to stop. They get no attempt, and the
  reason is legal rather than tactical (see the legal section of `SKILL.md`);
- **natural departure**: moved away, circumstances changed. It differs from the others in that
  nothing in this skill's toolkit addresses it;
- **a model with no return in it**: the purchase cycle is longer than any defensible attempt
  horizon.

If what remains after the subtraction is small or empty, the mechanic does not get built, and that
is an honest answer rather than a failure. Write it down the way a rejected row gets written down
in the register `scenario-map` keeps.

**6. Recheck recency at selection instead of trusting the snapshot.** A group assembled from a
snapshot (`rfm-segments`) is already wrong for part of it by the time the send goes: somebody
bought yesterday. The rule: the recency of the qualifying action is reread immediately before the
send, and where it disagrees with the snapshot, **the message does not go and the group is not
reassigned**. The assignment is frozen at assembly, and what enters the log is a suppression
rather than a move.

This is the same check `welcome-and-activation` runs from its own side for a series broken by a
purchase. One rule seen twice: the snapshot a send was assembled from is not a basis for sending
it.

**7. Split the outcome of the attempt from the fate of the record.** This skill finishes the
attempt and hands over an outcome. Removal from the active base and deletion of the record itself
are two tiers owned by `list-building`. The obligation from that side is discharged here: the
attempt has an end, and its last message says what happens next.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Entry threshold | your own median interpurchase interval for the category, plus a tolerance |
| Number of threshold steps | the number of distinguishable routes, not round calendar numbers |
| The cut the threshold is computed on | a segment with its own purchase cycle, not the whole base |
| Deletion threshold | owned by `list-building`: two of the person's own intervals with no reaction and no purchase |
| Moment recency is rechecked | immediately before the send, not at assembly |

## Edge cases

- **One purchase, so no interval.** A median needs intervals and this person has none. Their
  threshold is the end of the cohort window in `repeat-purchase`: time to second purchase measured
  on the whole first purchase cohort, which is a different quantity on a different population. Not
  a median over people who bought twice, which is a survivor sample and lands inside that window, so
  an attempt here would start while the second purchase mechanic is still writing. Until the window
  ends the person belongs to `repeat-purchase`, not to a win-back. Do not reach for the no history bucket in `rfm-segments` here: that bucket holds people
  with zero purchases and splits on time to first purchase, and that neighbor calls a win-back offer
  to somebody who never bought a mistake.
- **A seasonal category.** The interval is not constant, and a threshold computed on a yearly
  median catches people in the off season. Compute the interval inside the season, or shift the
  attempt window so it does not land in the trough.
- **A return or a canceled order.** Whether such a purchase counts as the qualifying action is a
  decision made once and written into the definition (`metric-definitions`). Left unwritten, it
  drifts apart between the report and the selection.
- **An offline purchase while the channel is silent.** The two axes give opposite answers. The
  first one decides: the person has not lapsed.
- **A lapsed segment that never empties.** The sign that the threshold is set so wide that more
  people enter than the attempt can process. Narrow the threshold or split the step.

## Failure mode

**A threshold borrowed from somebody else's category.** From the outside everything works: the
segment fills, messages go, there are conversions. Inside, the attempt is reaching people who were
never leaving, because their purchase cycle is longer than the threshold.

Two things show it. The share of returners whose pre-attempt interval was shorter than the
threshold is large. And the share of people who came back with no touch at all, held out as a
control, does not differ from the share among those who got one.

The second of those is shared with the failure mode in `return-attempt.md`, where the attempt has
turned into a discount channel, and the repair there is the opposite of the repair here. The
interval reading separates them: intervals sitting below the threshold from the first attempt
onward mean the threshold is borrowed, while intervals that used to sit below it and have drifted
up toward it mean people learned to wait.

The repair is to recompute the threshold from your own median and to date it. It drifts with the
assortment and the price, so a threshold with no date on it is a threshold nobody will revisit.
