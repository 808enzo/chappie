---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-12
---

# The bot on the first line: what it answers, and when it hands over

The unit here is **a topic of issues**: the kind of matter people write in about, and the decision
about what the bot does with it. Writing the individual turns follows from that decision rather than
preceding it.

The display rule for a proactive opener on a page belongs to `onsite-capture`, and what a messaging
app lets a bot do belongs to `messaging-channels`. A bot or a handoff route that stopped working is
an incident for `program-audit-and-ops`.

## Entry conditions

People already write in, or will, and somebody can read a sample of real conversations, or tagged
issues, from the channel the bot will sit on. A bot written from the FAQ page answers the questions
the company thinks people have.

For a new channel with no history, take the first topic list from the conversations of the nearest
channel people already use (email to support, notes from phone calls), and start the bot on the
narrowest scope.

## Exit conditions

Every topic on the list carries one of three scope classes, written down with its reason. The bot is
live, says it is a bot, shows the exit to a human at every step, and hands over with the contract in
step 7. A named person reads its conversations on the rhythm of step 10.

## Steps

**1. Build the topic list from real issues.** Take a sample of recent conversations and tag each by
the matter the person raised, in their words: "where is my order", not "logistics". Tag the matter,
not the product area and not the outcome. A topic you cannot name in the person's words does not go
on the list yet. Keep tagging after launch: the list is where step 10 feeds back.

**2. Put every topic in a scope class by two questions.** First: can the answer be checked against
data or a written policy at the moment it is given, as with an order status or the delivery terms?
Second: what does a wrong answer cost, and can it be taken back? A wrong delivery date is corrected by
the next message. A wrong statement about a refund, a price or what the person is entitled to is a
statement by the company, and the person may act on it before anyone corrects it (the legal regime in
`SKILL.md`).

| Scope class | Condition | What the bot does |
|---|---|---|
| **Bot settles** | the answer can be checked, and a wrong one is cheap and reversible | answers and closes, with the exit still visible |
| **Bot collects, a person decides** | a person has to judge, but the inputs can be collected: an order number, a photo, what the person already tried | asks for the inputs, one per turn, then hands over |
| **Person only** | a claim, a dispute about money, a cancellation, a complaint, or any answer that is a decision about this person: an exception, an entitlement, a refund | hands over at once, collecting nothing beyond what routing needs |

A topic that fails either question of the first class goes down, not up. Admitting a topic to *bot
settles* because it is frequent reverses the rule: frequency tells you where the bot saves the most
time, not where it is safe.

For a bot that generates its answers, ask both questions of each answer as well as of the topic. You
can check a generated answer when it quotes one named passage of the source, or one data field, and
shows it to the person; when the bot rephrases in its own words, nobody checked the answer at the
moment it went out. Admit a topic to *bot settles* for such a bot only when its answers quote the
source. Whatever the topic, when a generated answer would state a price, an entitlement, an exception
or a refund beyond the quoted passage, the bot hands over instead of sending it: a question about
delivery can produce a promise about a refund, and the topic's class does not stop it.

**3. Answer from the source the agents use, and write the negative answers.** The bot's answers and
the agents' saved replies come from one knowledge base or one policy text, so a change reaches both.
For every topic, write what cannot be done and where the person should go instead: "you cannot pay
from the blog page; payment is on the pricing page". A bot that generates answers from a knowledge
base fills a gap with a plausible answer, and what closes the gap is the written no.

**4. Say it is a bot before the person types.** In the name shown on the chat and in the first turn.
A name that could belong to a person, or an avatar with a face, makes people wait for a human and then
feel misled. When a person asks whether they are talking to a human, the bot answers truthfully.

**5. Ask for one thing per turn, and accept typed text at every step.** Buttons offer the choices;
typed text is read at every step too, because some people ignore buttons and type. When the bot does
not recognize a reply, it answers once with the choices and the exit. When it does not recognize the
next reply either, it offers the handoff rather than a third menu. Take the second unrecognized reply
in a row as the trigger to start with, for bots built on menus; revise it by reading where people
leave after an unrecognized reply (step 10), and move the trigger earlier if they leave after the
first.

**6. Keep the exit to a human visible at every step, including the first.** Honor a request for a human
without asking the person to justify it. Before handing over, the bot may ask the one question
routing needs (the topic, if the person has not said it) and nothing else. A bot that answers a
request for a human with "let me try to help first", or sends the person to another widget or a phone
number, has hidden the exit.

**7. Hand over with a contract.** The person who takes the issue receives, inside the issue: the
person's own words, the topic, every field the bot collected, every answer the bot already gave, and
whether the person is identified. The agent's first turn shows the contract was read: it does not ask
again for anything the contract holds. Outside working hours, the handoff goes through
`waiting-and-off-hours.md`, step 5.

**8. Record each branch as an event and each answer as a field, at the moment it is given.** Not at
the end of the flow. A person who leaves halfway leaves what they already said, and you can see where
the flow loses people. For an anonymous person, the fields stay on the thread until the person is
identified; matching them to a record is `list-building`'s.

**9. Launch on one topic, and widen topic by topic.** Before launch, walk every branch as a person
would, including typed text, the unrecognized reply and the exit. For a bot that generates answers,
start with the topic the knowledge base covers best, read every conversation of that topic, fix the
knowledge base, and only then add the next topic.

**10. Read the bot's conversations on a rhythm.** Three piles: a random sample of the issues the bot
settled on the first pass, checked against policy (the "policy match" number in `SKILL.md`); every
conversation where a person asked for a human; every low rating. Each finding becomes one of three
edits: a knowledge base change, a new negative answer, or a topic moved down a scope class. Reread a
topic whenever the policy it cites changes, before the change goes live.

## Thresholds and timings

- **Set scope per topic, not as a share of volume.** "The bot handles a given share of
  conversations" is a result, and as a target it pays for hiding the exit.
- **Admission to *bot settles* needs both conditions of step 2.** One wrong answer on a topic where the
  answer binds the company is enough to move the topic down. On a cheap, reversible topic, move it on a
  pattern rather than on one case.
- **The handoff trigger for unrecognized replies** is the second in a row, as a starting point, with
  its scope and the way to revise it stated in step 5.
- **A proactive opener does not open an issue.** Only a message in which the person raises a matter
  does, which keeps unanswered openers and filled-in capture flows out of the control metric.
- **The knowledge base changes before the policy does.** The rereading in step 10 happens before a
  price, a term or a policy goes live, not after the first wrong answer.

## Edge cases

- **Two matters in one message.** The bot takes the one its scope class lets it settle, says that
  the other goes to a person, and the issue splits into two issues with their own topics.
- **An account question from somebody not identified.** The bot asks for the least that lets it check,
  such as an order number and the address the order used. It gives no account detail to a person it has
  not matched.
- **Anger or distress in the first message.** Hand over, whatever the topic. A bot that answers an
  angry person with a menu turns a service problem into a complaint.
- **An outage brings a wave of the same question.** The bot answers that topic with one status message,
  updated as the incident moves, and hands over only the people whose situation differs from the
  status. The issues stay open until the fix (`routing-and-assignees.md`, edge cases). The incident
  itself is `program-audit-and-ops`'s.
- **The bot runs in a messaging app without buttons.** The flow falls back to numbered choices in plain
  text. `messaging-channels` covers what the platform allows; this skill checks that the flow still works without
  buttons, in step 9.
- **An automated outbound message the person can reply to.** The person replies and waits. Every
  automated message a person can answer says, in the message itself, whether replies are read and how
  to reach a person.
- **A question outside every topic.** The bot says it cannot answer that and offers the handoff. It
  does not guess, and the question goes into the tagging of step 1.

## Failure mode

**The signal (the trap):** the share of issues closed without a person keeps rising, requests for a
human fall, and complaints and repeat contacts arrive by phone, by email and in public reviews. Reading
shows people leaving right after a bot answer, or after the second menu. The causes are three: the exit is hidden, the handoff triggers are too narrow, or the knowledge base has a gap the bot fills with
an invented answer. **The bot's own reports cannot see this,** because a person who gives up after an
answer leaves the same events in the bot as a person who was helped. Only returns through other
channels catch it, and only those logged on the person's record, together with the reading in step 10.

**The second signal, which behaves the opposite way (over-handoff):** handoffs rise, and people reach
agents with matters the bot had everything to settle; agents ask again for what the bot collected. The
causes: triggers that fire on any keyword, a contract that does not carry the fields, or people who
stopped trusting the bot after it failed them early.

**The question that separates them:** did the person reach a human? In the trap they did not, and they
left. In over-handoff they did, with a simple matter. Repeat contacts by phone or email are also the
sign of a promise padded too long (`waiting-and-off-hours.md`, failure mode). Read where the person
stopped: right after a bot answer is this trap; at the promise, before any human, is that one.

**What to do:** for the trap, restore the exit at every step, then read every request for a human from
the last period and move the topics those requests cluster on down a scope class. For over-handoff,
check the contract first (does the agent see the fields?), then narrow the triggers to the reasons in
steps 5 and 6, and read the conversations of the topics with the most handoffs.
