---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-14
---

# The preference center and the unsubscribe: what the person chose, how far it reaches, how fast it holds

The unit here is **the instruction**: one recorded choice by the person after the basis exists, about one
scope: a message type on or off, a frequency, a channel, a pause with an end date, or a withdrawal. Each
instruction has a route it was taken through, a scope it reaches, and a deadline by which every sending
system has to honor it. Which basis made the first message lawful is `lawful-basis-and-collection.md`;
applying the resulting suppression to an audience is `email-program`'s step; reading the frequency as a
cap is `contact-orchestration`'s.

## Entry conditions

Basis records exist, and at least one marketing stream sends. Every system that sends can read one
person-level field, or receive a write, within the deadline that applies. Without that, the mechanic can
record instructions and cannot honor them, and that gap is `martech-stack`'s to close before this file is
used.

## Exit conditions

The axes of choice the preference center offers, each mapped to a real stream. The routes an instruction
can be taken through, all writing the same instruction object. A scope for every route and wording. The
unsubscribe page and its order of elements. A propagation deadline per regime and platform, the shortest
applicable, and a honoring log per system. The rule for service rows and the point where their exemption
is lost. The frequency and pause instructions in a form `contact-orchestration` reads. The reading of
instructions per period.

## Steps

**1. Define what the person can choose, and map every choice to a stream.** Four axes:

- **message type**, named in the person's words, not the program's: "sales and offers", "new arrivals",
  "the weekly digest", "surveys and feedback requests" (`voice-of-customer` reads the "no surveys" choice
  here), "reminders about my points";
- **channel**: email, texts, push, messaging apps, each on or off, and push by category where the app
  has categories (`push-notifications`);
- **frequency**: a ceiling the person sets from options you offer, "at most once a week", "once a month",
  built from your own cadence so that each option corresponds to something the program can do;
- **pause**: silence for a term the person picks, with an end date and an automatic resume into the
  normal cadence.

Keep **stop everything** on every page of the preference center: one action to withdraw all marketing
from this sender in this channel. The US commercial email rule allows a menu and requires the option
to stop all; the Canadian mechanism covers "any commercial electronic messages, or any specified
class". For TCPA-covered calls and texts, use the route and scope rules in steps 2 and 3.
Each type and channel on offer corresponds to a stream that exists, and each stream that sends is covered by a type; a
type nobody sends is a lie, and a stream no type covers is one the person cannot switch off. List service
rows and mandatory notices separately. Show which streams continue and which can be stopped (step 6).
Where more than one channel can carry a service row, let the person choose a default.
`transactional-messaging` uses that default and fails over when its conditions are met. `push-notifications` keeps service
and marketing in separate categories so that switching one off does not switch off the other.

**2. Take the instruction through every route, and let every route write the same object.** The routes:

- a link in every marketing message to a page where withdrawal completes in one action. For TCPA-covered
  calls and texts, check the route rule below. The US commercial email rule allows no step beyond
  "sending a reply email or visiting a single page", no fee and no information beyond the email address;
  the Canadian mechanism uses "the same electronic means by which the message
  was sent" or, where not practicable, another electronic means; the CRTC's example of a path through a
  login and a "delete account" page is the path not to build;
- the reply: an email reply that says stop. For TCPA-covered US calls and texts, check whether the
  caller properly designated and disclosed an exclusive method before you decide which requests count.
  A designated keyword reply must accept all the listed words, even if the message names only one.
  Without a valid exclusive designation, process reasonable requests, including replies in ordinary
  language that convey a revocation. See [US TCPA revocation](legal-regimes.md#us-tcpa-revocation);
- the account settings and the preference center reached from them;
- the mailbox provider's one-click, from the header `deliverability` owns; here, what it maps to: the
  widest scope for that channel, the sender as a whole;
- a person: support, a letter, a call, a message on a social account, the sales rep. The GDPR makes
  withdrawal "as easy ... as to give", and the ICO says to publicize the phone route too. The person
  who receives the request logs it with the route "human" and the time of receipt. For TCPA-covered
  traffic, distinguish the recorded request from a valid revocation under the route rule above;
- a spam complaint returned by a mailbox provider's feedback loop: `deliverability` reads it for the
  identity; here it is an instruction of the widest scope for that channel, written the day it arrives;
- a browser signal about sale and sharing (the GPC): an instruction with the scope "sale and sharing",
  not an email withdrawal, read in `processing-beyond-sending.md`, step 7.

Every route writes one instruction object: person, route, scope, timestamp, the wording the person saw
or said. A route that writes to a store of its own, the text provider's own opt-out list, the sales
tool's "do not email" box, is a propagation gap until it is copied into the person-level store; the
honoring log of step 5 is where it shows.

**3. Set the scope of each instruction from the wording it was taken under.** The scope values are
`email-program`'s five, the address or channel, the sender as a whole, one brand, one message type, one
program, plus one from `b2b-lifecycle`: the account. The scope is not chosen by the platform's list
structure; it is read from what the person was offered and what they answered:

- an email one-click header, a reply "stop" to an email, a "stop everything" button: the sender as a
  whole in that channel (`email-program`'s global scope). In email, use the From identity. A brand
  that sends under its own identity is the sender; brands that share one identity are all the sender,
  whatever the platform's lists say;
- a type checkbox: that type, across the brand that holds the preference;
- a brand's own unsubscribe, where brands are separate senders holding separate permissions: that brand;
  a wording that names the group: every brand in it;
- a valid revocation in response to a TCPA-covered US call or text: identify the caller and read the
  content that prompted the request. If it contained advertising or telemarketing, stop all covered
  advertising and telemarketing calls and texts from that caller. If it was informational, you can
  apply the request to the category it targets unless the person expressly revoked more. A number,
  provider list, or brand label alone does not define the caller. See step 6 for affected service rows;
- a request from a role with authority to speak for an organization, "do not write to anyone at X": the
  account, which suppresses the program's touches to every contact of that account; one contact's
  unsubscribe stays that contact's and does not suppress the account (`b2b-lifecycle`).

For covered US calls and texts, apply the FCC scope rule above. Elsewhere, give ambiguous wording the
wider reading. Scopes remove people; none widens a permission. A preference center that lets a person
"subscribe" to a type they had no basis for is writing a basis record, which needs the request of
`lawful-basis-and-collection.md`, step 3, not a checkbox.

**4. Build the unsubscribe page in this order.** First the withdrawal completes: one click from the
message, no login, no reason required, no delay announced. Then the confirmation, on the page: what was
stopped, for which address, and that service messages continue. Then, after the fact and optional, the
alternatives: a type, a frequency, a channel, a pause. Then a way back: a link that starts a new request
(step 8). Then, optional, a reason as choices, one click each, with a free text field nobody has to fill.
No promotion on the page: an offer to stay is a step between the person and the route out, and the US
rule allows none. A forwarded message carries the original recipient's token, so the page names the
address it will affect before it acts, and the person who is not that address sees whose withdrawal they
are about to make. No confirmation email after an email withdrawal: the page confirmed, and a message
after a withdrawal is a send to read against the metric. For covered US calls and texts, the FCC rule
does not require a confirmation. If you use a confirmation text, state what stopped, without promotion
or a question about scope. Apply the revocation without waiting for a reply. See the timing table below.

**5. Propagate inside the shortest applicable window, and log every system's write.** The instruction is
written to the person-level store first. From there it reaches every system that sends under the
company's name: the email platform, the text provider, push, messaging apps, the CRM's sequences, the
call list, the audience exports. Pass along the scope so each system suppresses only the streams the
instruction reaches. The deadline is the shortest of the windows that apply to that channel
and that base: ten business days under the US email rule and the Canadian rule; two days
under Yahoo's requirement for mail to its users; "promptly" under the ICO; "as easy as to give" under
the GDPR. Where no window that applies to a channel is a number, set one of your own for that channel,
no longer than the shortest number that applies to any channel of yours, and record it once: the control
metric reads sends after an instruction against this deadline. Where any Yahoo address is in the base,
two days is the ceiling for email, and refreshing the suppression list faster than that is the practice,
because the law's window and the platform's are both in force and the platform enforces by filtering.
For a valid TCPA revocation, honor it within a reasonable time from receipt, subject to the ceiling in
the timing table below. Cancel queued steps within the withdrawal's scope: flow steps scheduled for
later, a campaign segmented but not sent. A message in flight at the moment of the instruction cannot be
recalled; it is the cost of the lag, and the deadline is measured to the last system's write. The
honoring log holds, per instruction and per system, the time of the write; the maximum across systems is
the lag, and a system with no write by the deadline is the broken link.

**6. Check the basis and scope before keeping a service row.** The US email rule
exempts transactional and relationship messages from most of its provisions; the ICO says routine
customer service is not direct marketing; in Canada the service message is exempt from the consent
requirement and still carries an unsubscribe mechanism. What the person's unsubscribe from a Canadian
service message does is a question for counsel. For TCPA-covered US calls and texts, apply step 3. A
marketing revocation does not by itself stop a separate informational stream whose basis remains valid.
A valid revocation that reaches an informational category stops use of the revoked consent for that
category. If that interrupts a required notice, use `transactional-messaging`'s failover to a channel
with a valid basis. A separate number or a service label does not preserve revoked consent. Ask counsel
if you cannot establish that the rule applies or that the affected stream still has a basis. Hold
the affected stream while the basis is unresolved.
The exemption is lost by content, in each regime by its own test (`transactional-messaging`, class
check at the template version and at the send). From the version that carried promotion, the row is a
marketing send for this skill: the instruction applies to it, and it leaves the "continuing" list of
step 1. The sign that this went wrong: a promotional block switched on by the recipient's consent flag
without a change of class, so the message goes out from the service identity, with no unsubscribe, to
people who withdrew.

**7. Write the frequency and the pause as instructions `contact-orchestration` can read.** "Less often"
is written as a value from the options of step 1; the cap reads it and lets it win when it is lower and
not when it is higher. A pause is written with its end date; during it, marketing to the person is
suppressed, not deferred, so the resume is into the normal cadence and not into the backlog. The resume
needs no new request: the basis persisted through the pause. If the basis ends during the pause, the
record ends on its own date, and nothing resumes. No message goes out to announce the end of a pause.

**8. Re-subscribe only through a request.** A person who withdrew comes back through a new request in
the sense of `lawful-basis-and-collection.md`, step 3, from any point, with a new record. A person who
asks support to put them back gives express consent by that request; the ticket is the record, with who,
when, how and what was said. Nobody is re-subscribed on the program's initiative, and a withdrawn person
is not written to with an offer to return (`lapse-and-winback` states the same from its side: refused
means no repeat attempt).

**9. Read the instructions each period.** Instructions by route and by scope; the kept share, instructions
that chose a type, a frequency, a channel or a pause instead of the withdrawal; the honoring lag per
system against the deadline; sends after an instruction, by system; complaints arriving as instructions.
A route with no instructions in a period is a route that does not work, not a happy base: test it with a
withdrawal of your own.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| US email: honor an opt-out within 10 business days; the mechanism works for at least 30 days after the send; no fee, no information beyond the address, no step beyond a reply or a single page | FTC compliance guide, opened 2026-09-14 | legal |
| TCPA-covered US calls and texts: honor a valid revocation within a reasonable time, at most 10 business days from receipt. An optional text that only confirms the revocation and carries no promotion is presumed within prior express consent if sent within 5 minutes of receipt; later, show that the delay was reasonable | [US TCPA revocation](legal-regimes.md#us-tcpa-revocation), FCC 26-67, opened 2026-11-21 | legal |
| Canada: effect given without delay and no later than 10 business days; the address or page valid for at least 60 days after the send; no further action by the person | CASL section 11(2) and (3), opened 2026-09-14 | legal |
| Yahoo: honor unsubscribes within 2 days | Yahoo sender best practices, opened 2026-09-14; a platform rule | platform |
| UK and EU: "promptly"; "as easy to withdraw as to give" | ICO PECR guidance; GDPR Article 7(3), opened 2026-09-14 | legal |
| Options for frequency | your own cadence: the intervals the program can keep | parameter |
| Length of a pause | the person's choice from options you offer; offer terms shorter than the lifetime of your shortest event-based basis, so a pause does not outlive the record | parameter |
| Reason choices on the page | yours, one click each, optional | parameter |

The legal rows carry their sources and the people they do not bind in `legal-regimes.md`; the platform row binds
mail to that provider's users and nobody else. The rest are yours.

## Edge cases

- **The request arrives on paper, by phone or in a chat.** The person who receives it logs the request
  with route "human" and the time of receipt. For covered US calls or texts, apply the route check in
  step 2 before recording a TCPA revocation. If the request qualifies, measure the deadline from
  receipt, not from the time someone finds the note.
- **An unsubscribe from one address of a merged person.** The scope is the person, not the address, when
  the wording said "stop writing to me"; the second address is suppressed with the first. A type
  preference set on one address is a preference of the person as well.
- **A spam complaint from a mailbox provider.** An instruction of the widest scope for that channel, the
  day it arrives, whatever the program thinks the person meant.
- **A withdrawal while a campaign is in flight.** The send that already left counts as the cost of the
  lag; the send scheduled for tomorrow is canceled. Read the two apart in the honoring log.
- **STOP on a short code that serves several programs.** For a valid TCPA revocation, apply the
  advertising or informational scope from step 3 across the caller's systems. Keep provider blocks
  separate from that decision. If a required service row loses its basis on this channel, use the
  failover in step 6.
- **A one-time code the person asks for after STOP.** Keep the stop entry and log the separate request
  and its time. Check [the FCC ruling on a separately requested code](legal-regimes.md#us-requested-code)
  for the conditions and the question for counsel. The request does not lift the provider's block.
- **A one-click from a service message.** The header belongs on marketing and subscribed messages; a
  service message does not need it (`deliverability`). Where a service message carries one, the click
  is a withdrawal of the sender's marketing in that channel, and the service row continues.
- **A person whose basis ends during a pause.** No resume; the record ended. The person can come back
  through a point.
- **The preference center reached by somebody who is not the person.** The center changes preferences
  and withdraws; it does not show the person's data beyond the address or number it will act on, so a
  forwarded link cannot be used to read a profile.
- **A group of brands with one center.** Each brand's types are listed under the brand; "stop
  everything" names its scope on the button: this brand, or all brands of the group, as the request of
  `lawful-basis-and-collection.md`, step 3, named them. Apply step 3 to find the email sender or the
  caller for a covered US call or text. A shared center does not turn independent callers into one.
- **A parent's instruction about a child's data.** Written as the parent's, with the scope of the child's
  record, and read in `processing-beyond-sending.md`, step 4.
- **An instruction from a role with authority in an organization.** Account scope; the record names the
  role and the date; `b2b-lifecycle` suppresses the program's touches and lets the account executive's
  correspondence on an open deal continue, which is not a touch of the program.

## Failure modes

**Honored in one system only.** Signs: sends after an instruction concentrate in one system, the text
provider, the sales sequences, a second email platform; the honoring log shows no write from that system
or a write past the deadline; complaints come from people who unsubscribed. Remedy: step 5, one
person-level store, a write per system with a log, and the system with no write taken off sending until
it reads the store.

**The page that adds steps.** Signs: the unsubscribe rate falls while complaints rise, because people
who cannot find the way out mark the message as spam; the page asks for a login, a reason before acting,
or announces a delay ("within 24 hours", to take a made-up wording); the CRTC's example path exists on your site. Remedy: step 4.

**The center that widens permission.** Signs: basis records whose source is the preference center and
whose wording version is empty; people with a requested message state shown marketing types ticked by
default and "saved" into marketing. Remedy: step 3, the center writes narrowing instructions freely and
widening ones only through a request.

**The pause that ends in a burst.** Signs: sends per person on the day a pause ends exceed the cadence;
deferred messages queued during the pause go out together. Remedy: step 7, suppression during the pause
and a resume into the cadence, not the backlog.

**The service row that lost its exemption unnoticed.** Signs: a promotional block appears in the order
confirmation of people who withdrew, from the service identity, without an unsubscribe link; the
change was made by content, not by a change of class. Remedy: step 6 and `transactional-messaging`'s
class check at the template version.
