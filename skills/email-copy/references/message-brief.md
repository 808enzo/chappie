---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# The message brief: what this email is for, before the words

The unit here is **the job of one message**: the state a reader is in when it arrives and the state
it leaves them in. Everything in this file happens before the first sentence is written, and almost
every defect that survives to the send was decided here.

This file does not write the message. The words are `body-and-action.md`, the subject line is
`inbox-line.md`, and the decision to release the send is `pre-send-review.md`.

## Entry conditions

A slot exists and it belongs to a neighbor: a place in the standing program (`email-program`), an
event (`triggered-messages`), a step in a series (`welcome-and-activation`, `lapse-and-winback`,
`repeat-purchase`). The audience is chosen elsewhere. Somebody is about to write words.

## Exit conditions

A written brief another person could write the message from: the job in one sentence, the inherited
promise, the facts with sources, one action with the event that records it, what the message may
not say, the roles of its links, and the acceptance test in a single line.

## Steps

**1. Name the job in one sentence, with the reader as the subject.** "This message takes a person
who did X to doing Y, because Z." A sentence with the company as the subject, such as announcing a
collection or promoting a webinar, is not a job: it names neither the state the reader leaves nor
the state they arrive in. One test settles it and it is quick. **Substitute somebody else's product
into your sentence.** If the sentence still makes sense, you have not named a job.

**2. Write down what arrives with the reader.** A message almost never starts the conversation, and
it inherits three things it knows nothing about:

- **the wording of the capture point**, meaning what the person was offered and in which words
  (`onsite-capture`, `welcome-and-activation`). A promise reads as kept when the person recognizes
  the words they saw, not a restatement of them;
- **the event the person performed**, and when (`triggered-messages`);
- **the live offer and the order in which benefits apply**, which decides what can be promised and
  in what combination (`offer-design`).

Write these down before the text exists. Text breaks all three silently.

**3. Collect the facts before the words.** A fact is something you can point at: a specification, a
date, a deadline, a condition, a policy, a count, a quote from somebody you can name. An
evaluation is not a fact.

Break the job into the claims the message will have to make and put a fact under each one. Where
the facts are missing, they come from the places that already hold them: sales and support, meaning
what people ask and what they object to; the reasons people give when they unsubscribe; the
analytics of abandoned steps; and the product's own terms. This is not a source of inspiration, it
is a source of checkable claims.

**The threshold: a claim with no fact under it is not rewritten better, it is dropped.** A
paragraph with no fact underneath becomes a question to whoever owns the product, and it does not
return to the message until there is an answer.

**4. Name one action and the event that records it.** What the person does, where they do it, and
which system writes it down. An action with no record is not measurable: either name an observable
substitute, such as arrival on the page where the action happens, or write in the brief that this
message's job is not measured. A message in the second class does not take part in comparisons with
the rest.

**5. Write down what the message may not say.** Three classes: a claim with no fact, urgency that
is not real, and a benefit the offer does not carry. Keep it short and specific to this message
rather than general.

**6. Assign the link roles now.** Four roles: **work**, meaning links that lead to the named
action; **support**, meaning what helps somebody decide, such as terms, details or reviews;
**navigation**, meaning sections, catalog and the header; and **required**, meaning unsubscribe,
contacts, legal pages and the web version link, whose click says the message did not show rather
than that an argument was weighed (`email-design` reads that share). Assign them before the template
is built and carry them into whatever your platform uses to distinguish links in reporting. The control metric in `SKILL.md` stands on
this: it reads the first three and leaves required links outside the number, which is why required
is a role of its own and not a kind of navigation. Reconstructing roles afterwards is guesswork,
because a report shows the address: two links to the same catalog page can be the work of the
message in one place and the header menu in another.

**7. Write the acceptance test in one line.** Most of the time it reads: somebody who read only the
subject line and the first block can say what is being offered and what to do. Messages that ask
for nothing right now need a different test, and it is written here rather than assumed.

## Thresholds and timings

- **The brief comes before the text, always.** The reverse order, where the job is extracted from a
  finished draft, produces messages carrying two jobs with neither of them named. No later step
  catches it: the subject line, the body and the review all work on a draft that already exists.
- **A campaign brief is reread on the day of the send.** The inheritance goes stale faster than the
  text: an offer changes, an item sells out, a condition moves. Reread step 2 and leave the rest
  alone.
- **A triggered brief is written once** and revised when the trigger's definition changes, which
  `triggered-messages` owns, or when the inherited promise changes. It has no calendar: a message
  nobody touched does not rot on its own, the world around it does.
- **Two jobs are separated before the text.** The rule for separating them: keep the job the
  audience's state can carry. Do not sell an add-on to somebody who has not bought once, and do not
  sell at all in the message that still owes somebody the guide they came for.

## Edge cases

- **There are no facts at all.** The answer is not to write better, it is not to send. An empty slot
  is a question for `email-program`, not for copy. The intermediate answer is to shrink the message
  to the one fact you do have and give it the whole slot.
- **The job is "nothing yet".** A step in a series that warms rather than asks. An action is still
  named, such as read to the end, reply, or save, and its observability is worse. That goes in the
  brief rather than being discovered later in a report.
- **A step in a series whose argument was already made.** Do not repeat the argument, refer to it. A
  repeat reads as "they sent me the same thing again" and spends the trust the series is
  accumulating.
- **The capture point's promise has not been delivered yet.** Until it is, the message asks for
  nothing else. A program has no standing to ask while it still owes.
- **A message with no inheritance at all**, such as the first campaign to a base collected long ago.
  The silence is itself the inheritance, and it is named out loud in the text rather than stepped
  over.

## Failure mode

**The signal:** briefs get written and the job in all of them is the same, such as driving traffic
or telling people about new arrivals. Detect it by comparison: take the briefs from your last program
cycle and swap their job sentences around. If nothing breaks, there is no brief practice, only its
imitation.

**The second signal, which behaves the opposite way:** briefs are varied and detailed, and messages
still go out carrying two jobs. The cause is different. The brief is being written after the draft,
as a description of it. Check the dates: a brief created later than the draft never set the job.

**What to do:** in the first case, rewrite the job sentence around a change in the reader's state
and drop the slots where no state changes at all, because those are not messages, they are a habit.
In the second, restore the order starting with the next message out, and stop accepting drafts that
arrive without one.
