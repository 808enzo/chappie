---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Vocabulary of program design

Terms all three mechanics assume. Four of them are words other skills use for something else, and
this file separates those at the end.

## The program and its goal

**Program.** All the work with people after first contact, across every channel at once, with one
goal, one owner per number and a build queue. A program is not a channel and not a set of sends.

**Program goal.** The change the program is pursuing this cycle, stated through a metric and
derived from the goal one level above it.

**Target metric.** The single number the program is judged on in a cycle. It moves in response to
what the program does, it converts into money through arithmetic you can show, and it is legible on
the population the program controls.

**Key result.** A smaller metric that a specific person moves directly, and whose movement brings
the target closer.

**Balancing metric.** A number that gets worse when the target is bought too expensively: the cost
of an incremental result, complaints, unsubscribes, message load.

**Leading metric.** A number that moves before the target does, which is what makes it usable for
steering inside a cycle.

**Link model.** A table where metrics are joined by formulas, so that changing one shows what
happens to the money. The instrument for testing a metric before it is committed to as a target.

**Read cycle.** How often the numbers are looked at.

**Revision cycle.** How often the goals and the queue are re-cut. Longer than the read cycle, and
kept on the calendar so that one bad period does not rewrite the goals.

**Zero point.** The value of a metric at the moment the program first named it as a goal. Not a
result and not a benchmark: the point movement is measured from.

## People and money

**Owner.** The person answerable for moving one number. Not whoever does the work by hand and not
whoever approves the budget.

**Ownership map.** The list of metric, segment, owner. The document that answers "whose number is
this" before anyone has to ask.

**Infrastructure owner.** The person carrying integrations, monitoring and the taking apart of what
broke, so that the owners of metrics do not switch onto that work.

**Service model.** A program whose work arrives from other departments and whose priorities are set
outside it. Its metric is delivery time and quality rather than growth.

**Budget gap.** The difference between the forecast for the base with no promotion and the goal.
What the promo budget exists to close.

## The queue

**Queue item.** A mechanic that has not been built yet, together with the list of what it needs.

**Dependency.** What an item cannot be built without. The three kinds are `scenario-map`'s, and this
skill uses those rather than a second set of its own: **data**, an attribute, an event or a basis
that does not exist yet or arrives too late for the item to read it; **mechanic**, where the item
needs what another item produces; **promise**, where the item needs a construction nobody has
signed off. A template waiting on somebody's approval is a promise dependency; a template nobody
has written yet is work, not a dependency. Whether the item is also **blocked** is a separate
question, answered by where the owner of the dependency sits.

**Blocked item.** An item whose dependency belongs to someone outside the program. It lives in a
separate list rather than in the queue.

**Lane.** One of the two groups in the queue: what the team builds with its own hands, and what
needs a change in a system the program does not own. The lanes run in parallel.

**Work in progress cap.** How many items are being built at once. An upper bound, not a plan.

**Slice launch.** A first send to part of the base, read before the rollout to all of it.

**Re-cut.** The regular program decision on the goal, the resource envelope behind it, and the
blocked list. Verdicts on rows that are already live belong to the roster review in `scenario-map`.

**Handover.** The dated point at which the program stops cutting its own build order and the roster
in `scenario-map` takes it over.

## Four words this skill shares with neighbors

**Program.** Here it is all the work after first contact. In `email-program` it is one channel run
as a program. In `loyalty-program-design` and `loyalty-program-launch` it is a construct inside the
program, with rules and a launch of its own.

**Owner.** Here it is the person answerable for moving a number. In `scenario-map` it is the person
a row carries from admission onward, who answers for that mechanic after launch. In
`program-audit-and-ops` it is whoever the broken object goes to. In `metric-definitions` it is
whoever owns the definition of the number. In `martech-stack` it is the system where a fact comes
into existence. Five different questions: who grows the number, who runs the mechanic, who fixes
it, who defines it, where it lives. The first two are the pair worth keeping apart on purpose: the
same person often holds both, and the moment they do not, a row with no result and a number with no
movement are two different conversations with two different people.

**Priority.** Here it is build order in the queue. In `contact-orchestration` it is precedence
between messages at send time, when two of them arrive at the same person.

**Review.** Four of them, on four objects. Here it is the calendar re-cut of the goal and the
resource behind it. In `scenario-map` it is the roster review, which gives every live row a verdict
and is the only place a row is retired. In `program-audit-and-ops` it is the audit of a running
object, which establishes that something is broken and sends the finding to the roster review
rather than acting on the composition itself. In `email-copy` it is the review of a draft before
the send, the only one whose object is not live yet.
