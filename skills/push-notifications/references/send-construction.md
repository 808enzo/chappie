---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Building a push that survives the device

The unit here is **one send to one endpoint**. A neighboring skill has already decided what goes out
and to whom. This file decides how you build the push so that the device shows the right thing, at
the right time, to the right person, and so that the send does not cost the permission it relies
on.

## Entry conditions

A neighboring skill has decided the content and the audience. The registry supplies displayable
endpoints (`references/endpoint-registry.md`). The message has a class. You know until when its
content stays true.

## Exit conditions

Named for the send: class and category; interruption level; expiry; collapse key, where the push
updates something already sent; the screen a tap opens and its fallback; what is visible collapsed
and on the lock screen; the send time in the recipient's local time; the in-channel gap; the send
rate for a mass push.

## Steps

**1. Let the class of the message set its category and interruption level.** iOS has four levels.
Passive adds the notification to the list without lighting the screen or playing a sound. Active is
the ordinary level. Time sensitive presents it immediately, lights the screen, can play a sound, and
breaks through system notification controls. Critical presents it immediately, lights the screen,
and bypasses the mute switch to play a sound. Time sensitive is for what the person asked to hear
about immediately. Marketing is never time sensitive: a brand that uses the level routinely risks
people switching off all of its notifications.

**2. Set the expiry from the content, never from a default.** A push about an offer that ends on
Sunday should not appear on Monday.

- **APNs.** With a nonzero expiration, APNs stores the notification and keeps trying to deliver it
  until that date, on a best-effort basis without a guarantee. With zero, it attempts delivery once
  and does not store it. With the header omitted, APNs stores the push under its own storage policy.
- **Web push.** Every request to the push service must carry a time to live; the service rejects
  a request without one. Once the time to live elapses, the service does not deliver the message.
  A zero time to live is delivered only if the browser is available at that moment.
- **While a device is offline, APNs keeps one notification per app.** A later send competes with an
  earlier one for that single slot. A promotion sent to a phone that is switched off, after an
  order update, can take the update's place. While a service message the person is waiting for
  may still be undelivered, hold any promotion to the same endpoint or send it with an expiration
  of zero, which APNs does not store.

**3. Give updates of the same thing a collapse key.** The price dropped again, the courier is
closer: the second push replaces the first instead of stacking beside it. In APNs the field is a
collapse identifier; in web push it is the topic, and a new message with the same topic deletes any
undelivered one that shares it.

**4. Send the tap to the content, and give that screen a fallback.** Without a deep link, a tap
opens the app's home screen and the person has to find the thing themselves. When the item has sold
out or the offer has closed, fall back to the page of the product group it belongs to rather than
to the home screen. Any
substitution in a push is resolved at send time and gets no second chance, so every substituted
value needs a fallback (the rule and its ladder are `personalization`'s).

**5. Decide what is visible without a tap, and to whom.**

- **Put the whole claim in the title and the first line.** How much more shows before the person
  expands the notification depends on the device, the operating system and the person's settings,
  and so does whether an image shows before expansion. An image therefore cannot be what carries
  the meaning.
- **Anyone near the device can read the lock screen.** For apps distributed through the App Store,
  guideline 4.5.4 says push notifications should not be used to send sensitive personal or
  confidential information, and the reason applies to any push. The push says there is news about
  the order; the details sit behind the tap.
  **Who this does not bind:** web push and apps distributed outside the App Store, since the
  guideline is a platform rule enforced through review; keeping the details behind the tap is this
  skill's rule for every push.
- **A notification is not a place to keep anything.** Once it is tapped or cleared, the person may
  not find it again. Anything they need to keep, a booking reference or a code, does not travel by
  push alone.

**6. Send in the recipient's local time, and choose the slot by two numbers.** Quiet hours belong to
`contact-orchestration` and are not defined here. For a campaign, choose the send time by orders and
switch-offs read together, per slot, rather than by taps. The slot with the most purchases can also
be the slot with the most switch-offs, and the choice is about the sum. Count a slot's orders by the
people it reached, on any device, over the same window for every slot: orders inside the session a
tap opened miss everybody who reads on the phone and buys on a laptop. Where a device collects
notifications into a scheduled summary, an offer that lasts an hour can surface after it ended: the
expiry governs how long the push service stores the push, not what the device shows later.

**7. Hold an in-channel gap.** The minimum interval between two pushes to one person, for everything
that is not a service message the person is waiting for, is a property of the channel. Hold it per
person, across all of their endpoints: the fan-out rule moves messages between a person's devices,
and a gap kept per endpoint lets two pushes land minutes apart on the phone and the tablet. The gap
lives here, the way `email-program` keeps its own in-channel gap. The cap across all channels
per person belongs to `contact-orchestration`. Set the gap from your own data: read switch-offs by
cohort against the gap people actually experienced. **Check it at the moment of sending, against
sends already reserved and not only against sends already delivered.** Two triggers firing in the
same second both pass a check against a history that is still empty. `contact-orchestration`
reserves room under its cap for the same reason.

**8. Pace a mass send.** A mass push brings everybody into the app at once. Set the send rate from
what the app's backend and your support team can absorb.

## Thresholds and timings

| Quantity | Value |
|---|---|
| Interruption level for marketing | not time sensitive |
| Expiry | the moment the content stops being true |
| APNs storage while the device is offline | one notification per app |
| Web push time to live | required on every request |
| In-channel gap, per person across endpoints | from your own data |
| Mass send rate | what the app and the support team absorb |

The APNs and web push rows are platform limits. The other four are yours.

## Edge cases

- **A cascade waits on a push nobody can see.** In a cascade step (`triggered-messages`), a push to
  a person with no displayable endpoint does not go out, so there is nothing to wait for: skip the
  step at once. Delivered means something different on each platform, because it is a statement by
  the push service or by the app, so wait on a tap or on the conversion, as that skill already
  advises for its responses.
- **A data message instead of a notification.** A silent technical message consumes no attention
  and is not counted as a touch. If the app draws a notification from it, it is counted as one.
- **A long chain over many segments.** Checking segment membership and exclusions at every step can
  cut the audience to almost nothing before the chain finishes. Build a campaign as one selection at
  send time, not as a chain of checks.
- **Content that has to outlive the tap.** See step 5: it goes by a second channel or lives in the
  app, and the push only leads there.

## Failure modes

**A dead offer on the screen.** The expiry was left empty or at a default. The sign: complaints,
and taps after the offer closed.

**A stack of identical pushes about one thing.** No collapse key. The sign: three notifications
about one item's price side by side, and switch-offs among people who asked to hear about price
drops.

**Time sensitive as a habit.** Marketing goes out at the time sensitive level. The sign:
switch-offs across everything the brand sends, concentrated among the people who received time
sensitive marketing.

**A tap to nowhere.** An app update broke the deep link, or it lands on an empty page. The sign: the
screen that opens after a tap is not the one the push linked to, but the home screen, an error or an
empty page. Short sessions after taps with no orders are not the sign on their own: a person who
reads on the phone and buys on a laptop leaves the same trace.

**Sources for the platform limits in this file, each opened 2026-09-11.**

- Apple Developer Documentation, UNNotificationInterruptionLevel (passive, active, time sensitive,
  critical): https://developer.apple.com/documentation/usernotifications/unnotificationinterruptionlevel
- Apple Developer Documentation, Sending notification requests to APNs (apns-expiration,
  apns-collapse-id, storage of one notification per bundle ID):
  https://developer.apple.com/documentation/usernotifications/sending-notification-requests-to-apns
- IETF, RFC 8030, Generic Event Delivery Using HTTP Push (TTL, topic and replacement):
  https://www.rfc-editor.org/rfc/rfc8030
- Apple, App Review Guidelines, 4.5.4 (sensitive personal or confidential information):
  https://developer.apple.com/app-store/review/guidelines/
