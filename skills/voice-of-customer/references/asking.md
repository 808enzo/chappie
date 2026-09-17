---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# The ask: what to ask about, when, whom, with which questions, and how often

The unit here is **the ask**: one request to one person about one experience. An experience is an order, a
visit, a conversation, a refund, a cancellation, the end of a service, or silence after an expected purchase.

The closing state an ask waits for comes from the status map of `transactional-messaging`; the closure of a
conversation comes from `chat-and-bots`. The form of the trigger definition (event, delay, expiry, fallback
mechanics) is `triggered-messages`'; the display rule of a survey on the site is `onsite-capture`'s, and its
carrier inside the app is `in-product-messaging`'s. The steps after a low score are in `closing-the-loop.md`.

## Entry conditions

- The experience has a recorded closing state after which the person can judge it: delivery confirmed, order
  picked up, issue closed, refund landed, trip ended, order canceled, expected purchase not made (the lapse
  threshold is `repeat-purchase`'s and `lapse-and-winback`'s). States come from the map of internal statuses
  to states a person can see, not from the internal status itself.
- The person is identified by a key and reachable in at least one channel (`list-building`).
- **A route for a low score exists: it has an owner and a written promised time** (`closing-the-loop.md`). An
  ask with no route collects obligations nobody will meet. Launch with the one experience type whose route
  exists, then add the next.

## Exit conditions

The ask went out inside its window or expired. The answer is written to the person's record by key, with the
experience, the date and the instrument version. The person's ration is updated. The ask's events went to the
contact log and to the heartbeat of the flow.

## Steps

**1. Choose the experience type and its closing state.** One experience type, one ask: an order, a store
visit, a conversation, a refund, a cancellation, the end of a service, silence after an expected purchase. The
state is the one the person sees, from the status map of `transactional-messaging`, not the internal status:
"delivered" in the order system arrives when the carrier reports it, which is not when the person has the
parcel in hand. For a conversation, the state is the closure by the rule of the topic (`chat-and-bots`); for a
refund, it is the money landing on the card, not the request being accepted, with a check that no new purchase
happened in between.

**2. Set the judging point: the closing state plus the time a defect takes to show.** Do not ask at the peak
of the emotion. Ask about a delivery or a conversation at the closing state itself: a defect, if there is one, has
already shown. Ask about a product after the time it takes to use it. Ask about something perishable before
the guarantee runs out, close enough to its end that a defect has had time to appear and early enough that a
replacement is still possible. The time a defect takes to show is a parameter from your own
data: the distribution of lags from delivery to a complaint about this kind of product, read from support; the
judging point sits where the bulk of the complaints that will come at all have come, and no later than the end
of the return or replacement window. Where no such series exists (a service, a digital product, a category
people leave rather than complain about), the judging point is the closing state itself, and it does not move
until a series exists: complaints that arrive on their own (`closing-the-loop.md`, entry conditions) and return
or replacement requests, each recorded with its lag from the closing state, build one. An experience with no return window and no
lag has its judging point at the closing state. For a cancellation, the judging point is the cancellation itself, and the ask goes out only
when no reason was given at the moment of canceling. For silence after an expected purchase, the neighbor's threshold
sets the moment; this skill only supplies the questions.

**3. The population is everyone who had the experience.** Not "those likely to be satisfied," not "the active
ones," not "those with no open complaint on another order." When the channel is paid and the budget is limited,
take a random sample and record the sampling fraction with the instrument version, so that the response share is
computed on the asked and coverage on the experiences. People with no reachable channel go into the denominator
of coverage, not into the denominator of the response share.

**4. One overall question first, then the branch, then one free-text field.** The overall question about the
experience (would you recommend, how satisfied were you with this experience; the scale and the bands are
`metric-definitions`') goes first or alone. Specific questions come after it, never before: an overall score
read after specific ones is a different measurement from the same question asked first, and the version has to
say which. The branch by score: a low score opens "what went wrong" with options from the theme list
(`reading-and-change.md`), a text field, and "may we contact you"; a middle score opens "what would you
improve"; a high score opens "what stood out." When a third party delivered a part of the experience (the
carrier, the hotel, the marketplace), ask two questions about two parts, so that an answer about theirs does not
land on yours. The scale is fixed and versioned; a change of scale, wording or order is a new instrument version
(step 10). A long questionnaire is a separate research ask with its own ration, not a tail on the score.

**5. Carrier and fallback.** Where the experience happened inside the product, the first carrier is a screen of
the product: which screens, for how long, one display, and who counts as a participant are
`in-product-messaging`'s; an ask that the next session may not reach travels by email or push under that
neighbor's rule. Then email, then push; text messages and other paid channels come last and under a budget.
Fallback is sequential and fires on non-delivery only: the next channel goes when the previous one reports
that it did not deliver (a bounce, no token, a platform failure), never in parallel, and the fallback inherits
the ask's window. Silence is not non-delivery: a delivered ask with no answer gets the one reminder of step 7
and nothing else, on the same channel or on the next one in this order. A prompt on the
site for a person who returns without having answered from the email carries this skill's question under
`onsite-capture`'s display rule; it is the reminder when it shows, not a third touch. Whether one channel beats
a cascade is a test for `experiments-and-holdouts`, not a rule.

**6. The ask carries the key.** The link or the button holds the identifier of the person and of the experience:
no sign-in, no contact fields. An answer with no key (a kiosk at the register, an anonymous form) goes to the
reading only; it reaches no record and opens no obligation toward anyone.

**7. Ration per person.** One person gets at most one ask per experience type per window. Set the window per
experience type, from the base and not from the person: as a starting point, the base's median
interpurchase interval for the category (the interval is `repeat-purchase`'s term), and never shorter than the
time a loop takes to close. That holds in categories with repeat purchase; replace it with your own
distribution of time to the next experience of that type once you have one. The person's own interval is the
wrong anchor: it shrinks the window for exactly the people who have the most experiences, and a daily buyer
gets asked daily. Three orders in a month get one ask, about the latest order. A relational ask (about the relationship rather than an
experience) runs on the program's calendar and carries a lifetime cap per person, a parameter of the program.
One reminder goes to those who did not answer when half the window has passed; there is no second one; the
vote counts once. Do not condition the reminder on opens: opens are loaded by machines (`email-copy`). Do not
ask a person with an open loop (`closing-the-loop.md`) or an open issue (`chat-and-bots`); a person who chose
"no surveys" in the preference center (`consent-and-preferences`); a person inside a return attempt with a
holdout (`lapse-and-winback`, `experiments-and-holdouts`). The ask is a touch under the cap of
`contact-orchestration`, class automated flow; it has no exemption, because the person is not waiting for it.
An ask required by a contract or a regulator sits outside the ration and does not expire
(`in-product-messaging`).

**8. The ask says what happens with the answer and by when.** "If something went wrong, [who] will contact you
within [the route's promised time]." The time comes from the route (`closing-the-loop.md`, step 4); it is not
written into the copy on its own. A route without a promised time is a defect, and a date without a timer is
not written. An incentive, where there is one, is the same for every answer, does not depend on what the answer
says, is named in the ask, and is marked as an incentive next to the answer; there is no incentive for a public
review on a third-party platform (the legal regime in `SKILL.md`). An invitation to a public review, where the
program makes one, rides on the thank-you of this ask, in the same words for every score and with no incentive;
it is not a second ask, and no rule reads the answer before showing it. The ask carries no promotion: a promotional
block changes the class of the touch (`contact-orchestration`, `transactional-messaging`) and makes the ask
direct marketing on the regimes named in `SKILL.md`.

**9. Write the answer and emit the events.** The answer goes to the person's record as a declared attribute
(`segmentation`): the score, the date, the experience type, the experience identifier, the instrument version.
The latest answer per experience type replaces the previous one in the record; every answer stays in the
reading. A transactional score describes one experience: it goes stale at the next experience of the same type
that got no answer, because it no longer describes the latest one (the neighbor says a declared attribute goes
stale in silence; this is what silence means here). A relational score lives one cycle of the program's
calendar. The events asked, delivered, answered and expired go to the contact log of `contact-orchestration`;
asks per closing state go to `program-audit-and-ops` as the heartbeat of the flow; an answer that meets an
obligation condition goes to the route of `closing-the-loop.md` as the same event.

**10. Read the instrument, not only the answers.** The response share (answers over delivered asks), the
completion share (completed over started), the time to complete, the drop-off by question, opt-outs and channel
refusals that follow the ask before any other touch, and **asks with no answers by part of the experience**: a store whose asks go
out and whose answers are zero is a broken link, a wrong template or a bad substitution, not a store with no
problems. Any change of wording, scale, order, delay, carrier or population is a new instrument version and a
new baseline; no reading crosses a version change.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Delay from the closing state to the judging point | the distribution of lags from delivery to a complaint, per product kind; no later than the end of the return or replacement window | 4, a parameter from your data |
| Ration window per experience type | the base's median interpurchase interval for the category as a starting point, never shorter than the time a loop takes to close; holds in categories with repeat purchase; replaced by your own distribution of time to the next experience of that type; never the person's own interval | 4 and 5 |
| Lifetime cap on relational asks | a parameter of the program | 4 |
| The reminder | one, to those who did not answer, when half the window has passed; the only touch after a delivered ask | 3, half of a parameter |
| Sampling fraction under a budget | the channel's budget over the cost of one ask | 4 |
| Turns before a conversation is asked about | a parameter per topic | 4 |

## Edge cases

- **Several orders in one day.** One ask, about the latest; the others count in coverage.
- **An order delivered in several parcels.** The experience is the order; its closing state is the one the
  status map of `transactional-messaging` gives the transaction, which arrives with the last parcel. One ask
  after that, about the order; a parcel carried by a different carrier is a third-party part and gets its own
  question. A parcel that is very late is the neighbor's exception row and does not wait for the ask.
- **A buyer at an organization who orders daily.** The ration is per person, not per order, and the window is
  the category's, not this person's.
- **The first day.** The flow starts with the experiences that reach their judging point after it is switched
  on; the backlog of experiences whose judging point passed before that is not asked.
- **A part delivered by a third party** (the carrier, the hotel, the marketplace). Two questions; the reading
  attributes each to its part.
- **A canceled order.** One ask for the reason, no reminder.
- **An open complaint about this experience.** No ask: the answer already exists, and the loop is open at
  `chat-and-bots`.
- **An ask required by a contract or a regulator.** Outside the ration; its form and deadline belong to the
  neighbor that owns the carrier.
- **An anonymous answer.** Reading only; a kiosk at the register is read as its own series with its own
  baseline.
- **A person who answered twice.** The first answer stands in the reading; a second answer about the same
  experience inside the window reopens the obligation where the first answer opened one, and opens one where it
  did not and the second meets an entry condition (`closing-the-loop.md`).
- **A conversation shorter than the threshold of turns.** No ask about it; the threshold is a parameter per
  topic.

## Failure modes

**The order effect.** The overall score moved when specific questions were placed before it, and nothing in
the experience changed. Sign: the move coincides with an instrument version; complaints per order through
support did not fall. Remedy: the overall question first, a new version, the baseline restarted.

**The peak of the emotion.** The score is high on the day of delivery; complaints come later through support
and public reviews. Sign: the share of low scores in the survey falls while complaints per order do not; the
lag of complaints is longer than the delay of the ask. Remedy: the judging point from the lags.

**The collection mode.** A score collected by an employee (a call, a tablet at the register with the seller
present) differs from one the person entered alone. Sign: scores differ by collection mode; a change of mode
moves the score with no change in the experience. Remedy: modes are read apart, and a change of mode is a new
baseline rather than a change in quality.

**Over-asking.** The response share falls, opt-outs that follow an ask rise, asks per person exceed one per
window. Remedy: the ration.

**A filtered population.** The people asked are those likely to be satisfied: by behavior, by the absence of
complaints, or by a store choosing whom to ask. Sign: the share of low scores in the survey falls while
complaints per order through other channels do not; asks over experiences diverge by part. Remedy: everyone
with the experience; sampling random and central.

**A silent part.** Asks go out for a store and no answers come back: a broken link, a template, a
substitution. Sign: answers over asks by part at zero with asks above zero. Remedy: read answers over asks by
part before reading any score.

**The ask that promotes.** A block with an offer was added to the ask; the class of the touch changed, the
neighbors' exemptions are lost, and the regime became marketing. Sign: a promotional block in the ask
template. Remedy: remove it, or run the ask as a marketing message with its own basis.
