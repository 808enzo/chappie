---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Defining one trigger

A trigger is a rule that binds a moment to a reply. It outlives the message it sends: the copy
gets rewritten every season, the rule runs untouched for years. That is why an error in the rule
costs more than an error in the copy. A bad subject line is visible to whoever reads it. A bad
eligibility filter is invisible to anyone reading the messages, including you: only the count of
entries against fire volume shows it.

This mechanic ends with a written definition, not with a scenario switched on in a platform.

## Entry conditions

- The event is captured at the level of a person, not as an aggregate. A report saying how many
  carts were abandoned last week does not let you write to anyone.
- The person is addressable. An anonymous session gives you a statistic and nobody to send to.
- You can say what the person does next and how the message helps. If the message repeats what
  the site already shows, there is nothing to send.

## Exit conditions

You have written the definition in full: firing event, eligibility filter, delay, the object the
message carries, the recheck before sending, the exit conditions, and the age past which the
event stops counting. The delay comes from the category's decision cycle, and you have named the
retirement condition.

Deciding not to build the trigger is a normal outcome of steps 1, 3 and 4.

## Sequence

**1. Start from the moment, not from the list of events.** Say what the person just did, what
they do next, and what the message adds. An event you have no answer to is not a trigger. The
platform's catalog of ready-made scenarios is a menu, not a plan: it tells you what is
technically possible and says nothing about what is worth sending.

**2. Name the trigger's origin.** Five kinds, and each brings its own guard:

- **A customer action.** Viewed an item, opened a category, added to cart, started checkout. The
  event ages in hours.
- **A catalog change that concerns this person.** Back in stock, price drop, stock running low on
  something they saved. The object can change between firing and sending, which makes step 7
  mandatory. The change is new; the interest behind it may be old, which is why the age in step 5
  is counted from the person's own action.
- **A date that arrives.** Birthday, anniversary of a first purchase, expiry of a service,
  an upcoming appointment. The attribute is self-reported, editable and worth gaming, which makes
  the once-per-period guard mandatory.
- **A short-horizon absence.** Started checkout and did not finish, received a code and did not
  use it, subscribed to an alert and did not come back. An absence fires it, and the horizon is
  tied to an action already started.
- **A state the program records or computes.** An order delivered, a conversation closed, a
  customer moving from one group of a grid to another. The state belongs to another system's map,
  and that system is the owner named in part 4 of the definition. A transition computed from data
  gets the axis that produced it rechecked before anything fires on it (`rfm-segments`). An ask for
  feedback fires here: its delay runs from the closing state to the point where a defect of that
  kind of experience can show, and it carries its own ration per person (`voice-of-customer`). An
  ask sent a fixed number of days after the order is the failure.

Long-horizon absence, meaning someone who stopped buying or stopped opening altogether, belongs
to `lapse-and-winback`. The line runs through whether the person started a specific action you
can bring them back to.

**3. Check the event fires the way you think it does.** Establish three things: how many times
one session produces the event, what marks the end of a session, and how far back the stack keeps
event history. An open tab is not an abandonment: while the person can still
come back, nothing has happened yet. An event that fires several times per visit sends several
messages about one thing, and it does that from the first day, quietly.

**4. Check there is someone to answer.** For an anonymous visitor there is no address, and the
highest-converting trigger in the shop does not exist for them. Either the flow includes a point
where the address is collected, such as a form on an out-of-stock item page or an offer to send
the cart to an inbox, or you state plainly that the trigger only works for known customers.
Collection belongs to `onsite-capture`. You specify the reason to collect here, because only the
intended flow knows what is missing.

**5. Write the definition as a rule.** Seven parts, and people skip the sixth and the seventh:

1. the firing event;
2. the eligibility filter, meaning who is dropped before the first message;
3. the delay;
4. the object the message carries, and the system that owns it;
5. the exit conditions;
6. **the recheck before sending**, meaning what you verify between firing and delivery;
7. **the age past which the event stops counting.**

**6. Derive the delay from the category's decision cycle.** The platform default is a reasonable
starting point and a poor constant. The closer the event sits to a purchase, the shorter the
delay. The weaker the signal, the longer you wait, and the higher the chance that answering at
all reads as surveillance.

The decision cycle sets the delay you want; the source sets the delay you can have. A trigger
cannot fire faster than the freshness class of its firing event, which is how long after the
action that event becomes visible. Shorten the delay past it and the flow still runs, on a state
the person has already left. Check the class before you name the delay: `martech-stack` owns it
and writes it beside the event.

**7. Set the recheck before sending** for everything that could have moved: availability, price,
whether the cart is still unpaid and not emptied, consent still in force, and whether the person
has already bought. Use the recheck for two decisions: whether the message still goes, and which
live values it quotes. Do not re-read the event itself. The cart in an abandoned cart message is
the fact the message is about, so it stays as it was at firing (`personalization`); re-read at
send, it describes an empty cart. A live value assembled at firing time and delivered later is
wrong in exactly the share of cases where it changed, and it is the most expensive kind of wrong
in the channel, because it arrives looking like attentiveness.

**8. Name the exit conditions before launch.** Purchase, an order placed (an order awaiting
payment is `transactional-messaging`'s), cart emptied, entry into a higher-priority flow,
unsubscribe, hard suppression. An exit invented after the first complaint arrives later than it
was needed.

**9. Name the retirement condition.** State what would have to be true for this flow to stop
earning the attention it costs to maintain.

## Thresholds and timings

- **Entry moment: the end of the session**, not the click inside it. Take the session definition
  from your analytics rather than from intuition; it also sets the floor for the delay.
- **A delay ladder by strength of signal.** Started checkout answers faster than an abandoned
  cart, the cart faster than a viewed item, a viewed item faster than a browsed category. Express
  each rung as a fraction of the category's decision cycle rather than in hours. Where people
  decide in one evening, the whole ladder fits inside a day; where they decide over a month, the
  first rung lands the next day.
- **The "bought recently" window.** A fraction of the category's median interpurchase interval
  plus the fulfillment time. Someone whose parcel is in transit should not be told they forgot to
  buy.
- **A once-per-period guard on date triggers.** A birthday comes once a year, and the flow checks
  whether it has already sent one this period. Without the check, an attribute the customer can edit
  becomes a source of repeat gifts.
- **Data refresh faster than the delay.** Stock levels and prices have to update more often than
  the message quoting them waits. The reverse guarantees the failure in step 7.
- **A band, not a point, for a low-stock trigger.** It fires while a few units remain and stops
  before the last one goes, so the message is not written about the last unit. Set the width of the
  band from how fast that item sells.
- **A minimum size for a price change**, expressed as a share of the item price. An absolute
  amount fits one price tier at most: it is large on cheap items and trivial on expensive ones.
- **The age past which the event stops counting.** After it the flow does not start at all. A
  message about a cart assembled several decision cycles ago competes with a purchase already made
  somewhere else rather than with forgetfulness. For a catalog change, count the age from the
  person's own action behind it (the save, the view, the cart), not from the change. On the day
  such a trigger is switched on, every saved list in the history qualifies at once; apply the age
  before the first run, or the backlog goes out in one volley.

## Edge cases

- **The anonymous visitor.** The event exists, the recipient does not. The firing never becomes an
  entry, so the control metric does not see it. Count those firings beside fire volume: that share
  is how much of the occasion the flow cannot answer, and it is what address collection changes.
- **One person, two carts on two devices.** Until profiles are stitched, these are two people and
  both get the message. Stitching belongs to `list-building`, and the eligibility filter still has
  to say what the flow does with a duplicate.
- **A shared account.** One member of a household saved the item, another reads the mail. For date
  triggers it is the same problem: the stated attribute belongs to the wrong person, and it does
  so systematically rather than at random.
- **Nobody has the date.** The attribute is filled for a minority, so the birthday flow is a pilot.
  The substitute is the anniversary of the first purchase or of account creation: known for
  everyone who ever bought, and it needs no form.
- **The date was entered to get the gift.** A self-reported attribute with a reward behind it gets
  gamed. A once-per-period guard, plus refusing edits to the attribute inside the period, costs
  less than policing individual cases.
- **A trigger that fires rarely.** It can be worth running and impossible to evaluate: the sample
  never reaches the power a test needs. Ship it as a cheap flow and record that you are not
  testing it, so the gap is a decision rather than an oversight.
- **B2B and role addresses.** A birthday on a shared mailbox is noise, not a personal occasion.
  Anchor B2B date triggers to contract events instead: renewal date, end of term, warranty expiry.
- **A service rather than a product.** An appointment reminder is useful, and it needs an off
  switch. Someone who remembers the appointment needs a way to stop reminders without
  unsubscribing from everything.
- **A regulated category.** Where the law restricts what you may offer on the basis of behavior,
  meaning medicines, alcohol, financial products and products for children, a browse trigger turns
  into disclosure. Check before launch, not after the complaint.

## Failure modes

- **The message describes something that no longer exists.** The item sold out, the price went
  back up, the cart was paid for. The symptom is complaints in the form of "but your email said".
  Look for the recheck first, because a missing one is the usual cause. Where it exists and the
  message still went, the recheck ran against data that had not caught up, or the message had
  already left for the channel by the time the object changed.
- **The flow chases people who already bought.** The "bought recently" window is missing, or it
  was set as a calendar period and the category does not run on the calendar.
- **The trigger is on and barely fires.** The eligibility filters together exclude almost
  everyone. You see it in the count of entries, never in the open rate.
- **The delay is the platform default and has never been revisited.** A related tell: every flow
  in the set carries the same delay while the signals behind them differ.
- **One event, several messages.** The stack captures the event more often than it happens, and
  nobody has compared entries against distinct people.
- **The definition lives in the platform interface.** Ask someone to rebuild the same trigger from
  the written description. If the two populations differ, there is a configuration, not a
  definition.
