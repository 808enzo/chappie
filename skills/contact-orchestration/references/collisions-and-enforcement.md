---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Collisions, enforcement, revision

The policy starts existing at the moment two messages want the same person and a machine settles
it. Until then it is a document.

## Entry conditions

The policy is written: classes, precedence, caps, windows.

## Exit conditions

- The system checks the rule at the moment of sending, and when two candidates arrive at once, one
  of them holds a claim and the other does not.
- Every held message lands in a log.
- You know the share of sends the policy holds for each stream.
- You review the policy on a schedule and on signal.

## Steps

**1. Check at the moment of sending, not when the segment is assembled.** Between assembly and
send, the person receives a triggered message, and the campaign lands an hour later. The question
"how much has this person already received, and of what" gets asked when the message goes out.
Asking late is necessary and not sufficient. Two systems can ask in the same second, read the same
count, and both send. The person is now one message over the cap, and neither system broke its own
rule. A check holds only when you reserve the answer: count the cap against reservations rather than
against receipts, and release the reservation on a confirmed failure so that it costs the person
nothing. A reservation is a row in the contact log written before the send; step 3 writes the same
kind of row for the pitch, keyed on the pitch as well.

**2. Choose between three outcomes: pass, defer, drop.** The difference carries weight.

- **Drop** suits anything that will run again: a recurring promotion, a roundup, a digest.
- **Defer** suits anything that does not spoil while it waits.
- **Perishable messages are dropped, not deferred.** A personal offer that arrives late arrives
  dead, and it devalues the next one.
- Deferral has a side effect of its own: the held message is checked again when it lands and
  consumes the cap there. The same is true of quiet hours, where a message held until morning is
  checked against the cap as it stands in the morning. On a rolling window, a few hours later the
  window still holds the touches that caused the hold, so defer to the moment the window frees a
  slot, not to a fixed hour. Deferral moves load, it does not remove it.

**3. Deduplicate the pitch, not the profile.** If the same argument already reached a person in one
channel, it does not repeat in another. A person who qualifies for two flows carrying the same pitch
gets one; the second flow either drops out or gets replaced by another scenario the person also
qualifies for. Merging duplicate records of one person is a different job and belongs to
`list-building`.

Reading delivery and read history does not make that hold, because a message in flight sits in
neither. Both systems see an empty history and both send. Deduplication needs a claim written before
the send, not a fact observed after it.

- **Claim the pitch, then send.** The key is the person, the pitch and the window, and whoever gets
  there first writes it before anything reaches a channel. A second candidate on the same key finds
  the claim and drops or defers by step 2. Take the key from the event that triggered the message,
  so that reprocessing the same event finds its own claim and sends nothing.
- **One place holds the claims.** Two platforms with separate stores cannot deduplicate a pitch
  between them, however carefully each one reads its own history. Either they share a store, or one
  of them owns that pitch and the other does not carry it.
- **Four states, not two.** A claim is *reserved* (nothing has left yet),
  *in flight* (handed to the channel, no receipt), *delivered* (a receipt arrived), or *unknown*
  (the receipt window closed empty). Delivered is the only state that proves the pitch reached the
  person. Inside a product the receipt is the display: a queued message stays in flight until it
  shows, and expiring unseen is a confirmed failure that releases the claim (`in-product-messaging`).
- **A claim expires, and a confirmed failure releases it early.** Give every claim a lifetime.
  Without one, a sender that dies mid-send silences that pitch for that person until somebody
  notices by hand. A hard bounce or a rejected send means nothing landed, so release the claim and
  let the second flow have it.
- **Decide what unknown means and write the decision down.** Counting unknown as delivered protects
  the person and quietly loses messages. Counting it as not delivered recovers those messages and
  doubles some. Neither is safe as a blanket rule, so split it by what the message is for: unknown
  counts as delivered for anything the cap exists to protect the person from, and as not delivered
  for a message the person is waiting for.

**4. Collapse overlaps instead of arbitrating forever.** When two flows have argued over the same
people for months, merging them into one flow with a condition costs less than choosing every
time. What competes for the same people is normally copies of one mechanic carrying different
conditions, so merging them ends the arbitration instead of repeating it every week.

**5. Log what was held.** Suppression without a log is indistinguishable from a breakage. For each
stream, track the share of sends the policy held. A stream where most sends are held is either
redundant or sitting too low in the table, and both are decisions rather than observations.

**6. Revise.** On schedule, once per planning cycle. On signal: reachability loss rising, revenue
per reachable person falling while load holds steady, the held share climbing, or campaign owners
reporting that their messages never arrive.

**7. Treat a cap change as an experiment.** The design belongs to `experiments-and-holdouts`,
which also records that the unit is the person over a period, that the window runs longer than a
content test, and that the guardrail moves later than revenue. What stays here is the decision:
which reading changes the cap, and by how much.

## Thresholds and timings

- Check the cap at the moment of sending, and for a multi step flow, at every step separately.
- Maximum deferral: the message's shelf life, counted from the event that created it, not from the
  moment of the hold. Past it, the message is dropped. An unbounded queue of deferred messages is a
  volley in storage.
- Measure the cap in deliveries and enforce it against reservations. The two agree as long as a
  confirmed failure releases its reservation. They never agree if you wait for a receipt before
  counting, because everything in flight is then invisible to the next check.
- Set the lifetime of a reservation or a claim from the delivery window of the slowest channel it
  covers, plus the time a receipt takes to arrive. Set it longer and one failed send blocks that
  pitch for the rest of the period; set it shorter and the same offer goes out twice.
- A held share above half for one stream is grounds to reopen the stream itself. Half is a starting
  point we chose: keep it until your own history contradicts it, then write down what replaced it
  and why.
- The channel's technical ceiling (a handful of messages to one number inside a short window,
  with the next one refused) sits below the marketing cap. The channel and the cost of abuse
  dictate it, not the policy.

## Edge cases

- **A held step stopped the flow.** The most expensive failure here: the message did not go, the
  flow treats that step as pending, and the next step never fires. The rule is that suppressing a
  step does not stop a flow: the flow continues from the following step. A silent flow looks
  identical to a healthy one from the outside, and catching it belongs to `program-audit-and-ops`.
- **Two systems, two stores, no shared claim.** Say this one out loud instead of describing a
  guarantee the stack does not give: with nowhere to hold a shared claim, deduplicating a pitch
  between those two systems is best effort and stays that way. The reliable repair is to give each
  pitch one sending system. Whether the stack can hold a shared claim at all belongs to
  `martech-stack`.
- **Two messages of the same class and the same precedence.** Break the tie on signal freshness,
  then on how specifically it is addressed, then on channel cost, with the cheaper channel winning.
- **A notification the person asked for** ("tell me when it is back") is not held by the cap. They
  are waiting for it, and their own action created it.
- **Manual sends outside the platform.** These always exist. Put them in the register as a stream
  with an owner, or the policy stays true on paper and false in the inbox.
- **The same person is held over and over.** Someone who constantly hits the ceiling falls into
  every stream at once. That is a signal about overlapping flow conditions, not about the cap.

## Failure modes

- **A person enforces the rule.** A marketer looks at the calendar and decides what to move. It
  does not scale, it breaks during vacation, and it leaves no log. The symptom: the rule is
  written down and absent from every system a send passes through.
- **You process one event twice and send twice.** Tell: duplicates cluster around retries and
  restarts rather than around campaigns. The claim key came from the send attempt instead of from
  the event that caused it, so the retry wrote a second claim and honored it.
- **The same stream is always the one held.** Whatever sits at the bottom of the table never goes
  out. It is dead and still counted as live in reports.
- **The cap holds and the base still feels flooded.** Then the problem is composition, not volume:
  the person receives their allowance and every message is about the same thing. Vary the
  occasions, not the ceiling.
