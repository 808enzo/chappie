---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Vocabulary of chat and bots

The three mechanics assume these terms. Two of them, *issue* and *settle window*, share a word with something
in the tools or in a neighbor's vocabulary, and a third, *assignee*, stands where the library already
uses another word for something else. The confusion changes what gets counted. Settle them before the discussion.

## The unit

**Issue.** One matter one person raised, from their first message until it is settled, across every
thread, channel, agent and shift it crosses. It opens with a message in which the person raises a matter. An opener
nobody answered is not an issue, and neither is a capture flow in which the person only filled the
fields it asked for.

**Thread.** What the tool calls a conversation, a dialog or a ticket: a container of messages in one
channel. An issue can span several threads, and a thread can carry two issues. Metrics count issues;
threads only carry them.

**Turn.** One message from one side. One turn asks for one thing or gives one answer. It is the unit of
writing, and the rule from `email-copy` that every claim traces to a fact applies to each turn.

**Topic.** The kind of matter an issue is about, named in the person's words. The bot's scope and the
settle window are both set per topic.

**Identified issue.** An issue tied to a person's record by a key at the moment it opens. The tie is
not revised later. Anonymous issues are the rest.

## Counting

**Pass.** One cycle of answer and closure on an issue. A return starts the next pass.

**Settle window.** How long after closure a message from the same person still counts as a return, set
per topic as the time by which the person can tell whether the answer worked. Other skills in
the library use *window* for their own objects. The nearest to this one are the
engagement window of `email-program`, the response window of `deliverability`, the outcome window of
`experiments-and-holdouts`, and the reply window a messaging platform imposes (`messaging-channels`).

**Return.** A message from the same person inside the settle window. It reopens the issue unless an
agent marks it a new matter or no matter. Survey replies and automated replies are not returns.

**New matter.** A return that an agent marked as a separate issue with its own topic. It is a decision,
and it is sampled, because each one removes a return from the control metric.

**No matter.** A message after closure that raises nothing, such as a thanks. The agent marks it, and
the mark is sampled like a new-matter mark, for the same reason.

**Settled on the first pass.** Answered, closed, and no return inside the settle window. The numerator
of this skill's control metric.

**Read date.** An issue's first message, plus the longest time to closure you accept, plus its topic's
settle window. It counts from the first message because an issue that is never closed never starts a
settle window.

**Never claimed.** An issue that reached a person's queue and that no agent claimed within the longest
time to closure.

**Stuck.** An issue claimed and not closed within the longest time to closure.

## The bot

**Scope class.** What the bot does with a topic: *bot settles*, *bot collects, a person decides*, or
*person only*. Set by whether an answer can be checked when it is given and by what a wrong one costs.
For a bot that generates its answers, both questions are asked of each answer as well as of the topic.

**Negative answer.** A written statement of what cannot be done and where to go instead. It is how a
knowledge base stops a bot from filling a gap with an invented answer.

**Exit.** The visible way from the bot to a person, present at every step.

**Handoff.** The bot passing an issue to a person. Not a transfer, which happens between people. In
`b2b-lifecycle` a handoff is the program passing an account to sales, with a handoff record: the same word
for a different act, marked on both sides.

**Handoff contract.** What travels with a handoff: the person's words, the topic, the fields collected,
the answers already given, and whether the person is identified.

**Containment.** The share of conversations closed without a person. A result, not a target: it rises
when the exit is hidden.

## Who holds the issue

**Assignee.** The one agent answerable for an issue from claim to closure. This skill says *assignee*
rather than *owner*: other skills in the library already use *owner* for whoever answers for a
number, a mechanic or a broken object, and a person's matter is none of those.

**Routing key.** A fact known before anyone reads the message and used to route it: topic, page,
status, language, channel.

**Rule order.** The written order in which routing rules claim a conversation that matches several of
them. Not precedence in `contact-orchestration`, which decides which of two messages yields.

**Default group.** The group that receives what no rule took.

**Transfer.** An issue moving from one agent to another, with a summary.

**Postponed.** Waiting on somebody outside the team, with a return date on which the assignee writes to the
person.

**Closure.** The assignee ending a pass: on the person's confirmation, or when the quiet period has passed
after an answer. The event a post-conversation survey waits for.

**Quiet period.** How long after an answer the assignee waits before closing, set per topic.

## Waiting

**Promise.** What the chat tells a person about when a human will answer.

**Promise state.** The condition a promise is written for: in hours at normal load, in hours at heavy
load, off hours, a holiday, an incident.

**Breach message.** The message sent when the promised time passes without a reply, with a new time.

**Off-hours mode.** The bot settling its own topics and stating the next working time for everything
else.

**Backlog.** The issues waiting when the team comes online, cleared in a written order.

**Stale question.** An issue written off hours that the person no longer needs answered by the time
somebody reads it.

**Anonymous issue.** An issue not tied to a record by a key when it opened. Nothing that has to reach
the person later can be promised until an address is taken for it.

## Words shared with neighbors

- **Touch** (`contact-orchestration`): one delivered message to one person in one channel. A reply
  inside an issue is what the person is waiting for as a consequence of their own action, so it falls
  under that skill's exemption from the cap. A proactive opener to a person you know, a follow-up that
  pushes a sales decision, and a reply that carries promotion are touches.
- **Capture point** and **handover state** (`onsite-capture`): a bot the program opens to take a contact
  is a capture point; an address taken to deliver an answer holds the state *requested message*.
- **Key**, **hint** and **link** (`list-building`): an issue is identified only through a key. A hint,
  such as a device, and a link, which marks two records as probably one person, identify nothing here.
- **Object** and **heartbeat** (`program-audit-and-ops`): the bot and the handoff route are objects in
  that skill's sense, and a handoff that reaches a person is the handoff route's heartbeat.
- **CSAT** (`metric-definitions`): the formula lives there. Here it is an input, sent on closure, and it
  does not reach the people who left.
- **Incident** (`program-audit-and-ops`): an outage behind a wave of issues. This skill answers the
  wave; the incident belongs to the neighbor.
- **Window** in `promo-calendar`: a dated span with an offer in it. It brings its own arrival curve,
  which is why this skill writes the promise for it in advance. A wave that no offer causes, such as
  the last days to order before a holiday, is read from your own arrival history.
- **Resolution** in `personalization` is the moment a value is resolved. This skill says *settled* for a
  person's matter, so the two words do not meet.
