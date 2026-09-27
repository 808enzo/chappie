---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-14
---

# Control metric: how to read the unsupported send share

`SKILL.md` defines the metric: the marketing send, the join line and the trace line, and the denominator,
and says why sends and not people, and why not the opt-in rate, a flag share, the unsubscribe rate or the
complaint rate. This file holds what stays out of both halves, when a record covers a send, and how to read
the metric.

## What stays out of both halves

The confirmation message of a confirmed opt in and the one-time text confirming a revocation are service
rows, as `SKILL.md` defines them: each is a consequence of the person's own action, and neither enters
either half.

## When a record covers a send, by regime

The basis type is present; the point and the date resolve, through the registry of
`references/lawful-basis-and-collection.md`, step 1, to a wording version in the archive; under an
exception the event date is inside the term and the refusal-offered flag is set; under an opt-out regime
the source is present. A record with a field that does not resolve is no record for the join: a platform
that writes a row at every subscription writes rows, and the join reads only the rows whose fields
resolve, which is what keeps this line from becoming the flag share that `SKILL.md` rules out.

- **By regime** means by the regime of the person, from the country field on the person's row, an
  attribute in `list-building`'s plan whose consumer is this metric; the record carries the same value
  with the date it was set. "Unknown" is a line of its own. A send with no record is read by the same
  field, so the no-record sends do not all land in "unknown". The definition of "covers" differs by
  regime: under an opt-out regime a record is a source and an honored opt-out; under a consent regime it
  is the request and its proof; under an exception it is the event and its conditions, all of them.

## When the reading closes

- **The window.** The period is read once the longest propagation deadline that applies has passed, so
  that every instruction with a receipt inside the period is logged; an instruction logged later with a
  receipt inside a period already read reopens that period once, and the reading is written again with
  the date.

It is never added to the join line: the join counts every send and the trace counts a sample, and one
number made of both moves with the size of the sample instead of with the base. A period with no trace
read reports the trace line as "not read"; it does not report it as zero.

**An empty period leaves both lines undefined**, not zero.

## Where it moves

**Where it moves.** The join line goes down when capture points write full records, when imports go
through the same path as a form, when expiry timers run, when every route writes the same instruction
and every sending system reads it inside the deadline. It goes up when a new point, an import or an
acquired base lands without records, when a system drops out of propagation, when a merge moves a flag
without its record, when a service template gains a promotional block. The trace line goes up when the
trace starts and finds what the join could not, a version in the archive that bundled the request or a
point whose rows resolve to a version nobody showed the person: that rise makes the reading truer, and
it moves the trace line only.

## Read beside it

**What to read beside it, and promote none.**

- **Opt-in share by point and by wording version**, computed from the records: marketing records
  written at the point over contacts that entered through it, by version. The input to the wording.
- **Confirmation completion share and the age of pending rows**, where confirmed opt in applies.
- **Instructions per period by route and by scope**, and the kept share: instructions that chose a
  narrower option (a type, a frequency, a pause) instead of the withdrawal.
- **Honoring lag for each sending system**: the time from the instruction to that system's write, its
  maximum against the deadline that applies.
- **Bases expiring in the next window**, by regime: the refresh work ahead.
- **Access and erasure requests**: count, and time to close against the regime's limit.
- **Sends after an instruction, by system**, in two parts: inside the deadline, the cost of the lag;
  after it, the subset of the join line that names the broken link.

## What it cannot see

**What it cannot see.** A basis that is invalid for a reason neither the record nor the archive shows: an
incentive that made consent not freely given in your regime, or a regime read wrong for the person.
Those are questions for counsel; the trace is where a person reads the wording, and it sees a bundled
request only when the archive holds the page as the person saw it.
