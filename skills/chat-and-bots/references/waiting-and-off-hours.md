---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-12
---

# Waiting and off hours: what the person is promised, and how the promise is kept

The unit here is **the promise**: what the chat tells a person about when a human will answer, in each
state the chat can be in. Write the promise from the wait you deliver, show it before the
person types, and change it before it breaks.

`routing-and-assignees.md` covers who answers and in what order, and `bot-first-line.md` covers
what the bot answers while nobody is online. Quiet hours for messages the program sends are `contact-orchestration`'s;
this file is about answering people who wrote in.

## Entry conditions

Some hours have no person answering, or the wait changes during the day. A team staffed around the
clock, with the same wait at every hour, needs only steps 4 and 7 and the edge cases.

## Exit conditions

A promise is written for every state the chat can be in; the chat shows the current one; a broken
promise produces a message rather than silence; off-hours mode is configured; the order of the morning
backlog is written down.

## Steps

**1. Measure the wait you deliver, by hour of the week.** For each hour, take every issue routed to a
person and measure the time from the person's first message to the first reply typed by a person. An
automated greeting is not a reply. A person who left before any reply counts too. Where the thread
stays in the queue after they leave, measure their wait to the first reply typed into it. Where the
tool drops it, their wait is unknown and no reply reached them: count them as waiting longer than
every promise you consider. That overstates the wait of people who left right away, and the error falls
on the safe side of a promise. Entering the time they stayed as their wait errs the same way as
leaving them out: the hours in which people leave look faster than they were.

**2. Write the promise from that distribution, per state.** The states: in hours at normal load, in
hours at heavy load, off hours, a holiday, an incident. For each state in working hours, take a late
point of the wait distribution for those hours, not the median: at the median, half the people wait
longer than they were told. How late a point is your decision, and it is a decision about how many
people you accept disappointing, so write that share down beside the promise. State the promise as a
time or a range, and in the person's local time when it names a time of day.

**3. Show the promise before the person types, and change it before it breaks.** The chat entry shows
the current promise. When the queue grows past what the promise can hold, switch to the heavy-load state
before the people waiting under the old promise run out of time, not after. When the bot hands over, it
repeats the promise.

**4. When the promised time passes, say so.** At the moment the promise runs out without a reply, the
person gets a message saying the reply is late, with a new time. Have a person type it if anyone is
free for one line; otherwise send it automatically. Silence after a broken promise tells the person the chat was never
staffed.

**5. Off-hours mode: the bot settles what it may, and says when a person will answer.** The bot answers
the topics in its *bot settles* class (`bot-first-line.md`). For everything else, it says when a person
will read the message: the next working time, in the person's local time, not "soon". It asks for a way
to reach the person only if the answer will have to find them after they leave, and it says what the
address will be used for. A person signed in to an app, who will see the reply in the same thread, is
not asked for anything.

**6. Clear the morning backlog in a written order.** First the issues whose consequence falls today: a
delivery due, a payment deadline, an appointment. Then the oldest first. Before replying to an issue
written off hours, check whether it is still live: the person may have solved it, ordered, written again
somewhere else, or canceled. A reply to a question asked hours ago acknowledges the wait first, then
answers.

**7. A reply to a person who left goes where they will see it, and carries nothing else.** The same
thread, if they will come back to it; otherwise the address they gave for this answer. The message
answers their request and carries no promotion. The address taken for it holds the handover state
*requested message* from `onsite-capture`: it permits this answer, and using it once does not make it a
marketing address.

**8. Write the promise for a dated wave before it starts.** Take last cycle's arrival curve for it, set
the staffing and the promise from it, and name any temporary staff before it opens. Promotion windows
belong to `promo-calendar`; a wave that no offer causes, such as the last days to order before a
holiday, comes from your own arrival history.

**9. In an incident, switch the state and answer the incident once.** A spike caused by an outage
switches the chat to its incident state: a status line at the chat entry and in the bot, updated on a
written rhythm, and individual issues taken only from people whose situation differs from the status.
The incident itself is `program-audit-and-ops`'s.

## Thresholds and timings

- **The promise comes from your own wait distribution** for each state, at a late point you chose and
  wrote down together with the share of people it disappoints.
- **The breach message goes out at the promised time**, not with the next reply.
- **An off-hours promise names a time of day** in the person's local time.
- **Give a promise that has to reach the person after they leave** (we will write, a manager will call)
  only once you have a way to reach them: a record tied by a key, or an address taken for it. This
  holds in every state, not only off hours.
- **Recompute the distribution** whenever the hours, the staffing or the topic mix change, and the
  promise with it.

## Edge cases

- **The team and the person are in different time zones.** "Tomorrow morning" in the team's time can be
  the middle of the night for the person. Name the time in theirs.
- **A thin night shift.** Night is its own state, with its own promise and its own measurement. Averaged
  into the day, it promises the night a wait the night cannot keep.
- **Written off hours, back during hours through another channel.** It is the same issue: the second
  message is attached to the first and answered once (`routing-and-assignees.md`, step 9).
- **An anonymous person off hours who leaves no address.** Nothing that has to reach them later can be
  promised. Say when a person will be online, and whether the thread will still be there if they come
  back on the same device. Do not promise a callback.
- **An address already on the thread from a capture flow.** It was given for that flow's message, and
  its state permits that message and nothing else (`onsite-capture`). Ask whether the answer may go
  there; a yes gives the address a second *requested message*, for this answer.
- **A business customer with a contractual response time.** The contract's promise replaces the chat's
  promise for that account, and routing sends their issues on the contract's clock
  (`routing-and-assignees.md`, edge cases).
- **A weekend backlog larger than Monday morning can clear.** The Sunday promise names the time Monday's
  backlog will reach a new message, computed from previous Mondays, not "on Monday".

## Failure mode

**The signal:** people say nobody answered, while first response time looks healthy. Three causes stack: an automated greeting counts as a reply, people who left before any reply are
missing from the number, or the promise was copied from a target instead of from the distribution.
The first response number cannot show how many people left before any answer, because it is
computed on the replies that were sent.

**The second signal, which behaves the opposite way:** promises are padded so long that people do not
wait at all. The promise-kept share looks excellent, and the same person's issue arrives again soon after
by phone or by email.

**The question that separates them:** did people wait and get let down, or not wait at all? Read how
long people stayed before leaving against the promise they were shown. Repeat contacts through other
channels also follow the bot trap (`bot-first-line.md`, failure mode): there people leave right after a
bot answer, here at the promise.

**What to do:** for the first, rebuild step 1 with the greeting removed and the people who left counted
in, and rewrite the promise from that. For the second, shorten the promise to the late point you
deliver, and watch repeat contacts through other channels over the next cycle.
