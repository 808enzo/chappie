---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-06
---

# Vocabulary of running a program

The three mechanics assume these terms. The first two carry most of the weight: without a heartbeat
and a stated expected silence, monitoring has nothing to compare against and turns into opening
dashboards until something looks wrong.

**Object.** Anything that can stay switched on and stop doing its work. Sending flows, scheduled
sends, exports behind a metric, running experiments, contact policy rules, capture points, segments
behind a send, consumable resources, derived attributes computed on read, and open records with a
promised time are all objects. Campaigns are not: a campaign is a plan, and a plan cannot go
quiet.

**Heartbeat.** The countable event that proves an object is working: sends, events arriving at the
entrance, rows landing in an export, assignments into experiment groups, suppressions firing,
contacts accepted, a recompute finishing, what is left in a pool, a closing entry by its time. An object with no heartbeat cannot be monitored, only
remembered.

**Expected silence.** The longest gap between heartbeats observed while the object was healthy, plus
margin. It is the line that turns "quiet" into "broken", and you set it from your own history rather
than from a number somebody quotes. It applies to objects that report events; a consumable resource
reports a level instead, so its line is what is left, measured in days of supply at the current rate
of use. An open record carries its line on itself, as the time a neighboring skill wrote on it.

**Open record with a promised time.** A record that someone has to close by a time written on it: a
handoff awaiting acceptance, an obligation owed to a person who answered, a recovery or collection
case, a request to cancel, a date the customer promised, a renewal case at its decision point. The
skill that defines the record sets the time (`b2b-lifecycle`, `b2b-retention`, `subscription-retention`,
`voice-of-customer`); the roster reads whether it closed by then. Nothing about an open record fails
loudly, which is why it counts as an object: past its time it reads the same as a record still on
schedule.

**Consumable resource.** An object that reports a level rather than an event: a pool of codes, a
prize fund, stock behind a promise. Monitoring the level and raising the signal are ours. What the
level is set to, and what is owed to people already holding a promise once it is reached, belong to
`offer-design`, whose vocabulary states the same split from the other side. Two consequences for
the duty roster: the stopping level arrives from there rather than being chosen here, and it is
never zero, because the resource keeps draining between two checks. What drains it differs by
resource, which is why the level is theirs to set: a pool of codes goes down as they issue codes,
a prize fund and stock on a shelf go down as people redeem.

A third skill meets us on the same word from a different direction. In `loyalty-program-design`,
**redemption** is a side of the construction: the rule, the ceiling, the share of points burned
against points earned. Here the word points at a remaining quantity that can run out and be
watched. A rule cannot go quiet and is not an object of this skill; the pool behind it can, and
is.

**Problem.** The object is not doing its work now.

**Warning.** The object works and is going to break: a pool draining, an error share climbing, a
filter that recalculates more slowly every week.

**Failure surface.** The level at which the object failed: entrance, condition, state, content,
channel, or system. It determines who owns the fix, which in practice determines how long the fix
takes.

**Duty slot.** A fixed time and a fixed walking order through the roster.

**Exposure.** People affected in the period multiplied by the value of the action at risk. It orders
ordinary faults against each other, and it is the only ordering that survives contact with a long
list. It says nothing about severity: a fault in a severity class outranks any exposure at all.

**Failure class.** One of six: silence, duplication, wrong audience, wrong content, late, disclosure
of data the recipient should not have seen. It answers what you fix.

**Severity class.** One of three faults that leave the marketing queue the moment you name them:
disclosure, wrongful permission, missed obligation. It answers who to tell immediately. Membership
does not depend on how many people the fault reached or on what the send was worth, and each class
has an owner outside marketing.

**Escalation route.** For one severity class: the role that owns it, the person currently in that
role, and how to reach them outside working hours. Write it before an incident, because inventing it
during one costs you the first hour.

**Failure window.** The period between the first failure and recovery. Inside it, the object's
numbers are not comparable with its norm, which is what makes the window worth establishing before
you read anything.

**Time to detect.** From the first failure to the moment somebody knew. The first failure comes from
the data, not from the moment of noticing.

**Detection route.** How you found out: duty, an alert, a metric, a complaint, a colleague, the
vendor. The mix of routes says more about the health of monitoring than any single incident does.

**Correction message.** A second message sent to affected people because of what the first one
contained.

**Recall.** Pulling a message that has already been shown, in channels that support it. Email does
not.

**Dead mechanic.** Silent for longer than its expected silence, with no seasonal explanation.

**Empty mechanic.** Sends, and produces no target action on its own control metric.

**Coverage hole.** People or a lifecycle stage no mechanic touches. Found from the base outward, not
from the list of mechanics.

**Version.** A record of a change to an object: what, when, who, why. Versions are what let the next
audit read a difference instead of deriving the same conclusions again.

**Owner, in two senses.** Here an owner is whoever the broken object goes to, chosen by where the
fault sits. In `crm-program-design` an owner is the person answerable for moving a number, chosen
by which lifecycle stage they hold. One person is often both, and the two roles still fail
differently: an object with no owner stays broken, a number with no owner stays flat.

**Review, in four senses.** Here it is the audit of a running object, which establishes whether
something that is live still works. In `scenario-map` it is the roster review, which gives every
live row a verdict and is the only place a row is retired. In `crm-program-design` it is the re-cut
of the goal and the resource behind it. In `email-copy` it is the review of a draft before the
send, the one sense whose object is not live yet; a blocking defect found there in a flow that is
already sending arrives here as an incident. An audit finding travels to the roster review rather
than acting on the composition of the program itself.
