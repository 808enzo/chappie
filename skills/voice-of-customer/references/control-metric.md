---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Control metric: how to read the closed-on-time share

`SKILL.md` defines the metric: the obligation, what identifies it, what closes it on time and what does not, the
denominator, and why obligations rather than answers or the score. This file holds how to read it.

## Two readings, and when each closes

- **Two readings.** At the period's end the share holds the obligations whose promised time had passed by then.
  You read it a second time when the reopen window of its obligations has closed: the rest of the period's
  obligations enter, closures that were reopened leave the numerator, and a public review of the period
  identified after the first reading enters as late, because its timer ran from the posting. The published
  figure stays, and the correction goes into a restatement note (`crm-reporting`).

## The metric on invented numbers

Take a worked example with invented numbers. In a month, 120 identified obligations reached their promised
time. 84 were closed on time with a substantive outcome; 15 were closed late; 9 ended unreachable; 12 have no
closure record. The metric is 84 over 120, about 70%, not 84 over 108: the twelve without a record count
against the loop.

## What moves it

**Doubling the asks at the same quality leaves the share flat.** Obligations and closures double together.

**Where it moves.** Down when a route has no owner, when the timer starts at reading instead of at the answer,
when an automatic acknowledgement stands in for a reply, when a channel leaves people unreachable, when a wave
hits one part of the experience. Up with the steps of `references/closing-the-loop.md`.

## Read beside it

**What to read beside it, and promote none.**

- **Response share and coverage:** answers over delivered asks, answers over experiences.
- **Obligations over answers, per threshold version;** and the declined-contact share of low scores, per
  instrument version.
- **Time to the first substantive reply,** time to closure, and promises per obligation.
- **Outcomes by kind:** fixed, explained, compensated, already remedied, out of scope, unreachable.
- **Reopen share:** a second signal from the same person about the same experience inside the window: a second
  low score, a public review after a closure, a complaint, a chargeback.
- **Asks over experiences by part**, and complaints per order through other channels.
- **Unidentified negative public reviews**, as a count.
- **A hand-read sample of non-respondents.** Silence is not success: each period, a random handful of people
  who did not answer and showed low activity afterward is read by hand or called. As a starting point, size the
  handful from the readable floor in `references/reading-and-change.md`; that holds for programs where
  complaints also arrive through support, and it is replaced by complaints per order by channel once that
  figure exists.

## What it cannot see

**What it cannot see.** Obligations that never arose because the population was filtered (the counterweights
above); the quality of a fix (verification in `references/reading-and-change.md`); a closure on paper that
was not reopened inside the window, because a public review after the window is not caught.
