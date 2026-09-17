---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# The session budget and precedence: who owns the screen this session

The unit here is **the session of one person on one platform**. This file settles who gets the
screen in this session when the queue holds more than the session admits: how many interruptions a
session allows, how a message's frequency follows from its lifetime, which message wins a collision,
what a close changes, and where the rule executes.

## Entry conditions

The register of `slots-and-message-contract.md` exists. Sessions and screens are distinguishable in
the data. The display decision is made in one place, or it is known in how many places it is made
today, in which case step 7 comes first.

## Exit conditions

A written budget of blocking displays per session. A frequency for every message, derived from its
lifetime and from how often people open the product. A precedence order for collisions, the
collision at a value moment included. Rules for closes and returns. A decision log: shown, deferred,
blocked, held, suppressed, expired.

## Steps

**1. Read how often people open the product before setting anything.** The distribution of
sessions per person per week and per month, by install cohort. A daily product and a monthly
product need different budgets: "once every two days" for somebody who opens the product once a
week means "every session". Everything below is set relative to this distribution.

**2. Budget the blocking displays: one per session per person, across every source.** One is the
starting point. It holds for products opened more often than a few times a month; a product opened
once a quarter can carry more in a session before the person reads it as pressure. Revise it from
two readings in `SKILL.md`: when deferred messages expire unseen while wasted interruptions stay
rare, the budget is too tight; when wasted interruptions are common with an empty deferral queue,
the budget is not the problem. Passive formats do not count against the session budget; they have a
placement budget instead: one strip, one snackbar, one inline card per screen region at a time.
Service and mandatory notices sit outside the budget and still go one at a time: an outage notice
does not stack with a recall.

**3. Derive each message's frequency from its lifetime and the open cadence, not from a menu.** The
three settings a tool offers, every session, once, and once every N days, correspond to three
positions of the message's window relative to the gap between sessions. *Every session* is for
service (an outage, until it is fixed) and for testing on yourself. *Once* is for a message whose
window is shorter than the typical gap between sessions, such as a sale that lasts a few hours,
where the next session arrives after it ended anyway, and for an announcement that has no second
reading. *Once every N days* is for a message whose window is longer than the gap: N equals the
window divided by the number of exposures you are willing to give one person within it. For a person
whose gap between sessions is as long as N or longer, the setting is "every session" under another
name: they see the message in each session inside the window. Check N per cadence group from step
1, not against the whole base: where the distribution has two humps, the median gap of the base
belongs to neither group and jumps from one hump to the other with a small change in the mix. A group
for which N comes out at or below its own typical gap gets its own register row with fewer
exposures, so that its N clears the gap; for a group whose gap is longer than the window, the
message is *once*. A standing ask returns under the neighbor's rule, a new value moment and a
ceiling per person (`push-notifications`), with a floor taken from your distribution of opens; for a
data-for-discount ask in California the floor after a refusal is set by statute
(`slots-and-message-contract.md`, thresholds).

**4. After a close, lower the volume; never raise the frequency.** A closed blocking display does
not return in the same session. It returns in a passive form, a strip or an item in the notification
center, or it does not return. Several consecutive closes retire the message for that person; the
number comes from your own data, completions among people who closed this message before, the same
reading `onsite-capture` uses, and the neighbor already notes that the readable signal runs out
within the first few repeats. A "not now" on an ask returns on a new eligibility event (a new value
moment, a new version, a new order), not on a timer. Where no such event exists and a timer is all
you have, set it from the distribution of opens and record it as a starting heuristic.

**5. Suppress by completion and by the outcome in other channels, through the person's record.**
Already did it: out of the display. Already saw the same pitch in an email or a push and acted:
out. Saw it and did not act: that is a cascade (`handoff-with-outside-channels.md`), allowed once. A
pitch that already sits in the banner carousel on the home screen is not shown a second time as a
modal on the same home screen.

**6. Resolve collisions: perishable and personal wins, service first, and the ask that is spent
here outranks the ask that can travel.** The order for blocking displays: service, then mandatory
notice, then perishable and personal (the price of the item in the cart dropped, a slot for today),
then the asks of this moment in the order below, then automated flow, then campaign. Guidance does
not collide with a blocking display: it sits on an element, not over the screen. A blocking tour step
takes the rank and the budget of an ask of this moment, and it stays guidance in the contact log.
Among asks at the same value moment, the order is this. **The pre-permission screen goes first:** the
system prompt fires only inside the app, and a "not now" on your screen spends nothing.
**The store rating request goes second:** you choose when to call it and the platform decides whether
the card appears at all, so a deferral costs little, and the next completed sequence is another
moment. **The survey goes third:** it can travel by email or push, which is `voice-of-customer`'s
call. **The promotion goes last.**

The losers are deferred with their own expiry, each until its own condition comes back: the
pre-permission screen and the rating request until the next value moment, never the next launch,
which Apple's guidance on review requests also advises against; a survey until the next session that
reaches its screens. An ask that can travel does not sit in the queue past the point where the next
qualifying session may come after its window: at deferral, compare what is left of the window with
the person's gap between sessions, and hand the ask to the outside channel now. A survey the business
owes, by contract or to a regulator, must not end as expired unseen; for a person with no outside
channel it outranks the pre-permission screen and the rating request, because both get another value
moment and the survey does not. For an ask that follows an order, re-read at display time whether a
return was filed on that order since. Read the deferred share per slot on its own: a slot where
asks defer more often than they show is overloaded, and one ask moves to another value moment.

**7. Execute the rule in one place, and make the native surfaces obey it.** The SDK's in-app
messages, a banner the developers built, an item in the notification center, the call that presents
the rating card, the pre-permission screen: each asks the same layer "may I show now". A display with
no decision record is a rule violation by definition. A surface that cannot ask (an old app version)
is listed as an exception with a fixed frequency and an end date.

**8. Log decisions, not only displays.** Shown, deferred (and by which message), blocked by the
budget, held by the message's own rule (its frequency, its retirement after closes, a protected
screen), suppressed by completion, expired unseen, against the person and the session. This log is
what `handoff-with-outside-channels.md` hands to the contact policy. The control metric in `SKILL.md`
counts displays from the surfaces' own events and reads this log beside them: a display event with no
decision record is the direct reading of step 7, and a metric built from the log alone contains no
such display by construction.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Blocking displays per session | start with one; it holds for products opened more often than a few times a month; revise from the wasted interruption share and the deferred share | starting heuristic |
| N in "once every N days" | the message's window divided by the exposures per person you allow within it; checked per cadence group: at or below the group's typical gap it is "every session" for that group, which gets its own row with fewer exposures | parameter |
| Consecutive closes before a message retires for a person | completions among people who closed it before, from your own data | parameter |
| Sessions counted as one | gaps shorter than a parameter from your distribution of gaps merge into one session | parameter |
| Budget read per day instead of per session | for the cadence group from step 1 that opens the product many times a day, whether or not the merge parameter joins its sessions; the group's boundary from your distribution of sessions per day | parameter |
| Return of "not now" on an ask | on a new eligibility event; a timer only where no event exists, set from the distribution of opens, recorded as a starting heuristic | starting heuristic |
| Store rating quotas; the floor for asking again in California | `slots-and-message-contract.md`, thresholds | platform rule, statute |

## Edge cases

- **The first session of an install.** Its budget belongs to first-run guidance. Asks wait for a
  value moment rather than a session count; the disagreement between practitioners about the first
  session is already settled by `push-notifications`: a session count stands in for a value moment
  until the moment is found.
- **An incident.** The product's state switches the budget: only service shows, everything else
  defers until the state clears, and whatever expires in the meantime expires.
- **Peak season and a launch.** The promotional layer is switched off, or the budget changed, by
  class rather than message by message, for a fixed term with a named price and a number you read
  afterward, the same exception route `contact-orchestration` uses.
- **Many sessions a day.** A courier, a dispatcher, somebody who opens the product dozens of times:
  read the budget per day for that group, found in step 1. The merge parameter does not do it for
  you: it joins only the sessions closer together than the parameter, and somebody whose gaps sit just
  above it keeps every session and a budget for each.
- **Several accounts held by one person.** Eligibility keyed to the account gives a second display
  and a second prize. The key for participation is the person under `list-building`'s merge rule,
  not the account and not the device.
- **A person with no external channel at all.** The budget is the same: being unreachable elsewhere
  is no reason to double the interruptions here. What changes for them is the position of the
  display in the cascade (`handoff-with-outside-channels.md`), not the budget.

## Failure modes

**Every launch opens with a modal.** The wasted interruption share is high and flat, and the reach
of every message sits close to all of its eligible people. Either the budget is not executing
(three systems), or a promotion was given the service setting "every session". Two readings from the
surfaces' display events tell them apart: displays with no decision record, and the share of sessions
with two or more blocking displays. Either above zero, the budget is not executing; both at zero, it
is the class. Read from the decision log alone, both stay at zero under three systems, because the
surfaces that bypass the layer write nothing to it.

**The quiet one: reach collapses behind the budget.** One standing ask takes the one slot every
session; perishable messages defer until they expire unseen. Read it in the deferred share and the
expired-unseen share. The remedy is the order in step 6 (perishable outranks a standing ask), or
moving the standing ask into a passive form, an item in the notification center, a strip in
settings. A second cause with the opposite picture in the log: reach fell and the log holds no
deferrals. Then eligibility stopped being recomputed (stale state) or events are not arriving, and
that is `slots-and-message-contract.md`, not the budget.
