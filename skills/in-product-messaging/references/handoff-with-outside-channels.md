---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# The handoff with outside channels: the product as a step in the cascade, and the inbox

The unit here is **the pitch**: one thing a person is told or asked, carried by several messages in
several channels. It is the unit of pitch deduplication in `contact-orchestration`, and it is taken
from there as is. This file settles where a display inside the product stands relative to the email
and the push about the same thing, what a display hands to the contact log and to the other
mechanics, and how a display is read.

## Entry conditions

At least one outside channel runs (email, push, SMS), the product has a display layer, and the
person's record joins the two: a display event and a send event are written against the same key.
Without that join the mechanic is not available. Pitch deduplication does not hold across two
systems that cannot see each other, which is the neighbor's own caveat about the pitch claim.

## Exit conditions

Every pitch has a written position for its in-product display: the last step for people who did not
react, simultaneous with every channel, or in-product only. It is written which displays are
touches. The mirroring rules for the notification center are written. Display outcomes leave as
events on the person. The reading rule is chosen before launch.

## Steps

**1. Choose the position of the display per pitch, by how fast it perishes and by who is
reachable.** Three positions. *The last step for people who did not react:* email, then push, then
the display at the next open, only for people who received the earlier steps and did not act, once
per person; a monthly selection that has time to wait goes here. *Simultaneous:* a one-day offer goes
to every channel at once, because the next session may come after it ended. *In-product only:* for
people unreachable outside (no notification permission, no email; the product is the one channel
that reaches them), and for pitches that make sense only on the screen, such as the free shipping
threshold in the cart. The first position requires the cascade's steps to belong to
`triggered-messages`, and the display to read "did not act" from the log after a wait equal to the
read window of the previous channel.

**2. A display of a campaign, a flow, a perishable message or an ask to a known person is written as
a touch; guidance on a screen, service, and embedded content are not.** The rule at the seam between
`onsite-capture` and `contact-orchestration` says that a touch which would have gone out as a
message, had you held an address, counts toward the load. In the product everyone has an address, so
these displays are touches in the neighbor's log: delivery is the display, and the touch counts
toward the total cap and toward the cap of the channel "in-product". A blocking display is a touch
each time it shows, because each one interrupts again. A passive display is a touch at its first
display to the person within the message's window, and its later appearances in the slot are the
same touch; otherwise a banner standing on the home screen spends a daily user's whole cap and
pushes the email and the push out. A proactive bot invitation is an ask in any format, and
`chat-and-bots` counts the opener to a known person as a touch from its side. Guidance tied to a
screen, a service message, and embedded content are not touches: the first is a property of the
screen, and a blocking tour step stays guidance here even where it takes an ask's rank in the budget;
the second is the neighbor's exemption; the third is what `personalization` fills into a block, and
it carries no pitch. This is what makes "cutting in line" honest: a display may stand outside the
calendars of email and push, and it stays inside the person's total. A queued message holds the
delivery state *in flight* in the neighbor's vocabulary: it has no history yet, and only the pitch
claim keeps a second channel from repeating it. Expired unseen is a confirmed failure and releases
the claim; otherwise the next channel of the pitch finds it in flight and does not send.

**3. A pitch the banners and the newsletters already carry is not repeated, except for the awaited
event.** A points balance reminder to a regular customer who sees the balance in the site header, in
the newsletters and on social media is a repeat, and in a controlled comparison such a display
lowered the segment's conversion. A big sale the person read about in an email and is waiting for is
not a repeat; it is a reminder to make it in time. The test before a display: is the pitch new to
this person, absent from their log within the window and from the embedded content they see in the
product, or is it the event they are waiting for? Otherwise suppress. The log alone cannot answer
it: embedded content is not a touch, so the log holds no record of it, and the reminder above
repeated a balance the person already saw in the header. Separately: what sits in the banner
carousel on the home screen is not doubled by a modal on the same home screen.

**4. Outcomes leave as events on the person.** Shown, tapped, completed, closed, expired go to the
`contact-orchestration` log, for deduplication and the cap. To `triggered-messages`: a completion
inside the product ends the flow, so the reminder email does not go out after the app was updated
or the birthday was filled in. To `push-notifications`: a permission obtained through a screen inside
the product is written into the ask record with the screen named. To `offer-design`, which issues
and honors the prize: a prize won in a game goes out by email and push with its terms. To
`voice-of-customer`: the submitted survey. A tap can itself be the recorded event of a stage: signed
in to the app and tapped, as the condition for the next stage of a contest.

**5. The notification center mirrors what the person may have missed, with an expiry and a read
state.** The center is a passive, persistent slot. Outside messages of the classes service, mandatory
notice, and perishable and personal are mirrored into it, with the same expiry as the source; the
read state sits on the person, across devices; the badge counts items that are unread and not
expired. A campaign is mirrored only for a person who had no other channel; otherwise it is a
repeated pitch. An item mirroring a touch already logged is a second surface of the same touch, not a
new one; an item that is the pitch's only surface is a touch.

**6. Choose the reading rule before launch; a view with an attribution window is not a test on
its own.** The doubt practitioners voice is right: a display is seen by people who were about to act
anyway; a tap followed by an order placed from the catalog gets credited to the display; a view
window of weeks credits it with everything. Three things are read apart. *The completion event*
(`slots-and-message-contract.md`, step 7) is about the message's own job. *The holdout* is about the
effect on the business; `experiments-and-holdouts` builds it, and the conditions that belong here
are these: the population is the people who were eligible **and reached the slot** within the
window, not every user of the app; assignment happens at the first moment of eligibility; a split
by platform is mandatory, because a divergence between platforms catches a broken destination on
one of them. *A code that exists only in this display* (its construction is `offer-design`'s) reads
redemption without a holdout, and it does not read the increment.

**7. The attribution collision with the system prompt: no in-product screen where the system
prompt can fire in the same session.** If a person can grant permission in the system prompt and
tap your screen as well, the record will not say who persuaded them. The re-ask screen shows only to
endpoints in the state refused or switched off in the registry of `push-notifications`, and never to
endpoints in the state never asked in the session of the first ask.

**8. Season and incident switch the promotional layer off by class, not message by message.** One
switch on the class in the register, with an end date; the budget of
`session-budget-and-precedence.md` reads it; after the switch is lifted, a number gets read.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Wait before the display as the last step of a cascade | the read window of the previous channel: a late point on your distribution of time to a click or a conversion for email, to a tap for push; an open is not a response (`triggered-messages`, step 6) | parameter |
| Expiry of an item in the notification center | the expiry of the source message | follows from the definition |
| View-through attribution window | not a test; read only next to a holdout | none |
| Holdout population | eligible people who reached the slot within the window | parameter |

## Edge cases

- **The person acted on the email after the display already happened.** Completion is credited to
  the first completion event; the second display does not happen, because completion suppresses
  it, provided the person's record is joined. Not joined means two displays and two credits, and
  that is an entry defect, not a reading defect.
- **An unreachable person became reachable mid-cascade,** by enabling push through a screen in the
  product. The current pitch reaches them in the product; the next pitches use the new channel.
- **A session before sign-in.** It has no outside channels; the position is in-product only, and
  the log joins at sign-in.
- **The notification center arrived after the events.** Service items within the retention window
  are mirrored back; campaigns are not: the person is not shown offers that ended before the center
  existed.
- **A pitch whose only outside channel is SMS.** The price of SMS sets the position: the in-product
  display goes first for people who open the product more often than the pitch's window lasts, and
  SMS goes to those who did not appear by a cut-off inside the window that leaves the SMS time to
  work. The queued display expires at the cut-off rather than at the end of the pitch, and expiring
  unseen releases the claim (step 2); `messaging-channels` holds the price, `triggered-messages` the
  order.

## Failure modes

**One pitch arrives three times.** The symptom: the share completing falls while reach holds, and
over the same period reachability loss in the outside channels grows (`contact-orchestration`'s
metric). The cause: displays are not written as touches, so pitch deduplication does not see them,
or the cascade step does not read "did not act". A second cause with the opposite sign: completion
fell at the same reach because the destination broke, and a split by platform, reach and taps per
platform, tells the two apart. A third cause shows no rise in reachability loss and taps falling together
with completion: the message itself, expired with no expiry set or eligibility not re-read at display
(`slots-and-message-contract.md`, failure modes).

**The notification center turns into a graveyard.** The badge counts expired items; people stop
opening the center. The symptom: the share of sessions that open the center falls while the share of
sessions with a non-zero badge grows. The cause: the source's expiry is not carried onto the item, or
campaigns are mirrored to everyone.
