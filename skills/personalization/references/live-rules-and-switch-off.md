---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# Live rules: the register, the decay signals, and switching one off

The unit here is a **live rule**: a place or a placement already running on real people. This
mechanic is a separate file because its sequence is the same for both. You check output before
launch, you reread a fixed set of signals on a cadence, you catch a signal, and you replace the
rule. Split across the first two mechanics, that sequence would be written twice.

## Entry conditions

A rule is in production: a place from `substitution-and-empty-values.md` or a placement from
`recommendation-blocks.md` has been built and shipped.

## Exit conditions

The rule is in the register with an owner, a launch date and a date of last check. Or it has been
switched off, with a record of what took its place.

## Steps

**1. Keep a register of live rules.** One line per rule: the place, the source or the anchor, the
moment of resolution, the format contract, the fallback, the check case, the owner, the launch date,
the date of the last check. Those are the five things `substitution-and-empty-values.md` writes
down per place, plus the three the register adds. Leave the format contract and the check case out
and you write them once at launch and never read them again. Without a register nobody knows how
many rules are running: a rule outlives the campaign it was built for and keeps working long after
everybody has forgotten it exists.

**2. Check output before launch, not configuration.** The four seed profiles from
`substitution-and-empty-values.md`, step 7, and for a block, a named person whose output you compare
against what they viewed and bought. Configuration can read as correct while the output is
wrong, which is why the check looks at what came out.

**3. Reread the signals on a cadence, in one order.** Six of them, cheapest first:

1. the resolved share for the place, against its own baseline;
2. the count of distinct items the block emitted over the period, at the level its anchor resolves
   to;
3. the fill rate of the source field, and whether it has drifted since the rule was written;
4. the shape of the values arriving from that field, against the format contract in the register;
5. the fill rate of the catalog fields the selection runs on;
6. the split of one place's fallbacks by level: what share of its evaluations shipped a neutral
   value, what share shipped the rewritten version, and what share shipped nothing. Read per place,
   the way the resolved share is read; pooled across places it moves with the campaign mix.

**The fourth signal is there because nothing else catches a format drift.** The field holds a
value, so the fill rate looks right. The value came from the assigned source, so the resolved share
looks right. Meanwhile the message goes out with a job title in capitals sitting in the middle of a
sentence. A format contract nobody rereads is a contract at launch and nothing afterwards.

The cadence follows how fast the thing the rule reads changes, not the calendar. A catalog that
turns over weekly and a profile field that changes once a quarter do not get the same interval.

**4. Switch a rule off on a signal.** Four signals, each with its own action:

- **the source fill rate fell below the floor**: the fallback becomes the main version, and the
  message is rewritten around it;
- **the anchor stopped resolving for most people**: the rule drops a level and is renamed for what
  it has become, from personal to category based;
- **the constraints stopped holding after a merchandising change**: the rule is repaired or
  switched off, and does not stay in a "leave it for now" state;
- **the comparison against a fixed alternative shows no difference over a defensible period**: the
  rule comes off and the fixed version takes the placement, because it is cheaper to keep.

**5. Switch off as replacement rather than deletion.** Record what takes the rule's place, who
finds out, and what data stops being collected. A rule carrying a core class message
(`substitution-and-empty-values.md`, step 6) is never removed on its own: without a replacement it
leaves the message with nothing to be about.

**6. Hand the duty over.** Monitoring live scenarios, incidents and the roster belong to
`program-audit-and-ops`. What belongs here is the list of signals specific to personalization and
the order they are read in. The escalation route stays with the neighbor.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Reread interval | how fast the source and the catalog change |
| Period for the comparison against a fixed alternative | the requirement set by `experiments-and-holdouts` |
| "The anchor stopped resolving for most people" | the placement's own baseline |

## Edge cases

- **The rule cannot be switched off** because the message is about the value it supplies. Replace
  it rather than removing it.
- **One rule duplicated across several placements.** The register shows it by source. Fix it at the
  source, or the other copies keep running.
- **The rule has no owner** because the person left. Reassign it or switch it off at the next check.
  Nothing else counts as a state.
- **The rule outlived its campaign.** The launch date in the register is the tell: a rule whose
  carrier ended gets checked for whether it still makes sense at all.

## Failure mode

**Slow decay.** The rule ships fallbacks for months, the catalog is no longer the one it was
written against, the source field fills worse every quarter, and no report shows any of it, because
reports count sends and clicks rather than what got substituted. What catches it is the register
plus the cheapest signal, read on a cadence.

**Checking configuration instead of output.** The rule was checked in the interface, where it read
as right, and on a real person it returns something else. What catches it is reading one named
person's output.
