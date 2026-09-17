---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Vocabulary of feedback

The three mechanics assume these terms. Four of them are units. When two people disagree about a survey, check
first whether one of them means the ask and the other the answer, or whether one means the score and the other
the obligation the score created. Several words are shared with neighbors, and those are marked at the end.

## The units

**Ask.** One request to one person about one experience: an order, a visit, a conversation, a refund, a
cancellation, the end of a service, silence after an expected purchase. A touch under the cap. It carries the
key, the instrument version and the promised time of the route. The unit of construction.

**Answer.** What came back: a score, a choice, a text, a public review. It is tied to an ask by a key; or it
arrived on its own and was identified through the experience; or it is anonymous, in which case it goes to the
reading only.

**Obligation.** An answer that requires an action toward the person: a score below the threshold of its scale,
a text naming a problem at any score, a request to be contacted, an identified negative public review, a
complaint that answers an experience. One per answer; a reopen is the same obligation. The unit of the inner
loop and of the control metric.

**Part of the experience.** What an answer is attributed to when read: the store, the courier, the picker, the
supplier batch, the shift, the product, the flow and its message version, the screen, the assignee of a
conversation. The unit of the reading.

## The ask

**Experience type.** The kind of matter an ask is about, with its own closing state, judging point, questions
and ration.

**Closing state.** The state of the experience, as the person sees it, after which they can judge it: delivery
confirmed, order picked up, issue closed, refund landed, trip ended, order canceled. Taken from the status map
of `transactional-messaging`, not from an internal status.

**Judging point.** The closing state plus the time a defect takes to show, and no later than the end of the
return or replacement window. The moment the ask goes out.

**Population.** Everyone who had the experience. A sample is random and its fraction is recorded.

**Respondent.** A person whose answer arrived. **Response share:** answers over delivered asks. **Coverage:**
answers over the period's experiences, including people with no reachable channel. **Completion share:**
answers completed over answers started.

**Ration.** The limit on asks to one person per experience type per window, sitting inside the shared cap of
`contact-orchestration`; the window is the experience type's, set from the base, not the person's own interval.
A relational ask carries a lifetime cap on top.

**Relational ask.** An ask about the relationship rather than one experience, on the program's calendar.
**Transactional ask.** An ask about one experience, at its judging point.

**Branch.** The questions that follow the overall score, chosen by the score: what went wrong, what to improve,
what stood out.

**Instrument version.** The wording, scale, order, delay, carrier, population and obligation threshold of an ask.
A change of any of them is a new version and a new baseline.

**Collection mode.** Self-completed, or administered by an employee (a call, a tablet with the seller present).
Modes are read apart.

**Key.** The identifier of the person and of the experience, carried inside the ask so that the answer arrives
identified without sign-in or contact fields.

## The loop

**Route.** For an experience type: the table of theme to owner, the written promised time, the table of theme to
remedy, and the number of attempts before unreachable.

**Promised time.** The route's deadline, named to the person in the ask and in the thank-you, with a timer that
starts at the timestamp of the answer. A promise made in a reply starts a new timer.

**Substantive reply.** A reply that names the experience, states the problem in the person's words, asks for a
missing fact if one is missing, and says what happens next with a promised time. An automatic acknowledgement is
not one.

**Closed.** One of three: the person confirmed; the quiet period of the topic passed after the last substantive
reply with no return; the promised fix arrived as an event. **Closed on time:** closed with every promised time
on the obligation met by its own event, the route's and each one made in a reply.

**Outcome.** Fixed, explained, compensated, already remedied, out of scope, unreachable. Unreachable is not
closed, but it ends the obligation: it leaves the queue and the suppression on asks, and reopens on the next
signal. Declined contact is not an outcome of an obligation, because no obligation opened.

**Cause code.** The theme written at closure. A closure without one is not a closure.

**Reopen.** A second signal from the same person about the same experience inside the reopen window: a second
low score, a public review after a closure, a complaint, a chargeback. It reopens the same obligation.

**Inner loop.** From the answer to the closure of its obligation. **Outer loop.** From the reading to a change
and to the message back to the people who named the theme.

**Unidentified negative review.** A public negative review not tied to a person and an experience. A count
read beside the control metric; it enters the denominator on identification.

## The reading

**Theme.** A class of problem named in the person's words. **Theme list:** versioned; one list by identifier,
wording per language.

**Exposure.** A part's share of the period's experiences.

**Excess.** The rate of a theme on a part (answers carrying the theme on experiences with the part, per
experience with the part) above the rate on the other parts of the same kind and above the part's own earlier
periods; the same thing as the part's share of the theme's answers above its exposure.

**Readable floor.** The minimum number of answers in a cell (one part in one period) below which the cell is
not read; periods get pooled, parts do not.

**Priority.** The share of answers mentioning a theme, times the gap between their mean score and the mean score
of the rest.

**Decision record.** For a theme taken up: the theme and the part, the excess, the owner, the deadline, the
change and its date, the verification metric, and who gets told.

**Self baseline.** A part's own history of scores and excesses, reset only on an instrument change.

## Words shared with neighbors

- **NPS, CSAT, respondent as the denominator** (`metric-definitions`): the formula and the bands live there;
  here they are read.
- **Touch, class, exemption, cap** (`contact-orchestration`): the ask is a touch of class automated flow with no
  exemption; the reply to an obligation is exempt, because the person is waiting for it.
- **Issue, closure event, quiet period, settle window, topic** (`chat-and-bots`): the survey after a conversation
  waits for the closure; the quiet period before a closure here is the topic's; the reopen window of an
  obligation about a conversation is the topic's settle window; a low score after a conversation is not a
  return there, by the neighbor's rule, but an input read beside its metric, and it is an obligation here.
- **Declared attribute, fill rate, readable floor** (`segmentation`): an answer becomes a declared attribute; the
  neighbor's readable floor is the size of a segment, this skill's is the size of a cell of answers, the same
  idea on a different unit.
- **State, status map, service row, promised time** (`transactional-messaging`): the closing state comes from the
  status map; the ask is not a service row; a promised time is the same word with the same timer.
- **Display rule, capture point** (`onsite-capture`): a survey on the site shows under the display rule; the
  question is this skill's.
- **Carrier, window, participant** (`in-product-messaging`): the survey's carrier in the app is the neighbor's;
  the participant is the person who submitted.
- **Counterweight, vanity metric** (`crm-reporting`): a score without its response share is on the neighbor's
  register; the counterweights of the control metric here are read on the same page.
- **Hypothesis** (`experiments-and-holdouts`): a hypothesis from the reading goes there as a card; nothing is
  proven here.
- **Object, heartbeat, missed obligation** (`program-audit-and-ops`): the ask flow is an object with asks per
  closing state as its heartbeat; the neighbor says missed obligation for a required row that did not go out,
  and this skill says obligation for what one answer owes one person; an obligation open past its promised time
  is what the neighbor's duty reads.
- **Preference** (`consent-and-preferences`): an answer about what to receive and how often is a preference and
  lives in the preference center, not in the record of answers.
