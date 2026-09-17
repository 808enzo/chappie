---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Asking for permission, and not wasting it

The unit here is **an ask on an endpoint**. An endpoint is one installed app on one device, or one
browser profile on one site: the operating system or the browser keeps its permission, granted,
refused or not yet asked for, and a push service issues it an address. A person can have several; an
endpoint can have no person.

Push differs from every other channel in this library in one respect that shapes this file: the
permission is granted by the system to the app, per endpoint, and the system decides how many
times you get to ask. On some platforms the answer is once.

## Entry conditions

An app or a site exists, and **what the pushes are for is written down**: which classes of message
will arrive (service notices, alerts the person asked for, automated flows, campaigns) and roughly
how often. You know which actions in the product leave the person with something to wait for.
Your Android app targets Android 13 or higher; below that, the system picks the moment of the ask
for you (see step 2).

## Exit conditions

Named: the promise the ask makes, by class and frequency; the value moment each ask is tied to;
the pre-permission screen and its wording; the sequence on each platform and what that platform
allows; the re-ask path and its ceiling; the record of every ask on the endpoint. Two people
reading the record agree on what the person was promised.

## Steps

**1. Write the promise before you ask.** An ask promises content: which classes will arrive and
about how often. The frequency you promise is part of the basis on which you send, not a courtesy
(`contact-orchestration` holds the same rule for every channel), and you keep it.

**2. Count the ask budget on each platform.** The system prompt is a resource you spend.

- **iOS.** The first authorization request shows the prompt and records the answer; later requests
  do not prompt the person. After a refusal, the way back runs through the phone's settings.
- **Android 13 and higher.** Notifications from a newly installed app are off by default. An app
  that targets Android 13 or higher decides when the permission dialog appears. An app that targets
  12L or lower gets the dialog shown by the system the first time it starts an activity after
  creating a notification channel, which is usually at startup: the moment has been chosen for you.
  For such an app, a single tap on Don't allow holds until the person reinstalls the app or you move
  its target to 13 or higher. A refusal given on an older Android version persists when the device
  upgrades.
- **Web.** Each browser sets its own rule, so check the ones your visitors use. From Firefox 72, a
  prompt requested without a tap, a click or a key press shows only as a small icon in the address
  bar. On iPhone and iPad, web push exists from iOS and iPadOS 16.4 for web apps added to the Home
  Screen, and the request has to answer a direct action, such as tapping a subscribe button.

Each of these is a platform limit with a primary source (listed at the end of this file). They
change with the platforms, so check the date on the source before you rely on one.

**3. Put your own screen in front of the system prompt.** It says what will arrive and how often,
and it offers two answers. Yes calls the system prompt. Not now closes your screen and spends
nothing. A refusal on your screen costs you nothing. A refusal in the system prompt is what the
budget in step 2 counts: on iOS, and in an Android app that targets 12L or lower, it costs you the
endpoint. Neither platform requires the screen. Android's flow shows an explanation screen only when
the system reports that one is due, and Apple's guidance is to ask in a context that shows the
person why. You build the screen for the reasons in this step and in step 5.

**4. Ask at a value moment, never cold on first launch.** A value moment is an action after which
the person has something to receive: they placed an order and will want its status, set a first
reminder, subscribed to a price drop or a restock, followed an author. Both platforms' own
documentation uses moments of this kind as examples.

Practitioners disagree about the first session. One team moved the screen to the second session;
another found the first session converted best. The disagreement dissolves once you notice that a
session count is a stand-in for a value moment. Tie the ask to the action, and keep the session
count as what it always was, an approximation to use until you have found the action.

**5. Make the pre-permission screen carry marketing consent.** Apple's App Review Guideline 4.5.4
allows push for promotions or direct marketing only where people have explicitly opted in through
consent language shown in the app's interface, and only where the app gives them a way to opt out.
The system prompt carries no such language: it asks permission to display notifications, not
consent to receive marketing. So there are **two permissions**, the system's display permission
and the person's marketing opt-in. A pre-permission screen that names marketing outright is that
consent language. Record what it said.
**Who this does not bind:** web push, and apps distributed outside the App Store; the guideline is
a platform rule enforced through review, not a statute.

**6. Treat provisional authorization on iOS as a separate move.** An app can obtain a trial
authorization without any prompt. Its notifications then arrive quietly: no sound, no banner, not
on the lock screen, only in the history of the notification center, with buttons to keep them or
turn them off. A person who chooses Keep then picks between immediate delivery, which is still
quiet and grants no alerts, sounds or badges, and delivery in the scheduled summary. The move makes
sense where a real notification persuades better than a screen does, because the person decides by
looking at one. Since it shows no prompt, Apple allows the provisional request on first launch; the
person is asked to keep or turn off only when a notification arrives. Two consequences follow. The
first quiet notifications have to be the best you have, since the person decides on them. And a
quiet endpoint is not an endpoint that shows banners; the registry and the control metric keep it
as its own class. Apple's page names one way from quiet delivery to banners: the person changing the
app's notification settings. A quiet endpoint the person kept therefore reaches the displayable class through
the re-ask path in step 7, on a new value moment.

**7. Build the re-ask path.** For people who refused or later turned notifications off: a screen
inside the app that takes them to the system settings. Two rules govern it.

- **A re-ask is triggered by a new value moment**, one the person did not have when they said no,
  and never by a timer alone. A first order from somebody who refused on first launch is such a
  moment.
- **Re-asks have a ceiling per person**, and every one is recorded. You set the ceiling from your
  own data. A screen shown again and again risks becoming the very noise that made the person switch
  notifications off.

**8. Record the ask on the endpoint.** Which screen, at which moment, with which promise, the
answer on your screen, the answer in the system prompt, and the date. The record serves three
purposes: keeping the promise, reading permission by ask moment, and evidencing marketing consent
wherever it is required.

## Thresholds and timings

| Quantity | Value |
|---|---|
| iOS system prompt | shown once; after that, only the settings |
| Android 13 and higher, app targeting 13 or higher | notifications off by default, the app chooses when to ask |
| Android, app targeting 12L or lower | the system shows the dialog when the first channel is created; one refusal holds until reinstall or a target of 13 |
| Browser prompt, Firefox 72 and later | without an action by the person, only an icon in the address bar |
| Web push on iPhone and iPad | from 16.4, Home Screen web apps only, request tied to a direct action |
| Re-asks per person | a ceiling you set and record |

The first five rows are platform limits. The last is yours.

## Edge cases

- **The app still targets 12L or lower.** The system shows the prompt at startup, so steps 3 and 4
  do nothing on Android. That argues for moving the target, not for building a screen nobody will
  see before the prompt.
- **A refusal survived an upgrade.** Somebody who switched notifications off on an older Android
  version is still switched off after the move to 13. Do not ask them as if they were new.
- **Several endpoints, different answers.** Allowed on the phone, refused on the tablet. The
  answer is recorded per endpoint, and one endpoint's answer is never inferred from another's.
- **A shared device.** A family tablet, a work computer. The endpoint gave permission, not a
  person. The registry records whose account is signed in, not who holds the device
  (`references/endpoint-registry.md`, the person link), so keep personal details behind the tap
  (`references/send-construction.md`, step 5).
- **Children.** In the UK, the ICO's children's code guidance says non-essential push notifications
  based on personal data, with a nudge to return after a period of inactivity as its example, are
  switched off by default for child users, while notifications essential to the service's core
  function may be on by default.
  **Who this does not bind:** general service notifications pushed to all users without using
  personal data to target them, which the ICO places outside the scope of the code.
- **A web visitor on an iPhone in an ordinary browser tab.** They cannot be asked at all. Whether
  the site shows them an invitation is `onsite-capture`'s display rule; what belongs here is the
  fact that no endpoint will result.
- **A bonus for subscribing.** A code in exchange for the permission can recruit people who take the
  code and then switch notifications off. Compare the share of switch-offs in the first weeks of the
  bonus cohort with a cohort that got no bonus; without that comparison the bonus reads as growth.

## Failure modes

**The prompt was spent on first launch.** Permission on iOS is low and nothing but the settings can
recover it. The sign: in the ask record (step 8), the asks sit on first launch, before any value
moment. A large refused class beside an almost empty never asked says only that everybody was asked:
an app whose value moment comes at install shows the same split with the ask in the right place.

**The promise was not kept.** The screen promised order updates and promotions arrived. The sign:
switch-offs cluster after the first marketing send among people who were promised service messages
only. For an app distributed through the App Store this also breaches guideline 4.5.4, because the
marketing consent was never given.

**Permission is read on the wrong denominator.** The share who agreed is computed over the people
who saw the prompt rather than over every install. The sign: the figure looks healthy while never
asked is the largest class when the install cohort is split by state. The control metric in
`SKILL.md` counts every endpoint for exactly this reason.

**Sources for the platform limits in this file, each opened 2026-09-11.**

- Apple, App Review Guidelines, 4.5.4 (Push Notifications):
  https://developer.apple.com/app-store/review/guidelines/
- Apple Developer Documentation, Asking permission to use notifications (first request, provisional
  authorization): https://developer.apple.com/documentation/usernotifications/asking-permission-to-use-notifications
- Android Developers, Notification runtime permission (Android 13, targeting, the recommended
  flow): https://developer.android.com/develop/ui/views/notifications/notification-permission
- Mozilla, Restricting notification permission prompts in Firefox (Firefox 72):
  https://blog.mozilla.org/futurereleases/2019/11/04/restricting-notification-permission-prompts-in-firefox/
- WebKit, Web Push for Web Apps on iOS and iPadOS (16.4, Home Screen web apps, direct interaction):
  https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/
- ICO, FAQs on the 15 standards of the Children's code (push notifications):
  https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/faqs-on-the-15-standards-of-the-children-s-code/
