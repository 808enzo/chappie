---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Drift, verification and retirement

A segment is the one artifact in this area of work that **decays without a symptom**. A broken
flow stops sending and someone notices. A broken segment keeps returning people, and they are
the wrong people. Nothing in the interface changes, the counts look plausible, and the sends
keep going out.

So a set of segments needs a scheduled review, and every live cut needs an outcome from it.

## Entry conditions

- The set has run for several cycles.
- You have a history of size and response per segment. Without the history there is nothing to
  compare against, and the first review can only establish the baseline.

## Exit conditions

Every live segment carries exactly one outcome: keep, re-cut the boundary, merge, or retire. You
dated the decision, and you marked the period before any definition change as not comparable
with what follows.

## Sequence

**1. Verify the recompute ran.** Not that someone scheduled it, that it ran, and when. This
comes first because a frozen segment is the failure that best imitates health. This review catches
it only when the review runs, so the recompute also belongs on the monitoring roster as a heartbeat
between reviews (`program-audit-and-ops`).

**2. Read the size history.** A flat size in a base that is moving is more suspicious than a
jump. Compare each segment's movement against the base's. A segment holding still while
everything around it shifts is either stable or no longer being recalculated, and those two look
identical until you check step 1.

**3. Check separation.** Does the segment still behave differently from the rest of the base on
the target metric, with both sides counted on the reachable base and read under the same
treatment? If it does not, the cut has stopped carrying information, however tidy the definition
and however many people it returns. This is the control metric of the skill (`SKILL.md` gives its
three conditions and a worked example), and it decides whether a segment kept for its response
earns its keep. A segment kept for a stated reason is judged by that reason, as the edge cases
below say.

**4. Look at the boundary population.** The share of people crossing in and out every cycle. A
large share means you drew the boundary through the dense part of the distribution, where small
movements flip people back and forth. Move the boundary, or accept that the two groups are one
group and merge them.

**5. Count the cost.** A cut costs assembly time and it costs reach: the deeper the division,
the smaller the audience of each send. Both are real and neither appears in any report by
default. Weigh them against what the separation is worth. Deepening the cut is a trade, and
people forget the reach side of it until the calendar stops filling.

**6. Take one of four outcomes**, keep, re-cut, merge or retire, and write it down with a date.
"Leave it for now" is not one of the four. It is how segment counts only ever rise.

**7. Mark the break in the series.** After a definition changes, comparison with the previous
period is invalid even when the size happens to match. Write that where the numbers live, not in
a message thread, because whoever reads the chart in six months will not be in the thread.

## Verifying an exclusion

A cut you use to withhold a send is a decision about money, and you verify it differently. The
correct comparison is **the same people, selected by the same rule, who did receive the send.**
Without it you cannot separate what you saved from what you gave up: the cost side shows up in
the channel invoice and the revenue side stays invisible by construction.

Intuition can fail here in a specific direction. A group excluded on the reasoning "they would not
buy anyway" can turn out to hold active customers who buy without being prompted. Excluding them
does save money, and the saving is real, but for a different reason than the one assumed, so the
rule does not transfer to the next campaign the way a correct rule would. Treat the reasoning
behind an exclusion as the hypothesis the comparison tests, not as its explanation.

So run the exclusion against a part of the people the rule selects, chosen at random, that receives
the send as if the rule did not exist. Read the difference as the margin
given up, and set it against the send cost saved: the exclusion pays only where the saving is the
larger of the two. Read on revenue alone, every exclusion that loses a single sale fails; read on
cost alone, every exclusion passes. Re-verify when you carry the rule to a different offer.
Designing that comparison belongs to `experiments-and-holdouts`, whose payback reading uses the
same margin. What belongs here is the obligation to demand it and the ability to read the answer.

## Thresholds and timings

- **Recompute cadence.** Set when you defined the segment, from the attribute's volatility.
  Review does not change it. A failed recompute does.
- **Review cadence.** A multiple of the recompute cadence, and no less than once per program
  cycle. Reviewing faster than the segment recomputes tells you nothing new.
- **Drift threshold.** A size change beyond that segment's own ordinary cycle-to-cycle spread,
  computed from its own history. Every segment gets its own. A shared number would flag the
  volatile ones constantly and the stable ones never.
- **Boundary-churn threshold.** The crossing share above which you move the boundary rather than
  the people.
- **Separation floor.** The smallest separation, in the target metric against the rest of the
  base, that still justifies the assembly cost. Below it, merge or retire.
- **Declared-attribute shelf life.** The age past which asking again costs less than being
  wrong, applied at review rather than waiting for a complaint.

## Edge cases

- **Separation vanished because the whole base moved.** Season, an assortment change, an outside
  event. The segment is not at fault and retiring it would be the error. Check the base's own
  movement before judging any segment against it.
- **The recompute job fails in silence.** The segment freezes in its last state and keeps
  sending. The tell is a size that does not move at all while neighboring segments move
  normally, which is the same signature as real stability. That is why step 1 exists.
- **A source system stops delivering the attribute.** The segment empties quietly and its people
  flow into the remainder. It surfaces in the remainder share rather than in the segment, so a
  review that looks only at live segments will miss it.
- **Someone changed the definition mid-period.** The series is broken. Do not compare across the
  change even if the sizes match, because matching sizes under different rules mean different
  people.
- **The segment is small and required.** A regulatory exclusion, a contractual obligation, a
  group under examination before a launch. You keep it for its stated reason, and the readable
  floor does not apply. Record why, or the next review will merge it away correctly and for the
  wrong reason.
- **An inherited cut nobody can explain.** If you cannot reconstruct the decision it was built
  for, retire it. Keeping it in case it matters is how a set becomes unmaintainable, because the
  unexplained cuts are the ones nobody dares touch later.
- **Two segments have converged on the same population.** The definitions differ and the
  membership does not. Merge them and keep the definition that costs less to compute.

## Failure modes

- **The number of segments only ever grows.** Nothing has been retired since the beginning,
  which means no review is happening, whatever the calendar calls it.
- **Nobody measures the outcome of an exclusion.** The saving gets counted, the margin given up
  does not, and you make a decision about money blind and confident. This is the most expensive
  failure in the skill because it compounds: an unverified exclusion rule gets reused.
- **The recompute is scheduled and nobody checks that it ran.** The state in which segmentation
  looks functional for the longest while being least functional.
- **Nobody counts the cost of cutting.** Segments proliferate, the reach of each send falls, the
  calendar gets harder to fill, and the diagnosis lands on the content instead.
- **Someone compares across a definition change.** A conclusion gets drawn, it is wrong, and it
  looks exactly like ordinary period-over-period movement. Nothing about the chart will warn the
  next reader.
- **Review happens, outcomes get discussed, and nobody writes them down with a date.** The next
  review restarts from the same arguments, and the set never converges.
