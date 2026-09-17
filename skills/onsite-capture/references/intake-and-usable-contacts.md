---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# Intake: what happens after submit, and what makes a contact usable

A submitted form is a promise, not a contact. This file covers the minutes and weeks after the
button is pressed: validating, recording consent, delivering what was offered, handing the person
to the program, and reading later whether the point is worth keeping.

## Entry conditions

The point and its display rule exist. There is somewhere to put the contact and something to do
with it in the next few minutes. If the program that uses the contact is not built yet, stop here
and build it first.

## Exit conditions

You have validated the contact, recorded consent in full, delivered what you promised, handed the
contact to the route its request supports, and stamped the profile with its capture source under a
retention you have stated. Every point can now be read by what became of its cohort.

## Steps

**1. Validate in place, and keep four different things apart.** A form establishes four things
about an address, in this order, and each one proves only itself:

| What you have | What it proves | Where it comes from |
|---|---|---|
| An entered address | The string is well formed and the domain is real | Format, a typo in the domain, a disposable domain |
| A deliverable address | A mailbox there accepts mail | The first message goes out and does not bounce |
| A controlled address | Whoever confirmed can read that mailbox | A click on a confirmation link sent to it |
| A permitted address | The person agreed to hear from you for a named purpose | The consent record from step 2 |

Show the error next to the field and **never clear what was typed**: losing entered text is the
cheapest way there is to lose a contact.

**A match with an existing profile is where those four come apart.** The person at the
keyboard is not necessarily the person who holds the address. Attach the submission to that profile
as a pending change and leave the profile itself alone: no rewritten personal fields, no widened
consent, no second issue of a bonus that address already received. The profile changes once the
confirmation click proves control, and not before. That click has to exist: a match sends the
confirmation message even on a point that does not otherwise ask for confirmed opt in (step 4),
because a pending change with no confirmation in its flow would wait forever. The one named
message the person asked for, a restock notice, goes out regardless; it is the change to the
profile that waits, not the request. Two habits go with it. Answer a submitted
address the same way whether or not it is already in the base: a different answer tells a stranger
who your customers are. Rate-limit repeat submissions of the same address, because a form that
mails on every submit is a way to mail somebody who never asked.

**2. Record consent, do not merely tick it.** The box is not pre ticked and is not bundled with
the action itself. Separate purposes stay separate: processing the data, marketing messages,
phone calls. What goes into the record: the wording the person saw and its version, when, on which
page, and through which capture point.

The test is simple: **a year from now, can you show what this person agreed to?** The lawful basis
layer belongs to `consent-and-preferences`; what belongs here is the obligation of the point to
preserve the evidence. Log later changes to a permission the same way: what changed, when, through
which point or page, and what it was before. A permission granted in error is reversible only if
you can find it.

**3. Deliver what was promised immediately.** When the exchange arrives by email, the delivery
tests the address rather than the person: it takes you to line two of the table above and no
further. When you hand the exchange over on screen, a code or an access link, send the email
anyway; otherwise nothing has tested the address at all and a share of the base is typos. Keep
the gap between submission and the first message in minutes, because the person is still on the
site. Issue anything worth money once, whether it is a bonus, store credit or a code that can be
spent, and name the unit: per profile where the address matched one, per address where it did not.
The second address of a known person is a match, not a new unit. On a match, hold the issue until
the confirmation click.

**4. Decide about confirmed opt in.** It applies where you are building a mailing list. It does
not apply to a service subscription to an event such as a restock, where the person is waiting for
a fact rather than a newsletter. The price is part of the volume; what you buy is a base with no
mistyped or borrowed addresses and provable consent. This is also the only step here that
establishes control of the address, which makes it the strongest defense you have against a
borrowed one. The measures in step 1 limit the damage; this one prevents it. Whether a point
requires it is decided in `consent-and-preferences` by regime and by how much control the point
has over the address; no regime opened there requires the step, and where yours asks you to
demonstrate consent, this step is the proof that the address belongs to the person who agreed.

**5. Hand over on the route the request supports.** Intake ends in one of four states. Record which
one, because it settles where the contact may go next.

| State | What the person did | Where it may go |
|---|---|---|
| Requested message | Asked for one named message: tell me when this is back in stock, tell me when the price drops. Or gave the address for one transaction, at checkout | That message, and the timeout that closes it. For a transaction, its service messages and nothing else (`transactional-messaging`) |
| Marketing | Gave permission for the program, asked for separately and recorded | The welcome program (`welcome-and-activation`), then the regular program |
| Pending | Submitted, but the confirmation or the basis is not there yet | The confirmation message and one reminder inside the confirmation window. The window closes the state: the row is deleted when it passes unconfirmed and no other purpose holds the data, an order does (`consent-and-preferences` sets the window and the reminder) |
| Suppressed | A hard exclusion applies: a bounce, a complaint, a withdrawal, a deletion request | Nothing |

**A requested message does not become a marketing state by itself.** Asking to hear about a restock
is a request for one fact, not permission for a program, and both can be collected on the same form
as two separate asks with two separate records. Where the person made only the request, you
fulfill only the request. Check the handover against four things every time: purpose, channel,
brand or controller, and the regime the person is under. A state that permits email from one brand
does not permit a phone call from its neighbor. Which basis makes a marketing state permissible is
`consent-and-preferences`; what belongs here is that a capture point must not produce an ambiguous
one. When the person withdraws, the withdrawal runs back along the same routes and stops the
marketing steps already in the queue, not only the ones nobody has scheduled yet.

**6. Stamp the source, and give it an expiry like everything else on the profile.** The contact
carries a **capture source** field naming the point it came from. Without it, quality by point
cannot be read at all, and it cannot be reconstructed afterwards. The capture source is not exempt
from retention: it is a field on a person's record, it lives inside the purpose and the period set
for that record, and "we keep it forever" is not a period. Three clocks run separately here. The
profile runs on its own. You keep the consent evidence for as long as somebody may ask you to
produce it. The minimum suppression record, the one that stops you from re-adding a deleted
person, outlives both where the regime allows it at all. You can still read cohorts after all
three expire, because step 7 reads counts by point and period and a count holds no person. Move
the history into those aggregates while you still have it. Retention periods and lawful bases are
`consent-and-preferences`; what belongs here is that the source field has one.

The promise travels with the source. Write onto the record what you told the person they were
signing up for and how often you said you would write, not only into the consent evidence from
step 2: `list-building` carries the promise as provenance, and `contact-orchestration` treats a
stated frequency as part of the basis. Neither of them can reconstruct it from anything else the
record holds.

**7. Read quality by cohort, not by widget conversion.** For each point, over a window no shorter
than the purchase cycle in your category, four shares of the contacts it produced in a period:
share confirmed, of submissions; share reaching a first purchase *after* the capture, with the
order of the same session left out; share unsubscribing in the first month; share complaining. The
same-session order is left out because a point standing at the moment of purchase would otherwise
read as the best point on the site by construction: the checkout tick box, ticked by a person who
is paying, reaches "a first purchase" every time. A point that delivers volume without activity
after it changes its exchange or closes.

Two familiar sources of junk surface here and nowhere else. **The gift hunter** comes for the
bonus and never buys, which shows up as a healthy capture rate and a dead cohort. **The checkout
tick box** gets ticked along with everything else, which shows up as volume with the worst
engagement of any point on the site.

**8. Revise on the quarterly rhythm.** Three things to look at: points that stopped capturing,
points capturing junk, and points whose exchange has stopped being true.

## Thresholds and timings

- **The first message is minutes, not hours.** The absolute comes from the promise rather than
  from a norm: the person is waiting for a named thing while still on the site.
- Compare usability rates **between your own points**, never against the market, which publishes
  form conversion per impression and answers a different question.
- The threshold for closing a point is the one at which its cohort stops differing from visitors
  who left no contact, measured over a window no shorter than your purchase cycle. Compare like
  with like: the cohort is people, the comparison group is visitor identifiers, cookies or
  devices, that were recognized across the window and never submitted, and a person on two
  devices is two of them. Read the difference between your points first, where the unit is the
  same on both sides; the comparison with the uncaptured is a floor, not a verdict, and a point at
  the bottom of the funnel clears it by construction, which is what the holdout in `SKILL.md` is
  for.

## Edge cases

- **One person, two addresses.** Personal and work. Stitching is `list-building`, but the point
  must not manufacture duplicates by rewarding a "new" address, and it says which of the two it is
  asking for: a form that wants the work address says so, because the neighbor can link the two
  records only if it knows which one it was given.
- **Somebody else's address.** People enter one by mistake and on purpose. Confirmed opt in is the
  strongest defense because it is the one that establishes control, and it is not the only one:
  issue anything of value once per profile, or per address where nothing matched, rate-limit
  repeat submissions, answer the same way
  whether or not you know the address, hold profile changes pending until confirmation, and log
  permission changes so you can find and undo a wrong grant.
- **A deletion request arrives while the person is mid-flow.** You need five answers and the
  platform supplies the first. Queued messages stop. The profile goes. The capture source goes with
  the profile. You keep the consent evidence for as long as somebody may ask you to produce it. The
  cohort counts stay, because they hold no person. Write down which system does which before the
  first request arrives.
- **A phone number.** A different legal regime from email in most places, and in many of them it
  requires separate express consent. Do not add the field on the chance you will want it later.
- **A minor.** Points whose audience may include children need an age gate before anything is
  collected, and a separate path afterwards.
- **A repeatable exchange.** A bonus that can be claimed more than once attracts the people who
  do exactly that. Limit it per profile, not per session.

## Failure modes

**The contact is captured and nothing stands behind it.** The form works, the base grows, the
first email arrives weeks later and reads as though strangers wrote it. The diagnostic sign is a
point that launched before the welcome program existed. The order runs the other way: **first what
happens to the contact, then the point that captures it.**

**Everything that touched a form ended up on the list.** Intake has one route out, so restock
subscribers, the checkout tick box and people who came for a download arrive in the welcome program
together. It reads as growth for a quarter, then as complaints, unsubscribes and a deliverability
problem, and by then you cannot untangle the base, because nobody recorded what each person asked
for apart from the rest. The diagnostic sign shows on the day you build the point, long before any
of that: a single route out of intake.

**The silent point.** A form breaks during a site release, displays continue, submissions stop.
You see it only in capture volume split by point, so monitor that split rather than review it.
Watching live mechanics is `program-audit-and-ops`.
