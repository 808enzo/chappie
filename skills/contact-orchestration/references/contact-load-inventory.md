---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# What one person receives

The first job is not the cap. It is the measurement. A cap set before the measurement either
suppresses nothing, because it sits above what anyone sends, or cuts into working programs,
because it sits below a flow nobody counted.

The unit of this whole skill appears here: one person over a period. Everything downstream reads
wrong if you keep counting sends.

## Entry conditions

Messages reach a person from more than one source: campaigns plus automated flows, two brands on
a shared base, or a product that sends its own notifications. Or a signal arrived: unsubscribes
and complaints are climbing, someone said you send too much, or a new channel is about to launch.

## Exit conditions

- Every sending stream is in a register, and each one has a named owner.
- Load per person per period is calculated across channels and in total.
- You have the distribution, not the average, and you know how the top ten percent differ from
  the median.
- You know how many systems can physically send a message, and whether they can see each other.

## Steps

**1. Build the register of sending streams.** The unit is not the channel. It is any source that
can put a message in front of a person: the sending platform, the product with its own
notifications, the system of record that emits service messages, support, a neighboring brand on
the shared base, a partner send. For each one record the owner, the class (service, automated,
campaign), the channel, the expected volume, and who has the right to launch it.

**2. Count the sending systems.** If more than one system sends and they cannot see each other,
no total cap exists, because nothing can check it and nothing can enforce it. You can deliver
this on day one, before any distribution exists, and it converts an argument about the right
frequency into an engineering question about where sending converges.

**3. Reduce the send log to load per person per period.** For a rolling 7 and 30 days, count how
many messages each person received, by channel and in total. The unit is the person, not the send
and not the campaign. Build the distribution of step 4 on messaged people, those with a load of at
least one, and publish the count of reachable people at zero beside it: a base where most people
receive nothing otherwise pulls every percentile down, and where nine people in ten received
nothing the 90th percentile is zero. From here on, keep the send log as the contact log: one row per
person per message, with the channel, the class, the stream and the state (held by the policy,
reserved, in flight, delivered, unknown), fed by every system that sends a message or shows one to a
known person. The cap, pitch deduplication and the control metric all read this one log.

**4. Build the distribution, not the average.** Median, 90th percentile, 99th percentile. Load has
a long tail, and the damage lives in the tail. The people at the top are those who fell into
several streams at once, which makes them your most active buyers rather than a marginal group.

**5. Walk the path as a mystery shopper.** Create a fresh profile and go through signup, browsing,
an abandoned cart, a purchase and a return. Record a timing chart: what arrived, how long after,
following which action, in which channel. Compare against the register. This step catches what the
log does not hold, which is sends from systems that never made it into the report and flows nobody
remembers launching.

**6. Name where the load comes from.** Who asks for sends, and who is able to refuse. The usual
construction of an overloaded base is organizational rather than technical: messages get prepared
on request from internal departments, each requester sees only their own, and nobody reads the
total.

**7. Join load to outcome at the person level.** Split the reachable base into load buckets for
the period, then compute per bucket: revenue per person in the bucket, reachability loss (unsubscribes,
complaints, notifications turned off, hard bounces), and the share that goes silent in the
following window. Compute the loss the way `SKILL.md` defines it: people addressed in the
denominator, one loss per person per channel, `not defined` where a bucket addressed nobody in
that channel. Otherwise the buckets compare to neither each other nor the program total.

## Thresholds and timings

- Load windows: rolling 7 and 30 days. The monthly window is what you decide on; the weekly window
  catches spikes the monthly one averages away.
- The observation period for joining load to outcome runs no shorter than the category's median
  interpurchase interval. Below that, unsubscribes have already moved and revenue has not.
- Percentiles: 50, 90, 99. Read the tail at the 99th, make the decision at the 90th.
- Repeat the mystery shopper walk after every new flow goes live.
- The two windows and the three percentiles are starting points we chose, not values read out of
  anyone's data. Keep them until your own history contradicts them, then write down what replaced
  them and why.

## Edge cases

- **The log holds sends for less time than the window you need.** Start counting forward from
  today and postpone the cap decision by one period. Do not reconstruct the past from campaign
  reports: they count sends, not people.
- **One person lives in several unmerged profiles.** Their load is understated, so mark the figure
  as a floor rather than a measurement. Merging records belongs to `list-building`.
- **Several brands on one base.** The unit stays the person, not the subscription to a brand. The
  recipient does not separate senders inside one company, and the mailbox provider separates them
  even less.
- **Anonymous channels.** Web push without a profile, or an on site chat message, gets its own
  line and does not attach to a person until an identifier exists.
- **B2B.** Count load twice, on the person and on the company. Four emails to four people in one
  buying group is four touches on people and one touch on the account, and the second is what
  comes up in the next call.

## Failure modes

- **You counted sends instead of people.** Then every added send improves the picture, because a
  send costs almost nothing and channel revenue is read as a total. The symptom: channel revenue
  rises while revenue per reachable person stays flat or falls.
- **You read the correlation between load and revenue as causation.** It shows up almost every
  time, because active people qualify for more flows: they take more actions, and actions start
  flows. The symptom: load is explained by engagement rather than by the schedule. Compare inside
  one engagement tier, and confirm with a randomized check, whose design belongs to
  `experiments-and-holdouts`.
- **The inventory ran once.** A quarter later the register no longer matches reality. The symptom:
  the mystery shopper receives a message that is not in the register.
