---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Shaping the flow: steps, intervals, channels

A step costs more than it looks. Each further step reaches fewer people who act on it, while
everyone who entered the flow pays for it in attention, unsubscribes and sender reputation. Ask of
step three what it answers that step two did not, and drop it when the answer is nothing.

This mechanic starts once the trigger is defined and ends with a flow you can explain step by
step.

## Entry conditions

- You have defined the trigger: firing event, eligibility, delay, recheck and exits are written
  down.
- At least one message exists and you can name the objection it answers.

## Exit conditions

You have written down the step count, the intervals, the argument each step carries, the channel
order and the stop conditions. Each step carries one argument. For each step you know what counts
as a response, and what happens when the object the flow is about changes mid-flight.

## Sequence

**1. Start with one step.** One step is a working mechanic, not a draft. Add the second when you
can name the question the first one left unanswered.

**2. Give each step one argument.** Reminder, then help with the decision, meaning reviews,
comparison, delivery terms, an offer to answer questions, then a money argument. Two arguments in
one message cancel each other. The same argument twice in a row reads as pestering rather than as
persistence.

**3. Decide whether a money argument appears at all, and at which step.** On the first step it
pays for conversions you would have had for free, and it teaches people that abandoning a cart
produces a code. Incentive depth belongs to `offer-design`. You decide its position in the
flow here.

**4. Set the intervals from the decision cycle.** The first interval is the shortest and does most
of the work; later ones stretch. The whole flow fits inside the decision cycle. A message
arriving after the person bought elsewhere does more than miss: it tells them you were not paying
attention.

**5. Order the channels from cheap and mild to expensive and insistent.** A high-cost channel with
a high consent bar enters only when the cheaper one failed to land. Ordering by preference instead
of by cost is how a flow spends its margin on people who would have answered the free channel.

**6. Say what counts as a response at each step.** A cascade that waits on an open escalates to
the paid channel for no reason: prefetching by a mailbox provider records opens no human made, and
filtering those out on the platform side moves the count the other way. Waiting on a click, or on
the conversion itself, is sturdier.

**7. Write the stop conditions.** Conversion, an order placed, the reason disappearing (cart
emptied, item bought, price back up), entry into a higher-priority flow, a reply from the person,
an unsubscribe, a withdrawal or deletion request. Check them before every step rather than only at
entry. The last two stop the steps already in the queue, not only the ones nobody has scheduled
yet.

**8. Trim by contribution.** Count conversion per step, not per flow. A step that adds visible load
and invisible conversion comes out. Read each step on a window that covers that step and the wait
its response needs: on a window that closes before a step, that step counts as zero whatever it
did.

## Thresholds and timings

- **The first step** goes out at the end of the session plus the delay from the trigger definition.
  It is the only step whose timing comes from behavior; the rest are counted from it.
- **The interval between steps** is a fraction of the category's decision cycle. An identical
  interval across every flow in the set is a sign that nobody chose it.
- **Flow length.** Start at one, add one at a time, stop where the next step no longer pays for the
  load it adds. The ceiling is not a number: the flow stays shorter than the decision cycle, and
  shorter than what the team can maintain.
- **The wait inside a cascade** comes from how fast the channel gets read. A channel read in
  minutes waits minutes. A channel read in hours waits hours. An identical wait in every channel
  means you have a volley rather than a cascade.
- **The recipient's local time.** Messages go out during that person's waking hours. A paid channel
  firing in the middle of their night turns a useful reminder into a complaint faster than any
  wording can. Quiet hours across the whole program belong to `contact-orchestration`; sending in
  local time is a property of being timely, and it stays here.
- **The lifetime of any offer inside the message** matches the length of the flow. A code that
  outlives the flow removes the reason to hurry. A code that dies before the next step makes the
  next step pointless.

## Edge cases

- **The person bought between steps, in another channel.** Stop on the order, not on a click inside
  your message. Flows that check only their own clicks keep sending to customers who are already
  unpacking the box.
- **The object changed mid-flow.** The item sold out, the price returned to normal, the product was
  delisted. Either stop the flow or switch to a branch you wrote in advance that offers
  alternatives. Continuing silently is the one option that is never right. A branch that offers a
  different product is a marketing message, so check the basis before it goes out, on the terms in
  the next case.
- **The occasion never arrived.** Someone subscribed to a price drop and the price never dropped.
  That is a branch, not an error: on timeout, send the message that says there is nothing left to
  wait for. Without it the subscription dies quietly and the person assumes you ignored them. What
  that message may carry depends on what they gave you. Subscribing to one event is a request for
  one message, not permission for a program, so a substitute offer rides along only where the
  person holds a marketing state, or where the request itself named alternatives. Where it does
  not, the closing message ends the subscription cleanly and offers the program as something to
  choose deliberately. Which basis allows what is `consent-and-preferences`; the states a capture
  point produces are `onsite-capture`. What stays here is running the check before the substitute
  goes out rather than after somebody complains.
- **The event repeated while the flow was running.** They filled the cart again. Decide once for
  the whole set: restart, extend, or ignore. The worst option is a second copy of the flow running
  in parallel.
- **The flow lands during a site-wide sale.** A personal code is weaker than the public discount,
  and the message reads as an insult. Suspend the money step for the duration or replace it. The
  order between layers stays as it is: the flow still goes before a campaign on the same day
  (`email-program`).
- **The expensive channel is unavailable.** No consent, no number, no approved template. The
  cascade has to end cleanly instead of parking the person on a step that will never execute.
- **A push step for a person with no displayable endpoint.** The push does not go out, so there is
  nothing to wait for: skip the step at once. Delivered means something different for push on each
  platform, so wait on a tap or a conversion, as step 6 says (`push-notifications`).
- **A long consideration cycle.** The conversion arrives after the reporting period closes. Judge
  the flow on an intermediate response and write down that you are doing so, because an
  intermediate metric nobody wrote down ends up treated as the target.

## Failure modes

- **Unsubscribes concentrate on one step.** Visible only when you read the flow step by step. The
  flow average hides it. Tell it apart from load across the set (`trigger-set-and-collisions.md`)
  by reading the same unsubscribes against how many automated messages each person received that
  day: concentrated on this step whatever the count points here, rising with the count points to
  the set.
- **The money argument moved to step one** during an optimization, and conversion rose together
  with the share of discounted orders. The flow now pays for what it used to get free.
- **People learned to abandon carts.** The abandonment rate rises alongside the share of orders
  that use a recovery code. Check by repeat behavior: the same people entering the flow again and
  again, buying only with the code.
- **The cascade escalates for everyone.** The "did not respond" condition is broken or unchecked,
  so the paid channel goes to the whole flow. Costs rise and orders do not.
- **The flow is longer than the decision cycle.** The last steps reach people who decided long ago.
  Their conversion is indistinguishable from zero and their load is full price.
- **Every step repeats one argument.** A chain on paper, one message sent three times in practice.
