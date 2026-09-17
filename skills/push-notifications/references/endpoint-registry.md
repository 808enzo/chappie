---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# The endpoint registry: which endpoints are alive, whose they are, and when they died

The unit here is **an endpoint in the registry**. The registry exists because push hides its most
important event. An unsubscribe from email arrives as an event. A person switching notifications
off is a state change on their device, and the app learns about it the next time it runs and reads
its settings, or never.

This file also owns the promise the library made for this channel: what to do when notifications
get switched off.

## Entry conditions

The app or site registers endpoints with a push service and hands over their tokens, which is the
job of the platform SDK where you have one. You have an event for an app open or a site visit. You have a way to link an
endpoint to a person, through sign-in or through record matching (`list-building`).

## Exit conditions

A registry with one row per endpoint, a state for each, the date its permission was last read, and
its person link; a rule for how states get updated; a rule for which endpoints receive a message
of each class; a sequence for what happens when a switch-off is discovered. From the registry you
can say how many endpoints can show a notification, how many are quiet, how many are switched off
and how many are dead, and how many people all of that covers.

## Steps

**1. One row per endpoint, not per person.** Fields: the date the row was created, which is the first
app open, or on the web the moment of consent, and which places the endpoint in its install cohort;
platform (iOS, Android, which browser), token (empty until the push service issues one),
the push service that delivers to it, permission state and the date it was last read, category
states, when the endpoint was last seen, the person link or its absence, the ask history
(`references/permission-ask.md`), and marketing opt-in.

**2. Keep the states to a closed set.**

| State | What it means | What to do with it |
|---|---|---|
| never asked | the endpoint exists, no prompt has been shown | entry point for the ask |
| refused | the prompt was shown and the answer was no | re-ask on a new value moment |
| displayable | display permission granted, token accepted, endpoint seen recently | send under the fan-out rule |
| quiet | provisional authorization on iOS, or quiet delivery chosen | count apart: pushes reach the history only |
| category off | permission granted, one notification channel or one category switched off | send only to categories still open |
| switched off | permission was granted and then withdrawn | loss interval, step 8 |
| stale | the permission was last read longer ago than your threshold, so its state is unknown | out of reach counts; the mechanic's owner decides the rest |
| retired | the push service rejected the token | delete the token, close the row |

**3. Read the permission on every app open, and write it down with the date.** The permission lives
on the device and the app can only read it while it runs. Apple tells developers to check the
status because people change it at any time; on Android the app can also read each notification
channel's settings back. Treat the push service's response to a send as a statement about the
token. Whether the person allowed the notification to be shown is a fact the app reads on the
device, so an accepted send does not count as a shown notification.

**4. Handle push service responses as facts about the token.**

- **APNs.** Status 410 with the reason Unregistered means the device token is inactive for the app,
  and there is no need to send further pushes to it unless the app retrieves the same token again.
  ExpiredToken means the token has expired. A 410 response carries the time at which APNs confirmed
  the token was no longer valid.
- **FCM.** UNREGISTERED (HTTP 404), or INVALID_ARGUMENT (HTTP 400) when you are certain the payload
  is valid, means the registration is safe to delete: it will never be valid again.
- **Web push.** A push service that rejects a subscription makes the endpoint retired. The exact
  status to act on comes from your push service's documentation.

**5. Age out endpoints and refresh tokens.** FCM calls a registration stale when its device has not
connected for over a month, and on Android it treats a registration inactive for 270 days as
expired and rejects sends to it. On iOS, FCM relies on APNs, which has no such inactivity-based
expiry. FCM recommends refreshing tokens on your server once a month and says there is no benefit
in doing it more often than weekly. Those are FCM's figures for FCM; a different push service is
read from its own documentation. An endpoint nobody has seen for a long time inflates the subscriber
count. It deflates every rate whose events only live endpoints produce, such as taps and
conversions, and inflates the ones dead endpoints feed, such as failed sends, so count reach by the
date an endpoint was last seen.

**6. Keep one dated person link per endpoint.** An endpoint links to a person on sign-in, or through
record matching in `list-building`. Signing out closes the link. A different person signing in on
the same endpoint moves the link; it never adds a second person. An endpoint with no person stays
anonymous and is counted on its own line, which is how `contact-orchestration` already counts it.

**7. Apply the fan-out rule: the message goes to a person, delivery goes to endpoints.** A message
is addressed to a person. Which of their endpoints receive it is decided here, by class.

- **A service message about an event the person is waiting for**, such as an order status or a
  courier arriving, goes to every displayable endpoint the person has. Missing it costs more than
  seeing it twice.
- **Everything else** goes to one endpoint: the one the person used last among those that may
  receive this message, meaning displayable, with the message's category open and, for marketing,
  a marketing opt-in on record where one is required. On a tie, pick the one where the action that
  triggered the message happened. Pass over an endpoint used more recently whose category is
  closed; do not send to it.
- **One message is one touch** against `contact-orchestration`'s cap, however many endpoints it
  reached. That skill defines a touch as one delivered message to one person in one channel, so the
  number of endpoints is a delivery detail. Write the message to the log once, against the person.

**8. React to a switch-off.** An endpoint that was displayable turns up switched off. Six things
follow, in this order.

1. **Date it as an interval.** The loss happened somewhere between the last time the endpoint was
   seen with permission and the first time it was seen without. The loss has no exact date; do not
   invent one.
2. **Report it to `contact-orchestration` as a reachability loss in the push channel if it was the
   person's last displayable endpoint.** That skill counts a loss once per person per channel per
   period, and a person who still has another displayable endpoint has not lost push. Put the loss
   in the period in which you discovered it, at the end of the interval: that is the first moment
   anybody knows about it.
3. **Move service messages to another channel** if the person has no displayable endpoint left. An
   order status still has to arrive; what must arrive, and how fast, is `transactional-messaging`.
4. **Do not move marketing to another channel in its place.** The person has just told you there
   were too many messages. The other channel runs on its own basis and its own frequency.
5. **Find the last straw.** List the sends that reached the endpoint inside the loss interval, and
   their classes. When switch-offs cluster after one class or one flow, the finding goes to whoever
   owns it: `triggered-messages` for a flow, `promo-calendar` for a window, the campaign owner for
   a campaign. Four failure modes in this skill share one sign, switch-offs clustering in some
   group, and this list is what tells them apart: after marketing reached people who were promised
   service messages only (the ask), among people with several endpoints (the fan-out rule), among
   people following updates of one item (no collapse key), among people who received time
   sensitive marketing (the interruption level). Read which class and which setting preceded the
   loss, then go to the matching failure mode.
6. **The way back** is the re-ask path in `references/permission-ask.md`, and only on a new value
   moment.

**9. Design categories before launch, because they are a one-way door.** From Android 8.0, every
notification must belong to a channel. Once a channel is created, the app cannot change its
behavior; only the person can, in the system settings, and the app can still change its name and
description. Create separate channels for service and for marketing. Without them, somebody tired
of promotions switches everything off, order updates included, and those updates then have to be
duplicated in another channel. A category setting inside the app, one checkbox for service and one
for marketing, gives the same choice on iOS and on the web. The preference center as such belongs
to `consent-and-preferences`.

## Thresholds and timings

| Quantity | Value |
|---|---|
| Permission read | on every app open |
| FCM stale registration | no connection for over a month |
| Android registration expiry in FCM | 270 days of inactivity; iOS has no such expiry |
| Server-side token refresh (FCM recommendation) | monthly; no benefit more often than weekly |
| Staleness threshold: not seen for too long | set by you, from the usual gap between app opens; reach counts and the control metric use the same one |

The three FCM rows are platform figures, scoped to FCM. The first and last rows are yours.

## Edge cases

- **A reinstall.** A new endpoint appears, and the old one stays in the registry until the push
  service rejects its token. The person now has two endpoints on one device, one of them dead. The
  fan-out rule survives this because it picks the last used; an endpoint count does not.
- **A move to a new SDK or messaging platform.** Device identifiers in the old and new systems do
  not match, and the fresh registry fills only as people update the app. Until then the registry is
  mixed. Old installs registering with the new system are not new endpoints: carry over their
  original creation date, or keep them out of the cohorts, because otherwise they land in the cohort of the month
  they updated. Read the control metric by install cohorts after the move rather than comparing
  before and after.
- **An app built on a web view.** A site session inside the app and a session in the browser are
  different endpoints. If the platform cannot tell them apart, one person receives web push and
  mobile push as if they were two people.
- **Devices without the platform's default push service.** They use a third push service with its
  own tokens and errors. Keep it as a separate platform in the registry.
- **Sign-out on a shared device.** If the link is not closed, the next person receives somebody
  else's personal notifications. That is an incident involving personal data, and its route is
  `program-audit-and-ops`.
- **Separate campaigns for iOS and Android.** One campaign becomes two sends with two audiences, and
  nobody can say who got what. Keep one campaign and treat the platform as a field on the endpoint.

## Failure modes

**The registry counts tokens instead of people.** The subscriber figure exceeds the number of
people because it includes dead endpoints, stale ones, and several endpoints of one person. The
sign: the push base grows and the number of people it reaches does not.

**Click rate holds while the channel shrinks.** Once you learn of a switch-off, the
endpoint leaves the sends and the delivered count, and the most patient remain in the denominator.
Until then the push service keeps accepting sends to it, and the rate dips. The sign: switch-offs rise while click rate
on delivered pushes stays level or improves. It can also fall, when the content itself is what
drives people away; either way, a rate computed on delivered pushes says nothing about how many
people are left. The control metric in `SKILL.md` counts the whole cohort for that reason.

**The same promotion on every device.** Phone, tablet and laptop all light up at once. The sign:
switch-offs cluster among people with several endpoints. The fan-out rule is broken or was never
set.

**Sources for the platform limits in this file, each opened 2026-09-11.**

- Apple Developer Documentation, Handling notification responses from APNs (status 410,
  Unregistered, ExpiredToken, timestamp):
  https://developer.apple.com/documentation/usernotifications/handling-notification-responses-from-apns
- Apple Developer Documentation, Asking permission to use notifications (checking the current
  settings): https://developer.apple.com/documentation/usernotifications/asking-permission-to-use-notifications
- Firebase, Best practices for FCM registration management (stale and expired registrations, error
  codes, refresh frequency): https://firebase.google.com/docs/cloud-messaging/manage-tokens
- Android Developers, Create and manage notification channels (Android 8.0, what the app can and
  cannot change): https://developer.android.com/develop/ui/views/notifications/channels
