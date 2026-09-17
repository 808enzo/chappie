---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Vocabulary of the roster

Terms all three mechanics assume. Three of them are words other skills use for something else, and
this file separates those at the end.

## Units

**Mechanic.** A standing rule: it fires on an occasion and can run for a long time without being
edited. The unit of the roster. Its opposite is a campaign, not a message.

**Campaign.** A dated send built around a particular offer. The test: change the date and the
offer. A campaign stops making sense, a mechanic does not. Campaigns live in `promo-calendar`.

**Roster.** The single list of the program's mechanics: occasion, audience, the decision served,
owner, stated firing volume, admission date, last-read date, status. Kept outside the sending
platform, because it also holds what the platform cannot: rejected candidates, and rows waiting on
a prerequisite.

**Status.** One column with a closed set of values, and the set is closed on purpose so that a row
cannot be filed under a word invented for it: **waiting on X**, where X is a named prerequisite
with an owner and a date; **waiting on volume**, where the occasion exists and almost nobody
triggers it yet; **building**; **live**; **paused**, pending review; **retired**. The one word that
is not a status is **planned**: it obliges nobody and survives any number of quarters, which is why
every waiting row names what it waits on instead.

**Row.** One mechanic on the roster. One decision, one row, even where the implementation of two
rows will be a single flow.

**The decision a row serves.** One sentence: what the person should do, and inside what window.
Without it a row cannot be ordered, read or retired, because there is nothing to say it failed at.

## Admission

**Admission test.** Five questions asked of a candidate before it is built: is there an occasion,
does the data exist in the freshness class needed, will it fire often enough to earn a slot, is a
basis available for the audience named, and is there an owner after launch. A "no" is a
prerequisite with an owner and a date, not a rejection.

**Stated firing volume.** The estimate made at admission from the last comparable period: how many
people will meet the condition. Written into the row so that the actual has something to be
compared against. Counted in people who met the condition, not in sends.

**Industry set.** A ready-made list of mechanics for a business or a stage. A source of occasions
and not a source of constants.

**Own constants.** The values computed from your own data that configure a standard mechanic:
purchase cycle, length of relationship, decision window.

**Overlap.** Two rows coinciding on an occasion, on a person inside one window, or on a promise.
The first and third are settled by the roster; the second is load, and load is settled by
`contact-orchestration`.

## Building and reviewing

**Dependency.** The reason a row cannot be built yet. Three kinds: **data**, closed by somebody
else's work against a date; **mechanic**, closed by another row producing its output; and
**promise**, which does not close at all until a construction is agreed.

**Wave.** The portion of the queue one owner can verify end to end before the next one starts. A
quantity of the reader, not of the platform.

**Ramp-up window.** The period a row gets after launch before its first verdict. Before it there is
nothing to read, and a verdict given inside it retires working mechanics.

**Verdict.** One of the four outcomes of a review: keep, rework, merge, retire. Given with a date;
without a date it has not been given.

**Retirement record.** What the row did, why it went, and what would bring it back. Without it a
retired mechanic returns in a year as a fresh idea and passes admission a second time.

## Three words this skill shares with a neighbor

**Scenario.** In `triggered-messages` it is a flow: a firing event, steps, delays, branches, a stop
condition. Here it is a row on the roster: the mechanic as a unit of the program's composition,
whatever number of flows implements it. The same word for two different objects, tied together by
one rule: the neighbor reviews the live set of flows, and the roster decides whether a row exists
at all.

**Review of the set.** In `triggered-messages` it is the review of live flows (entries, conversion
per entry, contribution to load) and it answers whether a flow works. Here it is the roster
review, and it answers whether the decision deserves a mechanic. The roster neither repeats the
neighbor's reading nor overrides it: it takes the result and adds its own question.

**Owner.** Here it is the person a row carries from admission onward, who answers for that mechanic
after launch. In `crm-program-design` it is the person answerable for moving one number, and that
skill names three more senses the library uses. The same person often holds the row and the number,
and the two are still named apart, because a row that never fired and a number that never moved are
two different conversations. The row's owner is written into the row at admission; the number's
owner is written into the ownership map.
