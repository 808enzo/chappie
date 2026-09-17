---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# Monitoring duty: the roster, the heartbeat, the slot

Watching a program is not watching campaigns. It is a finite list of objects, each with a countable
sign that it is alive and a stated length of silence that means nothing is wrong. Without those two
columns, monitoring degrades into opening dashboards until something looks odd.

## Entry conditions

You need this file when more than a handful of objects run unattended, when somebody outside the
team is the one who spots the breakage, or when alerts arrive so often that nobody opens
them.

## Exit conditions

The roster covers every object that can go quiet, each one has an owner, a heartbeat and a line
that turns quiet into broken, and the slot closes more records than it opens.

## Steps

1. **List objects, not campaigns.** An object is anything that can stay switched on and stop doing
   its work. Ten classes cover a normal program:

   | Class | Heartbeat | What its absence means |
   |---|---|---|
   | Sending flow | sends in the period | the flow did not fire, or it selected an empty audience |
   | Scheduled send | the issue went out on time | the issue was never assembled, or it went out late |
   | Export or connector behind a metric | fresh rows arriving | the metric is being read off stale data |
   | Running experiment | assignments into groups | assignment stopped while the window kept running |
   | Contact policy rule | suppressions firing | the rule is not being applied and the cap is not holding |
   | Capture point | contacts accepted | the point is not showing, or the form is not submitting |
   | Segment behind a send | the recompute finished on schedule | the audience is frozen, so sends go to a list that stopped moving |
   | Consumable resource | what is left in the pool | you cannot deliver what the message promised |
   | Derived attribute computed on read | it still returns a non-empty value | the events behind it aged out, so the attribute went empty and every segment on it shrank |
   | Open record with a promised time | a closing entry by the time written on the record | the record lies open past its time, and nothing about it fails loudly enough to be seen |

   A frozen segment and a derived attribute are among the hardest of the ten to see. A frozen segment
   does not go quiet: the sends keep going out, to a list that stopped changing. `segmentation` owns what the segment is and how
   often it should recalculate; the roster watches whether that recompute ran. A derived attribute
   computed on read does not go quiet either: it answers, and it answers empty, on the day the
   event retention window rolls past the period it looks back over. `martech-stack` owns the split
   between an attribute stored as a fact and one computed on read; the roster watches whether the
   computed ones still return anything.

2. **Set expected silence from your own history, not from instinct.** Take a period when the object
   worked, find the longest gap between heartbeats, and add margin. Silence longer than that opens
   a record. Silence shorter than that is normal, however uneasy it makes you. One class in the
   table does not work this way: a consumable resource reports a level rather than an event, so it
   is never silent and has no gap to measure. Its line is what is left, counted in days of supply at
   the current rate of use, and crossing that line opens a warning rather than a problem. An open
   record does not work this way either: its line is written on the record itself, as the promised
   time, the deadline or the ceiling that a neighboring skill sets, and a record still open past that
   line is a problem from the day it passes.
3. **Measure the heartbeat at the entrance as well as the exit.** A flow whose audience selection
   broke still runs: it fires and sends to nobody. Sends read zero, so you also need the events
   arriving at the entrance, which separate "the event never happened" from "the event happened and
   nothing went out".
4. **Assign the owner by where it broke, not by how important the object is.** Integrations,
   exports and load go to whoever works on the systems. Conditions, segments, content and schedules
   go to whoever runs the program. The owner does not set responsibility so much as duration: a fix
   inside somebody else's sprint takes weeks, a fix in your own tool takes minutes.
5. **Split records into two classes.** A **problem** means the object is not doing its work now. A
   **warning** means it works and is going to break: the pool is draining, the error share is
   climbing, the filter takes longer to recalculate every week. They route differently. Problems go
   to the next slot, warnings go into a queue with a date.
6. **Subscribe to alerts selectively.** Set an alert where waiting until the next slot costs more
   than the interruption does, and on every object whose failure would land in a severity class in
   `incident-response.md`, whatever it costs. Everything else waits for the slot. Subscribe to
   everything and alerts become background, at which point none of them work, including the one you
   set up first.
7. **Run the slot at a fixed time in a fixed order, and put severity ahead of the order.** Take any
   record whose fault falls in one of the three severity classes in `incident-response.md` out of
   the slot the moment you see it and hand it to the person who owns that class, whether it touched
   one person or a hundred thousand. Everything left is ordinary, and ordinary work goes down by
   exposure,
   meaning people affected in the period multiplied by the value of the action at risk, then new
   records, then repeat offenders. Fix that order deliberately, because reading the system's own
   list top to bottom sorts your attention by whatever is noisiest.
8. **Close every record with one of four outcomes:** fixed; handed to an owner with a date;
   accepted as tolerable until a named date; object retired. A record with no outcome is why
   rosters stop being opened after two months.

## Objects that neighboring skills define

Six skills hand the roster objects of their own. Four of the six bring mostly the tenth class: a
record that someone promised to close by a time and nobody closed. What each object is, and what its time is,
stays with the skill that defines it; whether it went silent is read here.

- **A live personalization rule** (`personalization`). The rule keeps sending while what it
  substitutes decays, so sends are not its heartbeat. Read its six signals on a cadence, in this
  order, cheapest first: the resolved share for the place against its own baseline; the count of
  distinct items the block emitted; the fill rate of the source field; the shape of the values
  arriving from that field against the format contract; the fill rate of the catalog fields the
  selection runs on; the split of one place's fallbacks by level. The cadence follows how fast the
  thing the rule reads changes, not the calendar. The signals that switch a rule off, and what
  replaces it, are the neighbor's (`live-rules-and-switch-off.md`, steps 3 and 4).
- **The status map and service rows** (`transactional-messaging`). The status map is an object: an
  internal status that holds transactions and has no line in the map reads as "no change", with the
  timer still running and a signal to the map's owner, and that signal is a roster record. The
  heartbeat of a service row is the ratio of messages sent for it to the transactions that entered
  its state, minus the exclusions written for the row. A ratio that falls while events hold is a
  broken row; events that stop are a fault in the system of record or the integration. The expected
  ratio is defined there (`deadline-channel-and-failover.md`, step 8); you watch it here, and a
  required row that fails is a missed obligation (`incident-response.md`, step 3).
- **The ask flow** (`voice-of-customer`). Its heartbeat is asks per closing state, read by part of the
  experience. A part that has asks and no answers is a silent object, not a healthy one. An obligation
  (an answer below the threshold, which owes the person an action) still open past its promised
  time with no closing entry is a duty signal on its route. A wave of low scores on one part inside a
  short window is a candidate incident. Definitions: `closing-the-loop.md`, step 4 and the edge case
  on a wave.
- **The handoff and the next step** (`b2b-lifecycle`). Four objects: a handoff with no acceptance
  outcome by its promised time; an account past the handoff with no next step written in the
  register; a "not now" return whose re-entry date passed with no re-entry into the grade; a date the
  customer promised that passed with no step from the account executive. Definitions:
  `qualification-and-handoff.md`, steps 7 and 8; `buying-group-and-stalls.md`, steps 5 and 8.
- **Subscription terms and cases** (`subscription-retention`). Four silent objects: a term past the
  platform's collection window with no charge event, where billing is silent and the subscription
  still reads "active"; a recovery case past its deadline with no closing entry; a cancel request
  made by message past its promised time with no closing entry; a pause with no resume date. For
  recovery cases, read the heartbeat on closure: a case closed on its deadline with zero messages
  means the row's route is down. Definitions: `term-end-and-notices.md`, step 5; `failed-charge-recovery.md`, steps 2 and 6;
  `exit-and-save.md`, steps 1 and 7.
- **Contract terms billed by invoice** (`b2b-retention`). Seven silent objects: a won-deal record not
  accepted by its promised time; a contract that bills invoices and has no row in the contract
  register, or no decision point; a decision point that passed with no recorded outcome of the
  renewal case; a holdover past its ceiling with no closure; a collection case past its ceiling with
  no closure; a milestone of the success plan past its date and grace with no record; an amendment
  with an end date of its own, which gives one buying unit two decision points. The heartbeat:
  renewal cases open on their opening date, and a case that opened later is the row failing.
  Definitions: `success-plan-and-qbr.md`, step 1; `renewal-case.md`, step 1; `invoice-collection.md`,
  step 2; `expansion-and-contraction.md`, the failure mode on two decision points.

## Thresholds and timings

- **Derive the duty interval from how fast damage accrues, and read what comes out as a ranking
  rather than an optimum.** You need six quantities, written in units that compare: the loss per day
  while the object is broken, the cost of running one check, how often this object breaks, the
  detection delay you are willing to carry, the shortest interval anyone is available to act on, and
  whether anybody reads an alert on this object.
- **Get the loss per day right first.** People touched per day multiplied by the value of the action
  at stake is what passes through the object, not what you lose when it stops: some of those people
  buy anyway, later or elsewhere. The daily loss is that figure times the share the object itself
  produces, which comes from a holdout (`experiments-and-holdouts`) or from an assumption you write
  down as one.
- **Then weigh waiting against checking, in the same units.** A fault that starts at a random moment
  waits half an interval on average before anyone finds it, so the loss you expect to sit through is
  the daily loss times half the interval. Halving the interval halves that and doubles what the
  checks cost over the same stretch of calendar, so price the checks in money per period, the same
  way you priced the loss. Otherwise you are weighing effort against revenue, and that comparison
  settles nothing. Scale the result by how often the object breaks: an object that fails most months
  and one that has never failed do not earn the same interval. Where you have a history, take the
  rate from this object rather than from the category; where you have none, name the rate you
  assumed and revise it after the first failure.
- **A floor sits under the arithmetic.** You cannot check faster than somebody can act, so the
  shortest interval worth setting is one an owner is around for. Below that floor the only shorter
  option is an alert, and an alert shortens detection only while people still read it (step 6). When
  the arithmetic keeps pushing under the floor, the answer is an alert with an owner behind it, not
  a shorter slot.
- **This is not a solved optimization, and calling it one costs you the revision.** Read the result
  as a rank: this object deserves a shorter interval than that one. Do not read it as a number of
  hours. Take whatever interval it produces as a starting position and move it against what the
  object turns out to do.
- **Expected silence is the longest gap observed in a healthy period, plus margin.** For a rare
  object that gap is long, which is not a reason to leave it off the roster: for rare objects, the
  heartbeat is the arriving event rather than the send.
- **Seasonal objects get seasonal expectations.** A mechanic that runs three months a year is
  silent correctly for the other nine, and one flat threshold manufactures the same false problem
  every year.
- **The slot caps the roster.** If there are more objects than the slot can walk for
  several slots running, the roster is wider than your duty. Three levers close that gap: cut the
  roster back to objects with real exposure, lengthen the slot, or cut
  what one object costs to check by giving it an alert that reports itself. Choosing none of the
  three is how the slot quietly stops happening. One exception survives the cut: keep an object
  whose failure would land in a severity class at any exposure, because exposure is not what makes
  that one expensive.

## Edge cases

- **The object is silent for a good reason.** Paid traffic was switched off, so welcome sends
  dropped. That is a consequence rather than a fault, and it still belongs in the roster with the
  external cause written next to it, or you will run the same investigation next month.
- **One fault opens dozens of records**, one per failed send. Group by cause before you prioritize,
  or the most numerous fault gets worked first while the most expensive one waits.
- **The fault is in the platform, not in your configuration.** A record only leaves your team with
  evidence attached: timestamps, the object identifier, the relevant log lines. Without them the
  escalation comes back as "cannot reproduce" and the cycle repeats.
- **Two owners at once**, with one person editing conditions while another repairs the export. A
  record has a single owner at a time. The second person waits or gets a record of their own.
- **An object with no owner.** This appears when somebody leaves and their mechanics keep sending.
  Either it gets an owner or it gets retired. Leaving it running because it currently works is a
  deferred incident.

## Failure modes

Duty fails in four ways, and each one has a tell you can watch for.

1. **The roster is kept and records never close.** Tell: the share of records older than several
   slots grows from slot to slot. Within a few months nobody opens the slot, because opening it
   accomplishes nothing.
2. **Detection lives on complaints.** Tell: the share of incidents found by a customer, a colleague
   or your vendor rather than by duty. A complaint is the worst detector available. The people who
   write are a self-selected group, the rest stop showing up without saying why, and you cannot
   reconstruct the size of the damage from the number of complaints.
3. **Alerts go quiet.** Subscribe to everything, treat it as background, mute it, and then silence
   reads as health. Tell: no alert arrived all period while records kept appearing in the roster.
4. **Monitoring without owners.** Everything lands on one person who cannot repair an integration.
   Tell: records close as "handed to an owner" and stop closing as "fixed".
