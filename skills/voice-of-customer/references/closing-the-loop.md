---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Closing the loop with the person: obligation, route, promised time, closure

The unit here is **the obligation**: an answer that requires an action toward the person who gave it.

An issue, its closure event and its reopen rule belong to `chat-and-bots`; a remedy issued as a code or a credit
belongs to `offer-design`; open obligations past their promised time are a duty signal for
`program-audit-and-ops`. The word "promised time" is shared with `transactional-messaging`: a time the company
named to the person, with a timer on it.

## Entry conditions

An answer arrived with a key, or a public review was identified through an order number, and it meets one of
these conditions: the score is below the threshold of its scale; the text names a problem, at any score (five
stars with a complaint in the text is an obligation); the person asked to be contacted; the review is negative
and identified; a complaint arrived on its own as an answer to an experience, through a form, an email or a
chat (the issue is `chat-and-bots`'; here it is an obligation once it answers an experience). A route exists for
the experience type: a table of experience type and theme to owner, and a written promised time.

## Exit conditions

The obligation is closed with an outcome and a cause code: the person confirmed the matter is settled; or the
quiet period of the topic passed after the last substantive reply with no return; or the promised fix was
delivered as an event (replacement received, refund landed). The closure record carries the date, the outcome,
the cause code and the part of the experience. "Unreachable after the attempts" and "declined contact in the
answer" are separate outcomes: the first is not closed; the second never opened an obligation.

## Steps

**1. Set the threshold per scale, and two speeds.** On the recommend scale, the scores that the NPS definition
of `metric-definitions` subtracts, six and below on zero to ten, open an obligation. The bottom of the scale gets the fast route: as a starting point, the
lowest third of the scale; that holds on scales with ten or more points, and it is replaced by your own
distribution of outcomes by score, where the share of fixed and compensated outcomes jumps as the score falls.
On a satisfaction scale, everything below the satisfied options opens an obligation, by the neighbor's
definition of CSAT. A text naming a problem opens an obligation at any score. The threshold is written into the
instrument version; a change of threshold is a new version.

**2. Route to the owner of the part of the experience, not to marketing.** A table of experience type and theme
to owner: a store to its director; delivery to the carrier desk; a product to the category owner or the
supplier desk; a conversation to its assignee, while the issue stays closed at `chat-and-bots`, whose rule does
not count a survey reply as a return, and what the assignee writes to the person runs in that thread under the
neighbor's marks; a flow or a message to
the owner of the flow; an unknown theme to the claims desk by default. The owner receives the person, the
experience identifier, the whole answer, and the promised time. A route without an owner is a defect of the
route, not "the shared inbox for now."

**3. Deduplicate against what is already open.** By the experience identifier and the person: when an issue is
already open, or was closed on the same matter and is still inside the settle window of its topic
(`chat-and-bots`), the answer attaches to it and no second contact goes out. When the person has already received a remedy (a refund,
a replacement), the obligation closes with the outcome already remedied, and the answer stays in the reading.
Two contacts on one obligation is a failure mode.

**4. Start the timer from the promised time.** The promised time is the route's written deadline, the same one
named in the ask and in the thank-you (`asking.md`, step 8). The timer starts at the timestamp of the answer,
not when somebody reads it: to take an invented promise, an answer on Friday evening with "two business days"
runs out on Tuesday, not on Thursday. A promise made inside a reply ("we will call you back tomorrow") starts a new timer
(`transactional-messaging`: every promised time carries one), and the obligation is on time only when every
timer on it brought its event: the reply by the route's time, the callback by tomorrow, the replacement by the
day the reply named. A reply that arrives by its time and only names a later date keeps the timer and spends a
promise; read promises per obligation beside the share. A route with no written promised time is a
defect: its obligations count as not closed on time. For a public review, the answer's timestamp is the
posting: identification later does not move the timer, the way reading on Tuesday does not.

**5. The first substantive reply: name the experience, ask for what is missing, say what happens next.** A
template apology does not count. The order is named; the problem is stated in the person's words; one question goes out when
a fact is missing (an order number, a photo, a date); and the reply says what happens next, with a new promised
time. The channel is the one the person answered in; a call goes out when the person asked for one or when the
route is the fast one. The reply to an obligation is what the person is waiting for as a consequence of their own
action, so it is exempt from the cap (`contact-orchestration`); the ask had no such exemption. For a negative
public review that is not identified, reply publicly with the way into the route and without arguing; the
obligation opens when the person is identified.

**6. Remedy by written policy, not by score.** A table of theme to remedy (replacement, refund, credit,
explanation only) is written before launch. The score chooses the speed and the route, never the remedy. A
remedy in the form of a code is `offer-design`'s construction (margin, terms, expiry). A remedy is never
conditioned on changing or removing a public review (the legal regime in `SKILL.md`). When the company was
right, explain and close with the outcome explained; do not compensate for persistence.

**7. Hold the loop until it is closed.** Closed means the person confirmed; or the quiet period of the topic
passed after the last substantive reply with no return, the period being the one the topic gets from
`chat-and-bots`, which is the time a person needs to act on the reply, and set per theme the same way where no
chat program runs; or the fix arrived as an event (replacement received). An answer about something that is not
yours ("the sea was dirty") closes with the outcome out of scope once you have told the person so. Unreachable
after the attempts in more than one channel, the number of attempts being a parameter of the route, is the
outcome unreachable and is not closed: the ask promised something the company could not deliver. It still
ends: the obligation leaves the owner's queue and the suppression on asks, stays in the control metric as not
closed, and reopens on the next signal from the person. A return of the same person about the same experience
inside the window is a reopen of the same obligation, not a new one.

**8. Record the closure.** The outcome (fixed, explained, compensated, already remedied, unreachable, out of
scope: "the sea was dirty"), the cause code (the theme), the part of the experience, the time to the first
substantive reply, the time to closure. The cause code feeds `reading-and-change.md`; a closure without a cause
code is not a closure.

**9. Return the person to the program.** After closure, and after the outcome unreachable, the suppression on
asks is lifted; the next ask waits for the ration window. No automatic "sorry discount" goes out unless the policy says so. When a change comes
out of the theme this person raised, it reaches them through `reading-and-change.md`, step 10.

**10. Read the loop.** The closed-on-time share (the control metric in `SKILL.md`), the time to the first
substantive reply, the time to closure, promises per obligation, outcomes by kind, the share unreachable, the reopen share (a second signal from the same
person about the same experience: a second low score, a public review after a closure, a complaint, a
chargeback), and two contacts per obligation.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Obligation threshold | six and below on the zero to ten recommend scale; below the satisfied options on the satisfaction scale (`metric-definitions`) | 3, from the definition |
| Fast-route boundary | the lowest third of the scale as a starting point; replaced by your own distribution of outcomes by score | 5 |
| Promised time of a route | your own reply capacity per route; named in the ask | 4 |
| Quiet period before closure | the topic's rule in `chat-and-bots`; set per theme the same way where no chat program runs | the neighbor's |
| Attempts before unreachable | a parameter of the route, over more than one channel | 4 |
| Reopen window | the settle window of the topic (`chat-and-bots`) or the return window of the experience | 4 |

## Edge cases

- **A low score, no text, "do not contact me" chosen.** No obligation toward the person; the answer goes to
  the reading; the outcome declined contact is counted apart and is outside the denominator.
- **A negative public review with no identification.** A public reply with the way into the route; the
  obligation opens on identification; until then it sits in the count of unidentified negative reviews next
  to the metric. Once open, its timer runs from the posting, so a review found after its promised time is not
  closed on time, and it belongs to the period of the posting; the lag from posting to identification is the
  loop's own lag and is read beside the share.
- **A wave.** Many low scores on one part inside a short window (a batch, an outage): one cause, many
  obligations. The reply may be common to everyone affected, and it is substantive when it names the cause and
  what happens next for each affected experience; a person whose text names anything beyond the common cause
  gets an individual reply. The closure is per person, by that person's fix event, confirmation or quiet period;
  the common reply closes nobody by itself. The wave is a candidate incident for `program-audit-and-ops`.
- **An employee named in the text.** The route is the same; access to the text is limited to the owner of the
  part (the employee's personal data, in `SKILL.md`); the reading attributes to the shift and the batch before
  the person.
- **A late answer**, after the ask's window. The obligation opens anyway; the answer does not count toward
  the ration.
- **A high score and a complaint through another channel in the same period.** A reopen of the obligation if
  there was one, otherwise a new obligation from the complaint; the score stays in the reading with a
  contradiction flag.
- **An answer on behalf of an organization.** The obligation is toward the person at the account; the route
  goes to the account executive before the deal or the account manager after it (`b2b-lifecycle`,
  `b2b-retention`); the closure goes to the person who answered, with that executive or manager copied.

## Failure modes

**The loop became an acknowledgement.** "Thank you, we will look into it" counts as a closure. Sign: the time
to the first reply near zero; the reopen share rising; negative public reviews after "closed." Remedy: closure
only by the three conditions of step 7.

**The route into marketing.** Low scores reach the messaging team, which has no authority over the store or
the supplier; "closed" means "forwarded." Sign: cause codes empty; outcomes read forwarded. Remedy: the owner
table by part of the experience.

**The score picks the remedy.** People learn that one star pays. Sign: the share of the lowest scores rises
while complaints per order through support stay flat; remedies per obligation rise. Remedy: the policy of
remedies by theme; the score sets only the speed.

**The double contact.** The claims desk calls and the program writes. Sign: two contacts per obligation.
Remedy: deduplication by the experience identifier before the first contact.

**The timer from reading.** Friday's answers close "on time" on Tuesday. Sign: the closed-on-time share is
higher for answers that arrived before a weekend. Remedy: the timer from the timestamp of the answer.

**The rolling promise.** Every reply arrives by its time and names a later one; no timer is ever missed and
nothing gets fixed. Sign: promises per obligation and the time to closure rise while the closed-on-time share
holds; the reopen share rises after. Remedy: promises per obligation and the time to closure in the same row as
the share; the owner of the route reads every obligation with more than one postponement by name.

**The remedy conditioned on a review.** "We refund if you remove the review." That is a violation on the
regimes in `SKILL.md` rather than a failure of the metric; its sign is a review mentioned in the correspondence
about a remedy.
