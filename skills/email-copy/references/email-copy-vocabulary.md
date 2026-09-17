---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Vocabulary for email copy

The terms the four mechanics assume. The last section lists eight words this skill shares with its
neighbors, most of them under different meanings.

## The unit

**Job of a message.** What the message changes in the reader: the state they are in when it arrives
and the state it leaves them in. Not the topic and not the format. The unit of this skill.

**Promise.** What the message asserts as its debt to the reader. Usually inherited from a capture
point, an event, or a live offer, and almost never invented by the message itself.

**Inheritance.** The three things a message owes before it says anything: the wording of the capture
point, the event the person performed, and the offer that is live. A message can break all three
while knowing nothing about them.

## Claims

**Claim.** A sentence that can be checked for truth. It divides into claims with a fact under them
and claims without; the second kind is cut.

**Fact.** Something you can point at: a specification, a deadline, a condition, a policy, a count, a
named person. An evaluation is not a fact.

**Substance.** The set of facts collected before the writing starts. An empty set is a reason not to
send rather than a reason to write generally.

## What is seen before the open

**Inbox line.** Sender name, subject and preheader read together: everything visible before the
message is opened.

**Subject.** The field beside the sender name. Not the heading inside the message and not a
technical header.

**Heading.** The first large line inside the body. It continues the subject and does not contradict
it.

**Preheader.** The line a client shows after the subject. An unwritten preheader is not empty: the
client fills it with the first words of the body.

## Inside the message

**First block.** What the reader sees before scrolling. Measured here as an order of meaning rather
than in pixels; pixels are `email-design`. The requirement is that the job is named before the
reader has to do anything with their hands.

**Action.** The one thing the message asks for, named with a verb and an outcome.

**Exit.** The link or button through which the action happens. One action can have many exits.

**Index message.** A message whose job is to let somebody choose: a digest, a roundup, a list of
articles. The one case where many exits are legitimate.

**Link role.** One of four: work, support, navigation, required. Assigned in the brief, carried into
the reporting. The control metric reads the first three and excludes the fourth, which is why
required is a role of its own rather than a kind of navigation.

**Fallback wording.** The text that stands where a substitution would have gone when there is no
value. `personalization` chooses the level; the words are written here, next to the original
sentence.

## The review

**Blocking defect.** A defect after which the message does not go: a broken promise, a claim with no
fact, a legal breach, a broken substitution, a disappeared action, a destination that contradicts
the message or does not carry what it promised. In a flow that is already sending, the same classes
hold and the action becomes a pause through `program-audit-and-ops`.

**Remark.** Everything else. It stops nothing and is not discussed at the moment of sending.

**Short review.** Steps 1 to 3 only, run when there is no time, and named out loud as incomplete.

## The metric

**On-job click share.** The control metric: unique clickers on links with the role of work, divided
by unique clickers on a work, support or navigation link in that message. Required links are
outside both halves. Normalized inside one message, which is what removes the audience and the
delivery from the number.

## Eight words this skill shares with neighbors

| Word | Here | At the neighbor |
|---|---|---|
| offer | the wording of the promise in the text | `offer-design`: the construction of the benefit and its economics |
| personalization | the words a fallback is written in | `personalization`: where the value comes from and what happens when it is empty |
| message | what the email says | `triggered-messages`: what goes out and when |
| promise | the message's debt to the reader | `welcome-and-activation`: the promise of the entry point that the first touch keeps |
| subject | the field beside the sender name | `deliverability`: the same field as a provider and legal requirement |
| review | reading a draft before the send, which is the fourth sense of the word in this library and the only one whose object is not yet live | `program-audit-and-ops`: the audit of a running object; `scenario-map`: the roster review, the only place a row is retired; `crm-program-design`: the re-cut of the goal and the resource behind it |
| first screen | a requirement about the order of meaning | `email-design`: the area above the fold as a layout question |
| click | the event the job of a message is read on | `metric-definitions`: the formula and the denominator |
