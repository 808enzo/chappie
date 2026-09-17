---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# Incident response: stop it, size it, find the cause, write it down

A fault that has already reached people is a different job from watching for one. The order matters
more than the speed: teams that diagnose before they stop spend the investigation adding to the
number of people affected.

## Entry conditions

Something that runs has visibly misbehaved: nothing went out, it went out twice, it reached the
wrong people, it carried the wrong content, it arrived after it stopped meaning anything, or it
showed somebody data that was not theirs.

## Exit conditions

The object works again on its own heartbeat, anything that tripped the severity gate has reached
the person who owns it, the people affected have been counted, the correction decision has been made
either way, and the log carries a cause class and the check that would have caught this sooner.

## Steps

1. **Open the incident before you investigate.** The minimum record is the object, the symptom, the
   time of the first failure taken from the data rather than from when you noticed, and how you
   found out. Write the first failure time first. A week later you cannot recover it, and
   without it you can measure neither detection time nor damage.
2. **Name the failure class.** There are six, and they lead to different decisions: **silence**
   (nothing went out), **duplication** (it went twice), **wrong audience**, **wrong content**,
   **late**, and **disclosure** (the message showed the recipient something that was not theirs to
   see).
3. **Route by severity before you weigh cost.** Three kinds of fault leave the marketing queue the
   moment you name them. None of them waits for a slot, a size estimate or a correction decision.

   | Severity class | What happened | Who hears about it immediately |
   |---|---|---|
   | Disclosure | somebody saw personal data that was not theirs: another person's name, order or balance, or a recipient list carried in the open | whoever owns privacy or security |
   | Wrongful permission | somebody holds a right they should not, or lost one they should keep: a discount granted to people who never qualified, an opt-out that stopped suppressing, a link that opens somebody else's profile | whoever owns the entitlement, and privacy as well when the right in question is a consent flag |
   | Missed obligation | a message you are required to send did not go, went late, or went out wrong | whoever answers for the obligation, which is rarely marketing |

   Record the class next to the failure class. They answer different questions: you repair by the
   failure class, and you escalate by the severity class.

   **One person is enough.** Do not scale severity by how many people the fault reached or by what
   the send was worth. One wrong name in one email is a disclosure; the largest promotion of the
   year going silent is not. Order ordinary faults by exposure after this gate, never through it.

   Write the route down before you need it: the role, the person currently in it, and how to reach
   them outside working hours. Invent the route during an incident and the first hour goes to
   finding somebody instead of to stopping the fault. Reporting runs on a clock somebody else sets
   (`SKILL.md` quotes the EU articles that set it), and this library does not describe the procedure: name the person who owns it where you work,
   and route to them. `consent-and-preferences` covers lawful basis and the records you keep,
   `transactional-messaging` covers what a required message must contain and how fast it has to
   go.
4. **Stop before you diagnose.** Pause the object, halt the send, pull the message where the channel
   allows it. Diagnosis without stopping is diagnosis while the affected population grows.
5. **Size what already went out:** how many people, which ones, what they saw. Do this before the
   correction decision, because the decision follows from the size and the content rather than from
   how bad it feels.
6. **Decide on a correction with three questions.** Did money or a promise change? Can you identify
   who was affected? Will the correction reach more people than the error did? Money, dates and
   promises always get corrected. Typos and broken layout never do: the correction spends a
   contact and repeats the error to everyone who missed it.
7. **Walk the cause ladder from the top**, rather than starting at the level where you noticed:

   | Rung | What you check | Typical finding |
   |---|---|---|
   | 1. Entrance | are events arriving, did the segment recalculate | the site stopped sending the event |
   | 2. Condition | selection, negations, per person caps, expiry | a missing "not"; a test address left in; a once-per-lifetime cap on a repeating event |
   | 3. State | switched on, not paused, running the version you think | a pause set while the template was edited and never lifted |
   | 4. Content | template, substitutions, links | a template edit broke the name substitution |
   | 5. Channel | handoff and channel limits | the send hit a channel limit, which hands off to `deliverability` |
   | 6. System | load, queues, connectors | a heavy segment filter, or simultaneous recalculations stalling processing |

   The order is not arbitrary. Each rung explains the one below it and costs less to check. Start
   at the bottom and you will tune capacity for a flow that never received an event.

8. **Line a dip up against the failure window when the symptom is a number.** Take the objects whose
   metric sagged, group them by something they share, establish the failure window for each group,
   and compare the metric inside the window against that group's own norm outside it. Treat the
   fault as the place to look when the dip appears only in affected groups and only inside their
   windows. **This reads a fact, it does not run an experiment.** A before-and-after gap does not
   separate the fault from seasonality or from anything else that moved that week, so any claim
   about what the fix achieved belongs to `experiments-and-holdouts`. What you get here is where
   to look.
9. **Fix it, then confirm recovery on the heartbeat rather than on the absence of errors.** Errors
   also disappear when an object is switched off. Recovery means the object is producing its sign of
   life again at the level you expect.
10. **Add the two fields the log exists for:** the cause class, and **which check would have caught
    this sooner**. The second field is how an incident puts a new object on the roster, and it is
    one of two routes there. The audit is the other: it finds the objects that never broke loudly
    enough to reach this log. Every incident either gives an object a heartbeat it lacked, or states
    plainly that faults of this class are visible only after the fact.

## Thresholds and timings

- **The channel bounds what you can recall, and the bound is dictated by the channel.** A widget, a
  chat message and a bot can be pulled from people who have not opened or answered them. A delivered
  email cannot: once it is in someone's mailbox it is theirs, and the only repair is a second email.
  The bound covers delivered mail. The part of the send still sitting in the queue can be stopped
  where the platform allows it, which is the next bullet, so the first question in an email incident
  is how much of the send has already left. When a message stops
  making sense on a known date, set that expiry when you build it: automatic removal on a date costs
  nothing compared to handling it afterwards.
- **Start the severity clock at the first failure, not at the moment you classified it.** Step one
  already made you take that time from the data. A disclosure you find on Friday that began on
  Monday has been running four days, however late you opened the record.
- **Stopping a running send means pausing it, not canceling it,** until you have decided whether to
  repair or rebuild. In several systems canceling destroys the send statistics, and with them your
  ability to count who was affected.
- **Treat a running send as uneditable.** Where a platform does allow an edit in flight, part of the
  audience has already received the old version, so you now have two versions out and no record of
  who got which. Rebuilding is what keeps that answerable. The two moves that stay safe while it is
  in flight: stop it, or let it finish.
- **A correction goes to the affected population and no further.** Sending the apology to the whole
  base informs everybody who never saw the error and spends a contact on all of them.
- **Compare the repair time against the damage window.** If the fix waits longer than the damage
  accumulates, switch the object off while it waits. A broken object left running costs more than a
  disabled one.

## Edge cases

- **It went to the wrong people, and some of them never consented.** That is a wrongful permission
  fault, so route it through step three before you do anything else. Lawful basis and what you have
  to record belong to `consent-and-preferences`; what you have to report, and to whom, is the privacy
  owner's procedure that step three routes to, and this library does not describe it. The duty that
  stays here is capturing who was affected and when.
- **The error was in a price or a discount.** The correction carries the weight of a promise, and
  that decision is not made inside marketing. Your job is the record: what went out, to whom, when.
- **The flow sends into a void.** Selection broke, the audience is empty, no errors anywhere. Only
  an entrance heartbeat catches this one.
- **Duplication across two systems.** Neither log shows a duplicate, because each system correctly
  reports its single send. The duplicate exists only in the person's contact history, which is where
  you have to look.
- **A fault inside a running experiment.** Pause the whole test. Repairing it in flight and
  continuing to read the same result is a decision for `experiments-and-holdouts`, which has its own
  stopping rule.
- **The fault cleared itself before you found it.** Log it anyway, marked as evidence lost. Three of
  those on one object is itself the argument for giving that object a heartbeat.

## Failure modes

- **You fix symptoms.** Tell: incidents recur on the same object with the same cause class, and the
  field for the check that would have caught it earlier is empty in every record.
- **The correction goes to everybody.** The error becomes known to an audience that never saw it,
  and the apology is now the most widely read thing you sent that week.
- **The investigation sits in somebody else's queue** while the object stays switched on and keeps
  causing harm. This is step four going unapplied: nobody considered switching it off for the
  duration.
- **You rate severity by size.** Tell: the log ranks one wrong name below a promotion that went out
  late, and the privacy owner hears about disclosures from somebody outside the team.
- **The log is kept without the first failure time.** Detection time then cannot be computed, and
  duty stops improving because there is nothing to measure against.
