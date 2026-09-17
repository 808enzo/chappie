---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Enrollment and identification

Enrollment is the machinery that turns an anonymous transaction into an attributable one. It is
the part of the program the customer meets in person, it happens in seconds at a counter or a
checkout page, and almost all of it is decided by people who are not in the marketing team.

The distinction that organizes this whole mechanic: **members are not the point, identified
transactions are.** A member who never gets recognized at the moment of purchase costs you the
discount and returns nothing.

## Entry conditions

- The program's rules exist and you have written the staff-facing material from them.
- You know which system holds the member record and which identifier is canonical.
- The processing answers fast enough at the till to be part of a transaction rather than an
  interruption to it.

## Exit conditions

Every place a transaction can happen has a defined enrollment path or a stated reason for not
having one, the ask fits inside the transaction, staff have a target expressed in identified
transactions, and you measure the quality of what arrives separately from the volume.

## Sequence

**1. Inventory the entry points.** List every place a transaction can start or finish: each
checkout type, the site, the app, the call center, the courier hand-off, self-service, orders that
arrive through a third-party platform. Against each, mark three things: can someone join here, can
an existing member be recognized here, is the answer no to both.

The rows where the answer is no to both are the program's ceiling, and they belong next to the
control metric rather than inside it: they sit in its denominator and can never reach its
numerator. Where such a row carries a large share of transactions, work on the reward moves the
metric only as far as the remaining rows allow, and a shift of trade between rows moves the metric
on its own. Count those transactions and keep the count visible.

**2. Count the steps at each entry point, then cut them.** Between "I'll join" and "you are in"
there should be one identifier and, at most, a name. Everything else (date of birth, preferences,
a second contact channel) is collected later, from someone you can already reach, by people who are
not standing between a customer and a queue.

Every additional field at the counter costs a share of enrollments. The cost is measurable: run
the short and the long ask in comparable locations and compare identified transactions, not forms
completed. Long asks produce more complete records of fewer people. The argument runs toward the
short ask: the missing fields can be collected afterward and the missing people cannot. It stays an
argument until you run the comparison, which tells you what the extra field costs in your own
category.

**3. Separate the identifier from the carrier.** The identifier is the member number, and it
survives every change of carrier: plastic to virtual, virtual to app, app to a phone number read
out at the till. The carrier is whatever the person has to hand at the moment of payment. Deciding
this explicitly is what makes it possible to change carriers later without reissuing anyone's
membership, and reissuing membership is where migrations go wrong.

Where the program is offered on a phone, a wallet pass is the cheapest carrier: it is already
installed, it survives the customer forgetting to install anything else, and it carries the
balance without an app. What it cannot do is show purchase history, so it complements an account
rather than replacing one.

**4. Decide what the member gets when they join, and what they get across the first purchases.**
A single welcome benefit is spent on the purchase already in progress, which is the purchase you
had anyway. Spreading the same value across the first few purchases buys a second visit instead,
and gives you a reason to make contact between them. The value itself belongs to
`loyalty-program-design`; what belongs here is its distribution over the first purchases, because
that is a property of enrollment rather than of the reward. The messages that carry it are not: a
new member is inside the welcome series, `welcome-and-activation` owns its touches and spacing, and
this step hands that skill the occasions rather than sending anything of its own.

**5. Make the staff side workable.** Everyone who faces a customer gets: one sentence explaining
the program, a script for asking, an answer to the two objections they hear at the counter, and a
channel where their question gets a same-day answer. Managers get the reasoning as well as the
target: the connection between identification and their own numbers is not obvious, and staff who
believe the discount comes out of their revenue will decline to mention it.

Set the target on identified transactions. Never on cards issued.

**6. Measure the quality of what arrives, alongside the volume.** Contact validity is its own
number: the share of records where at least one contact is deliverable, and, separately, the share
with a deliverable email address. The second cannot come out above the first, since an email counts
in both. Read the size of the gap: it is a fact about your collection method rather than about your
customers, because an address dictated aloud at a counter is harder to record correctly than a
number typed into a keypad.

Watch for the fingerprints of records created to hit a target: a repeated impossible phone number,
addresses built from the location name, a cluster of accounts with exactly one purchase. These are
found by looking at the top of a sorted list by hand, weekly, not by building a model.

**7. Track enrollment and activation as two states.** Enrolled means you can attach purchases.
Activated means a contact channel is confirmed and you can reach them. Most programs report the
first and plan as though they had the second. The share of members who enrolled and never
activated is its own number with its own remedy, and the remedy is a campaign rather than a fix
to the till.

## Thresholds and timings

- **The ask fits inside the transaction: one identifier, optionally a name.** Anything else is a
  later conversation. The binding constraint is the queue, so this is a threshold for the counter,
  the call center and the courier hand-off. On the site and in the app there is no queue and the
  form is `onsite-capture`'s object; what carries over there is the order of fields, not the count.
- **Staff targets move in steps, and every step stays inside the cluster.** Set the first target
  at a location's own current average, so that people already doing the job honestly are not
  punished on day one; then move toward the level the leading locations *of that cluster* reach. A
  network-wide best is the wrong destination for a location whose ceiling is structurally lower: it
  is the contest below, rewritten as a target. The leading fifth is a starting choice, not a norm:
  a cluster of six locations has no fifth, so pick the rung from the shape of your own distribution
  and write down when you will revisit it.
- **Compare locations inside clusters of similar identification levels, not by geography.** A store
  on a busy thoroughfare and a neighborhood store have structurally different ceilings, and a
  contest between them is decided before it starts.
- **Fix the cluster boundaries for a named term, and recompute them on a written date.** The
  cluster is drawn on the same number the target moves, so continuous recomputation promotes every
  location that succeeds into a harder cluster and makes sitting just under a boundary the
  profitable move. Announce the term, keep the boundaries still inside it, and recompute with the
  target cycle rather than with every reading.
- **Read enrollment by entry point weekly during rollout, monthly afterward.** A single flat entry
  point is invisible in a total that is rising.
- **Measure validity on a real send, not on a format check.** A well-formed address that bounces
  is an invalid address.

## Edge cases

- **Enrolled but never activated.** You have attribution and no channel. Count it separately, and
  treat collecting the channel as its own piece of work with its own offer.
- **Attaching a purchase after the fact.** Without an identifier at the moment of sale it cannot
  be done in the general case. A "scan your receipt" path exists, but it is a separate build with
  its own authenticity checks, not a softening of the rule.
- **The customer wants the discount without the identification.** A discount available without
  being recognized spends the margin the public half was meant to spend and returns none of what it
  was meant to buy. Give it anyway if you choose, but make that call as a pricing decision, with
  whoever owns pricing.
- **Third-party platforms where soliciting is prohibited.** Platforms commonly forbid diverting
  their customers to your own channel, and each one words it differently; this library has not
  opened a primary address for any of them, so the wording of the platform you sell on is the only
  thing that answers. What you put in the parcel is the entry point most likely to stay inside
  those rules, and the platform's terms decide whether it does, so read them, with a date, before
  the insert is printed.
- **One card, several people.** A household card is a shared carrier in the sense `offer-design`
  gives the word, and it produces a purchase history that belongs to nobody in particular. The
  program cannot fix this; what it must not do is build decisions on an attribute inferred from
  that history. The handling of the resulting attribute belongs to `segmentation`.
- **Staff enrolling on the customer's behalf.** Some of it is help and some of it is fabrication,
  and the two look identical in a member count. They separate in the data described in step 6:
  repeated impossible numbers, addresses built from the location name, a cluster of accounts
  carrying exactly one purchase.
- **A minor at the till.** Where the program collects personal data, the age at which someone can
  consent is set by law and differs by jurisdiction. The enrollment path either handles it or
  states that it does not; `consent-and-preferences` owns the rule.

## Failure modes

- **The target was set on cards issued.** The predictable result is a new card per receipt, a base
  full of single-purchase accounts, a member count that looks excellent, and identification worth
  nothing. This is the most expensive failure in the mechanic, because it corrupts the exact asset
  the program was launched to build, and the corruption is not reversible by deleting the records:
  the real customers behind those receipts are still anonymous.
- **Staff believe the program costs them money.** Penetration stays flat in a subset of locations
  while the terms are identical everywhere, which reads as a customer problem and is not one. This
  is found by watching a checkout for a day and comparing the share of customers asked while
  someone is watching against the share asked when nobody is. A survey will not find it.
- **The ask lengthens over time.** Each department adds one field. Identification declines while
  the program's terms have not changed, and nobody attributes the decline to the form because no
  single field was the cause.
- **The entry point exists where marketing sits.** A polished enrollment flow on the site, nothing
  at the counter where most transactions happen.
- **A contest that compares incomparable locations.** Participation collapses after the first
  round, and the tool is spent: a second attempt at a contest is harder than the first.
- **Enrollment is reported and activation is not.** Campaign plans are built on a reachable
  audience that turns out to be a fraction of the member count, and the shortfall is discovered
  when the first campaign underdelivers.
