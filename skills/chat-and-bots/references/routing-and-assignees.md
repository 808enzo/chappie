---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-12
---

# Routing and the assignee: how an issue reaches someone who can settle it, and stays theirs

The unit here is **the issue and its assignee**. A thread can be closed, split or moved between channels;
the issue stays one matter with one assignee until it is settled.

`bot-first-line.md` covers which topics the bot keeps and when it hands over, and
`waiting-and-off-hours.md` covers what the person is told about the wait. Matching a person to their
records belongs to `list-building`.

## Entry conditions

Conversations arrive through more than one channel, or more than one person answers them. With one
agent on one channel, steps 1 to 6 reduce to a single rule: the agent is the assignee of every issue. Closure and
returns (steps 8 and 9) still apply.

## Exit conditions

Routing rules are written in order and end with a default group. Every open issue has one assignee,
visible to the team. Transfers carry a summary. Closure has a written rule per topic, and a return
reopens the issue it belongs to. The team is staffed to the hourly arrivals it measured.

## Steps

**1. Receive every channel into one queue, tied to the person's record.** Site chat, app chat, messaging apps
and support email land where the assignee sees the person's history, whichever channel the issue started
in. An agent who asks a person to repeat what they wrote in another channel is doing work the queue
should have done. Matching threads to a person is `list-building`'s; the requirement that the assignee
sees the history is here.

**2. Write the routing keys: what is known before anyone reads the message.** The topic the person
picked in the bot; the page or product they wrote from; their status (a customer, an open order, an
active contract); the language; the channel. Route to a group, not to a named agent, except where a
relationship already exists: an account manager, or a sales conversation already under way.

**3. Write the order of the rules, and end it with a default group.** A conversation that matches
several rules goes to the first rule in the written order. The last rule catches everything no other
rule took, and somebody reads that group. Without a written order, the result depends on how the tool
evaluates rules, which nobody on the team decided.

**4. Claim before replying.** An agent claims an issue before typing. Unclaimed issues are visible to
the whole group; claimed ones leave the shared view. Two agents answering one person, each unaware of
the other, is the failure this step prevents.

**5. One assignee until closure; transfer only with a summary.** The agent who claimed the issue keeps it.
When a specialist is needed, the assignee consults them inside the issue, in notes the person does not
see, and gives the answer. When the issue has to move, the transfer carries a written summary: what
the person asked, what has been done, what they were told, what comes next. Tell the person who has
the issue now and when they will hear back.

**6. Shift boundaries do not change the assignee by default.** Choose one of three arrangements and write
it down. Shifts are long enough for an assignee to settle the topics they take. Or, near the end of a
shift, an agent takes only issues they can settle before leaving. Or an issue that crosses the boundary
is transferred with the step 5 summary to a named assignee on the next shift, and the person is told. An
issue that belongs to nobody between shifts is the failure. When an assignee is away for longer than the
person was promised, a service issue is reassigned with a summary. Do not reassign a sales
conversation: tell the person their message was received and when the assignee will answer.

**7. Postpone with a return date.** An issue waiting on somebody outside the team (engineering,
finance, a carrier) is neither left open nor closed. Postpone it, with a date on which the
assignee writes to the person, and tell the person what they are waiting for and by when. On that date the assignee
writes even if there is no news, and sets the next date. If the person may not be in the thread on
that day, promise the date only once you have a way to reach them: a record tied by a key, or an address
taken for it (`waiting-and-off-hours.md`, thresholds). Without one, give the date as the time to come
back to this thread, and say so.

**8. Close by the written rule for the topic.** The assignee closes when the person confirms the matter
is settled, or when the quiet period for the topic has passed after an answer. Set the quiet period
per topic from your own process, the same way as the settle window in `SKILL.md`: how long until the
person can act on the answer. An issue closed before an answer went out is not closed; reopen it. The
survey that follows a conversation waits for this closure event (`voice-of-customer`).

**9. A return reopens the issue it belongs to.** A new message from the same person inside the settle
window reopens the earlier issue, with the same assignee if they are working, rather than opening a new
one. The assignee may mark it a new matter, with its own topic, when it is one. Sample the marked ones on
the reading rhythm, because every mark removes a return from the control metric.

**10. Split into lines only when a line can settle a topic on its own.** A first line that can name
the topics it settles by itself, with a second line for the topics that need deeper skill, saves the
specialists' time. A first line that cannot name one topic it settles by itself is a relay: every issue
waits twice and is explained twice. In that case run a flat team, where every agent settles every topic
and consults inside the issue (step 5).

**11. Staff to arrivals by hour, not to the daily average.** From your own history, count the issues
opened by hour of day and day of week, and staff each hour to its own arrivals and to how long its
topics take. Promotion windows (`promo-calendar`) and incidents bring their own arrival curves, so plan
them separately. Name who covers breaks, so that an hour does not lose capacity at lunch without
anyone deciding it.

## Stalled sales conversations

A conversation in which a person was deciding to buy, and stopped replying, has its own rule, because
follow-ups here are touches rather than service. Before the first follow-up, write down how many
follow-ups the conversation gets and at what spacing. Each follow-up asks for a decision (yes, no, or a
date to talk again), not for attention. Stop at the number you wrote, and close with a stated way back.
These follow-ups count against the cap in `contact-orchestration`, and a follow-up that carries an
offer needs a basis for marketing (`consent-and-preferences`). A follow-up that asks a service question
the issue needs, such as whether a fix worked, is part of the issue and not a touch.

## Thresholds and timings

- **Write the rule order and the default group** before routing goes live, and check every change to
  a rule against the rules above it.
- **Record every transfer on the issue.** As a starting point, read every issue with a second
  transfer; when the volume makes that impossible, sample, and say that you sampled.
- **Set the quiet period and the settle window** per topic from your own process.
- **A postponed issue always carries a return date.** Without one, nobody is due to write to the person,
  and the issue drifts toward the class *stuck*.
- **Staff to the hourly arrivals** measured from your own history, and recompute when the topic mix
  or the hours change.

## Edge cases

- **The person switches channel in the middle of an issue.** It is still one issue. When the new
  channel is not tied to the person's record, as with an anonymous chat after an email, the assignee ties
  it by asking once for what identifies the earlier issue.
- **Two matters in one thread.** Split them into two issues with their own topics, possibly with two
  assignees, and tell the person each one will be answered.
- **Abuse.** The assignee may end the conversation, saying why and how to come back to the matter. The
  issue closes with the reason recorded.
- **An account with a named manager.** The relationship key routes sales and account matters to the
  manager. A service matter still goes to the service group, with the manager added in notes, so that
  the service promise does not depend on one person's calendar.
- **An assignee leaves the company or falls ill.** A lead reassigns every open and postponed issue with a
  summary on the same day, and each person is told who has their matter now.
- **An incident wave.** Route the incident topic to one assignee and one status answer
  (`bot-first-line.md`, edge cases). A separate assignee for every issue of one incident means a separate
  answer from each. The issues stay open, postponed with the status rhythm as their return dates, and
  close on the notice that the fault is fixed. A status message does not answer the matter: close the
  issues on it, and every "is it fixed yet?" reads as a return, sending you to edit a bot that answered
  correctly.
- **A contractual response time for a business customer.** The contract's promise replaces the chat's
  promise for that account, and the routing key for status carries it (`waiting-and-off-hours.md`, edge
  cases).

## Failure mode

**The signal (ping-pong):** transfers per issue rise, people repeat themselves, and the time to settle
an issue grows while first response time looks fine. The causes: overlapping rules without a written
order, routing by channel where the topic should decide, or shift boundaries that move issues by
default.

**The second signal, which behaves the opposite way (hoarding):** transfers are close to zero, assignees
hold issues they cannot settle, postponed issues pass their return dates, and the first-pass share holds
up on easy topics while the hard ones age. The causes: transfers are discouraged or counted against the
agent, or the specialist behind a topic cannot be reached from inside the issue.

**The question that separates them:** is the issue moving between people, or sitting with one? Read the
transfer count and the age of postponed issues together.

**What to do:** for ping-pong, write down the rule order and read every issue with a second transfer
from the last period, to find the rule that sent it the wrong way. For hoarding, list the postponed
issues past their return date by assignee and by topic, and give each topic a named specialist the assignee
can consult in notes.

A third pattern belongs to neither: **closures rise, and returns rise with them.** The closure rule of
step 8 is being ignored, and the control metric already shows it in the class *returned*.
