---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Vocabulary of in-product messaging

The three mechanics assume these terms. The first three, *session*, *message* and *display*, are
the reason arguments about "how many is too many" do not settle in a team: one side counts messages
in the queue, the other counts interruptions in a session, and they are counting different things.

## The units

**Product.** The app, and the part of a site that exists only for an identified person: the account
area, the workspace. The public pages of a site are not the product, even when a known person is on
them; those belong to `onsite-capture`. The boundary runs along the surface, not along the person.

**Session.** One use of the product by one person on one platform, as the platform's analytics
defines it, with a merge parameter: sessions closer together than the parameter count as one.

**Message.** One row of the register: class, slot, eligibility, trigger, action and destination,
completion event, expiry, owner.

**Display.** One message shown in one session. The unit of reading.

**Appearance.** A session of a person who is eligible for a message, within the message's window,
whether or not the message was shown. The unit a decision is logged against; reach counts the people
behind appearances, not the appearances.

## The slot and the format

**Slot.** A pair: a screen and a format.

**Blocking format.** A format that stops the current task until the person answers: a modal, a
full-screen takeover, a bottom sheet, a tour step with a dimmed background, the pre-permission
screen, the store rating card.

**Passive format.** A format that does not stop the task: a strip, a snackbar, an inline card, a
badge, an item in the notification center, an embedded block, a story in a stories row.

**Protected screen.** A screen where nothing blocking opens: payment and checkout steps, a form in
the middle of entry, the arrival screen after a deep link from an outside message.

**Placement budget.** How many passive elements a screen region carries at one time.

**Embedded content.** What `personalization` fills into a block of a screen: recommendations, the
balance, the status. It carries no pitch of its own and is not a row of the register. A block that
carries a pitch, a banner in a carousel or an inline card with an offer, is a message in a passive
slot.

## The class and the condition

**Message class.** The five classes of `contact-orchestration`, service, mandatory notice,
perishable and personal, automated flow, campaign, plus two that exist only in the product:
**guidance**, help with the screen the person is on, and **ask**, a request only this surface can
make. The class decides the formats allowed, whether a display counts against the session budget,
whether a display is a touch, and what completion means.

**Eligibility.** The state that has to be true at the moment of display, read live from the
server.

**Exclusion by completion.** Whoever already did what the message asks is not shown it.

**Expiry.** The moment after which the message is not shown, taken from its content.

**Completion event.** The event at the destination by which the message counts as having done its
job. Not the tap.

**Destination.** The screen inside the product the action leads to, with a fallback when it is not
available.

**Queue.** The messages waiting for the person. In the neighbor's vocabulary a queued message holds
the delivery state *in flight*.

## The budget and precedence

**Session budget.** The number of blocking displays a session admits per person, across every
source.

**Collision.** Two or more messages wanting one screen in one session.

**Precedence.** Not redefined here: `contact-orchestration`'s order, by how fast a message perishes
and how precisely it is addressed, extended here with the order of asks at one value moment.

**Deferred.** Lost a collision and waits, with its own expiry, until its own condition comes back:
the next value moment for an ask tied to one, the next session that reaches its screens for the
rest.

**Held.** An eligible appearance in which the message's own rule kept it back: its frequency, its
retirement after closes, a protected screen.

**Blocked by the budget, suppressed by completion, expired unseen.** The remaining outcomes of a
decision.

**Interrupted.** A display the system removed while the app was in the background, with no close by
the person. Recorded, and left out of the numerator of the control metric.

**Decision log.** The record of every outcome, against the person and the session.

## The reading

**Wasted interruption.** A blocking display closed without its completion event within the session,
with closed and completion as `SKILL.md` defines them.

**Wasted interruption share.** The control metric of this skill (`SKILL.md`).

**Reach of appearances.** The people shown a message at least once among the eligible people with
at least one appearance in its window.

**Budget breach.** A session with two or more blocking displays.

## Words shared with neighbors

- **Session** (`onsite-capture`). There, a visit by a browser to the site, the unit a widget is
  shown to, anonymous until it hands over a contact. Here, a use of the product by a known
  person. One word, two surfaces, and the boundary between them runs along the surface: a catalog
  page is the neighbor's session, the account area is this skill's.
- **Display rule** (`onsite-capture`, `personalization`). The neighbor's rule governs widgets on the
  site; this skill's rule governs displays inside the product. `personalization` leaves "whether the
  block shows" to the neighbor on the site and to this skill in the product; the content of the block
  stays with `personalization`.
- **Touch, message class, precedence, pitch, pitch claim, delivery state**
  (`contact-orchestration`). Not redefined. This skill names which displays are touches: a display
  of a campaign, a flow, a perishable message or an ask to a known person is one, a proactive bot
  invitation included, which is how `chat-and-bots` counts its opener; a blocking display each time
  it shows, a passive one once per person within the message's window. Guidance, service and
  embedded content are not. A queued message is *in flight*; expiring unseen is a confirmed failure
  and releases the pitch claim.
- **Value moment, pre-permission screen, re-ask** (`push-notifications`). Not redefined. This skill
  holds the slot, the frequency and the precedence of those screens; the neighbor holds the moment,
  the promise and the record of the answer.
- **Expiry** (`push-notifications`). One idea on two surfaces: there, the moment after which a push
  is not delivered; here, the moment after which a message is not shown.
- **Activation, first value** (`welcome-and-activation`). Not redefined. Guidance completes by the
  step it pointed to, not by a tour clicked through to the end; the neighbor says the same from its
  side: a finished tour is not a value.
- **Holdout** (`experiments-and-holdouts`). The neighbor's construction. This skill fixes the
  population, eligible people who reached the slot, and the split by platform.
- **Capture point** (`onsite-capture`). An ask for a profile field inside the product is not a
  capture point: the contact already exists, and an attribute is being asked for. The neighbor's
  ladder, the identifier now and the attributes later, applies here as a technique.
- **Ask** (`onsite-capture`). There, the fields a form requests. Here, a message class: a request
  only this surface can make.
- **Eligible session** (`onsite-capture`). There, a session the display rule allowed to see a point,
  a property of the rule. Eligibility here is the person's state and leaves the rule out, which is
  why an eligible appearance can end held.
- **Reachable** (`contact-orchestration`, `push-notifications`). A property of a person in a channel.
  Reach of appearances here is the share of eligible people a message was shown to, not
  reachability.
