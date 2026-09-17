---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Vocabulary for push-notifications

The terms all three mechanics assume. The last section lists seven words this skill shares with
its neighbors, most of them under different meanings.

## The unit

**Endpoint.** One installed app on one device, or one browser profile on one site. The operating
system or the browser keeps its permission, granted, refused or not yet asked for, and a push service
issues it an address. This is the unit of the skill. A person can have several endpoints; an endpoint can have no person.

**Push token.** The address a push service issues for one endpoint. It can change, and the push
service can reject it.

**Person link.** The dated record that an endpoint belongs to a person, written on sign-in or by
record matching and closed on sign-out. One endpoint, at most one person at a time.

**Install cohort.** Every endpoint whose registry row was created in one period, at the first app
open, usually the installs of one month.

**Check age.** The one age, the same for every cohort, at which the control metric reads a cohort.
Set it from your own data at a late point on the distribution of time from install to the value
moment, not at its median, and change it only with a new baseline.

## The permissions

**Display permission.** The system's or the browser's permission for an endpoint to show
notifications. Held per endpoint, withdrawn by the person at any time, and on some platforms asked
for only once.

**Marketing opt-in.** The person's consent to receive promotional pushes, given through consent
language in the app's interface. A different thing from the display permission, and on apps
distributed through the App Store a condition for sending marketing at all.

**Ask budget.** How many times a platform lets you show its permission prompt, and on what
condition. On iOS it is one. On Android, for an app that targets 12L or lower, one refusal holds
until the app is reinstalled or targets 13 or higher.

**Pre-permission screen.** Your own screen shown before the system prompt. Its yes calls the prompt;
its not now spends nothing.

**Value moment.** An action after which the person has something to receive by push: an order
placed, a reminder set, a price alert requested. The ask is tied to one.

**Re-ask.** A later request to people who refused or switched off, leading to the system settings.
Triggered by a new value moment and capped per person.

## The states

**Displayable endpoint.** Permission to show notifications as alerts granted (on iOS, more than
quiet delivery), token accepted, permission read within the staleness threshold. The numerator of the
control metric. An endpoint with one category switched off stays
displayable for the categories still open.

**Quiet endpoint.** An endpoint whose notifications arrive only in the notification history, without
banner or sound: provisional authorization on iOS, or quiet delivery chosen by the person. Counted
as its own class.

**Marketable endpoint.** A displayable endpoint with the marketing category open and, where the
platform or the basis for sending requires one, a marketing opt-in on record.

**Stale endpoint.** An endpoint whose permission was last read longer ago than your staleness
threshold, set from the usual gap between app opens, so its current state is unknown: the person has
stopped opening the app, has removed it without a send testing the token since, or the app has
stopped reading its settings. Push services have their
own notion of staleness for their registrations; the registry keeps the date and applies yours.

**Retired endpoint.** An endpoint whose token the push service rejected in answer to a send. Its row
closes. Nothing tests the token of an endpoint you do not send to, so a removed app can sit among
stale endpoints instead.

**Category.** A class of notification the person can switch off separately: a notification channel
on Android, a category setting inside your app elsewhere. Designed before launch, because on
Android the app cannot change a channel's behavior once it exists.

**Loss interval.** The span between the last time an endpoint was seen with permission and the
first time it was seen without. A switch-off has no exact date; it has this interval.

## The send

**Fan-out rule.** Which of a person's endpoints receive a message of a given class. Service messages
about an awaited event go to all displayable endpoints; everything else goes to the one used last
among those that may receive the message: displayable, with its category open and, for marketing,
an opt-in on record where one is required.

**Expiry.** The moment after which a push should not be delivered, set from the content. Called
expiration in APNs and time to live in web push.

**Collapse key.** The value that makes a new push replace an earlier one about the same thing.
Called a collapse identifier in APNs and a topic in web push.

**Interruption level.** How forcefully the device presents a notification. On iOS: passive, active,
time sensitive, critical.

**In-channel gap.** The minimum interval between two non-urgent pushes to one person, across all of
their endpoints. A property of the channel, checked at the moment of sending against reserved sends.

---

## Words this skill shares with its neighbors

**Touch.** Not redefined here. In `contact-orchestration` a touch is one delivered message to one
person in one channel, and this skill keeps that meaning on purpose: a message the fan-out rule
delivers to three endpoints is one touch. Endpoints are a delivery detail. That seam is the reason
the fan-out rule writes each message to the log once, against the person.

**Reachable.** In `contact-orchestration` and `list-building`, reachability is a property of a
person in a channel. Here the endpoint-level word is displayable. A person is reachable by push when
at least one of their endpoints is displayable.

**Token.** Here, the push token. In `personalization` a template token is an unresolved placeholder
in a message. Same word, unrelated objects.

**Subscription.** Not used here, for three reasons: `welcome-and-activation` uses it for a person's
arrival, `subscription-retention` for a paid plan, and the web platform for a push endpoint. This
skill says endpoint throughout.

**Provisional.** Here, Apple's term for trial authorization that delivers quietly. In
`metric-definitions` a provisional value is one still settling before its freeze date; in
`crm-program-design` a provisional target is one still waiting for data. Unrelated to either.

**Category.** Here, a class of notification the person switches off separately. In `repeat-purchase`,
`promo-calendar` and `personalization` a category is a group of products, and the fallback screen in
`references/send-construction.md`, step 4, is a product group page in that sense. Same word,
unrelated objects.

**Message class.** Not redefined here. `contact-orchestration` sorts messages into service,
mandatory notice, perishable and personal, automated flow and campaign, and this skill uses those
classes. The fan-out rule and the in-channel gap split one part off service: an event the person is
waiting for.
