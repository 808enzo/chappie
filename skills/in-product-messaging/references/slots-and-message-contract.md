---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Slots and the message contract: what may appear in the product, where, and in what form

The unit here is **the message and the slot it occupies**. A slot is a pair: a screen and a format. This
file settles what has the right to appear inside the product at all: which screens admit which
formats, what class each message belongs to, how its eligibility is written, where its action leads,
when it expires, and what counts as done. How many times it may appear and which message wins a
collision is `session-budget-and-precedence.md`; how a display relates to the email and the push
about the same thing is `handoff-with-outside-channels.md`.

## Entry conditions

An app, or a signed-in area of a site, exists. Events from the product (a screen opened, an action
taken) reach the layer that decides displays, through a vendor SDK or your own code. At least one
screen is instrumented. With no events from the product the mechanic does not work even
qualitatively; that is an input for `martech-stack` and the same edge case `welcome-and-activation`
names for activation.

## Exit conditions

A register with one row per message: class, slot, eligibility written as state, trigger, action and
destination, completion event, expiry, owner, and how it counts against the session budget and the
contact log. A list of protected screens. Every message passes the contract in step 5.

## Steps

**1. Inventory the surfaces before the messages.** List the screens of the product and, for each,
the formats it admits. Formats split by one property: whether the format stops the current task
until the person answers. **Blocking** formats: a modal, a full-screen takeover, a bottom sheet, a
tour step with a dimmed background, the pre-permission screen, the store rating card. **Passive**
formats: a strip at the top of a screen, a snackbar, an inline card in a list or feed, an unread
badge, an item in the notification center, an embedded block, a story in a stories row. Mark the **protected
screens**, where nothing blocking opens: payment and checkout steps after the person tapped pay, any
form in the middle of entry, and the first screen after arrival through a deep link from an external
message. The person came for what the email or the push promised, and a display on top of it takes
away the thing they were called in for.

**2. Give every message a class: the neighbor's five, plus two of the product's own.** Service,
mandatory notice, perishable and personal, automated flow, campaign are `contact-orchestration`'s
classes and keep their meaning here. Two classes exist only in the product, because they have no
life outside the surface: a tooltip has nowhere to be sent. **Guidance** is help with the screen the
person is standing on: a tour step, a tooltip on an element, an empty state, a what's new note on the
screen where a feature the person has not used lives. A what's new note at entry that announces a
release is not guidance: it is about no screen the person is on, it would have gone out as an email,
and its class is campaign. **Ask** is a request that only this surface can make: notification
permission (the neighbor's screen), a profile field, a store rating, a survey, a proactive bot
invitation. The class decides four things: which formats the message may take, whether a display
counts against the session budget, whether a display is a touch in the contact log
(`handoff-with-outside-channels.md`), and what counts as completion (step 7).

**3. Write eligibility as state, not as a segment list.** What has to be true at display time: the
old app version is installed; the birthday field is empty; notifications are not enabled; the cart
holds an item above the free shipping threshold; the person is a member of the loyalty program.
And the **exclusion by completion**: whoever already did what the message asks is not shown it again. The
person who updated the app leaves the old version segment and the display with the same event. A
segment list built yesterday is stale by exactly the people who did the thing since; state is read
live.

**4. Bind the message to the screen where the person can answer it in one tap, and to the moment
on that screen.** A category promotion on that category's screen, not on the home screen. The free
shipping threshold at the moment an item lands in the cart. Expiring points at entry, after an
order, or at the entrance to the catalog, wherever the person can spend them. An outage notice on
any screen at entry, with another way to get the service. An announcement at entry. A delay on the
entry screen is a parameter: after the person's first action on the screen rather than on arrival,
and its size comes from your own distribution of time to first action on that screen. The home
screen as the default slot is a sign that nobody chose a slot.

**5. The contract: one job, one action, a close, and a destination with a fallback.** One job per
display. The action leads inside the product, by deep link, to the screen where the job gets done:
the cart, the category, settings, the profile. The destination has to keep the session and the
sign-in; a link that opens a browser where the person is not recognized is a destination defect,
and defects of this kind live on one platform, so test on each. A close always exists and costs one
tap; the system back control and the dismiss gesture have to work. `email-copy`'s rule that every
claim carries a fact you can point at carries over with the screen as its unit: the price, the
availability and the size of the benefit
named in the message have to be true on the destination screen at the time of display.

**6. Set the expiry from the content, and keep it with the queued message.** Because the message
waits for the person, every message has an expiry. A one-day offer ends with itself; a what's new
note ends with the next release; a survey ends with its collection window; a points reminder ends
on the expiry date of the points. A standing ask (notification permission) has no expiry and is
bounded by frequency instead. At display time the rule re-reads eligibility and expiry: the person
may have done the thing since the message was queued. Expired unseen is a recorded outcome, not a
silent disappearance.

**7. Completion is the event at the destination, not the tap.** Permission granted, read from the
system through the endpoint registry of `push-notifications`. Field saved. App updated, read as
leaving the old version segment. Survey submitted. Game played through to the prize: the participant
is whoever reached the end, not whoever tapped. For a promotion, the destination reached and the
promoted action taken: the item added, the code applied. A service message completes by being
displayed; a mandatory notice by being displayed, or by the acknowledgment when it asks for one.
Guidance completes when the step it pointed to gets done. A destination outside the product, such as
the system settings behind a re-ask screen, completes on the person's first return to the product
after the display, credited to the display's session. A store rating request has no completion the
product reads: the platform decides whether the card appears at all, so record the call as
requested. Record an outcome for every display, against the person and the session: shown, tapped,
completed, closed, interrupted, expired unseen.

**8. Guidance: a step shows when the person reaches it, one element at a time, and completes by
the event.** A tour that fires every step at first launch is a series of modals. Instead, each step
is keyed to a screen and a state (has not used X, is on the screen where X lives), highlights one
element, and a close skips this step, not the sequence. A what's new note is guidance only on the
screen where the feature lives and only for people who have not used it; to those who use it, it is
noise. Guidance about an element people confuse with another one hangs on the confusing action
itself. A sequence retires when the
share of people completing a step among those who reached it stops growing, read by install cohort;
the threshold is a parameter from your own data.

**9. Register the row and its owner; the register is where the class gets checked.** Every message
has an owner responsible for its expiry and retirement. The register is also where the question
`transactional-messaging` leaves open, when a service message became a marketing one, is answered
for the product surface: a promotional block inside a message in a service slot changes the class at
registration, and the display rule reads the class field. A change of class is therefore always
visible as an edit to a row, not as a quiet change of content.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Delay of a blocking display on the entry screen | after the person's first action on the screen; the size from your distribution of time to first action there | parameter |
| Expiry of a message | from the content: the end of the offer, the next release, the survey's collection window, the points' expiry date | parameter |
| Completion window for a promotion | inside the session of the display; anything later is attribution, not completion | follows from the definition |
| Retiring a guidance sequence | the share completing the step among those who reached it stops growing across install cohorts | parameter |
| Store rating request, iOS | the system shows the prompt at most three times in a 365-day period; people can turn review requests off for good; not at launch, not as the result of an action by the person | platform rule, Apple, StoreKit "Requesting App Store reviews", opened 2026-09-13 |
| Store rating request, Google Play | a time-bound quota, unpublished and subject to change; no question before or during the card, "do you like the app" included; no button of your own that triggers the request | platform rule, Google Play In-App Reviews API, opened 2026-09-13 |
| Asking again for consent to a data-for-discount exchange after a refusal, California | not before 12 months have passed | statute, Cal. Civ. Code §1798.125(b)(3), opened 2026-09-13 |

The first four are yours. The last three are dictated from outside, and each carries its source in
`SKILL.md`, with the people it does not bind.

## Edge cases

- **A session before sign-in.** An install exists and a person does not. First-run guidance and the
  pre-permission screen show; messages whose eligibility reads the profile do not. State lives on
  the install until sign-in, then merges into the person's record (`list-building`); what the
  anonymous install saw is not shown a second time to the same person after sign-in, provided the
  merge worked.
- **Two devices.** Message state sits on the person, the display on the session: closed on the phone
  means closed on the tablet; an item in the notification center read on one is read on both.
  Eligibility is read from the server, not from the device, or one person gets one display per
  device.
- **A web product.** The signed-in area of a site lives by these rules; the public pages of the same
  site live by `onsite-capture`'s display rule. The browser's back button is a close path. The
  site's widget layer and the product's layer have to see each other, which is step 7 of the
  neighbor's rule; otherwise the person crossing from the catalog into the account gets both.
- **Arrival through a deep link from an external message.** The arrival screen is protected for
  this session: nothing blocking until the person's first action. A queued message waits for the
  next screen or the next session.
- **An app version without the feature, or without the display layer.** A message about a feature
  shows only to versions that have it. Installs on an SDK version that cannot display anything
  show nothing; their share is read in the reach of eligible appearances (`SKILL.md`), and it is not
  restraint.
- **Local time.** "Tonight until midnight" runs on the person's clock, not the server's; so does the
  expiry.
- **Accessibility.** A blocking display closes with the system gesture and from a screen reader;
  otherwise the product is locked for part of its people.

## Failure modes

**The register lives in three systems.** The vendor SDK's in-app messages, banners the developers
built into screens, and the notification center each keep their own rule and their own count, and
the person gets the sum. Diagnose it by asking where the class and the budget are read for a banner
built into a screen, and getting no answer. In the data it shows as display events with no decision
record (`session-budget-and-precedence.md`, step 8). The remedy is one register and one executing
layer, `session-budget-and-precedence.md`, step 7.

**A custom integration loses events.** Not every display and tap reaches the system. The share
completing among those shown can read anything, and reach reads low. Check absolutes, not the ratio,
in two joins. A decision logged as shown with no display event from the surface is a telemetry hole.
An appearance of an eligible person on the slot's screen with no decision logged at all (shown,
deferred, blocked, held or suppressed) means the layer did not see the session: screen events lost
on the way in, or eligibility not recomputed. Neither is restraint.

**A message shows after its end, or to people who already did the thing.** The symptom: the share
completing falls toward zero while reach holds. Two causes, and taps tell them apart. Taps hold
while completion falls: the destination broke, a deep link after a release, a session lost in a
browser, found by splitting platforms. Taps fall together with completion: the message itself, an
expired one with no expiry set, an eligibility not re-read at display time, or a pitch the person
already saw everywhere else (`handoff-with-outside-channels.md`); the last one shows as reachability
loss in the outside channels growing over the same period.
