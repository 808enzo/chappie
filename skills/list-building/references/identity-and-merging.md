---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Identity: keys, conflicts, and what a merge never pools

One person is in the base three times: once from the store card, once from the website account,
once from a support request. Every skill downstream reads that as three people. This mechanic
covers how you decide that two rows are one person, what happens when the two rows disagree, and
what a merge is not allowed to touch.

It is the least reversible operation in the skill. Whether you can unmerge at all is a property of
your system, so check it before you rely on it. Where you cannot, once two histories are one
history, nothing in the merged row says which event arrived from which side. Treat it as one way
until you have checked, and keep the snapshot in step 6 either way. Everything below follows from
that.

## Entry conditions

The base holds, or is about to hold, several records about one person: two systems, two channels,
offline and online, two brands under one owner.

## Exit conditions

A written merge rule: what identifies a person, what happens when fields conflict, what a merge
never pools, and how you review a wrong merge.

## Steps

**1. Sort attributes into two classes and merge on the first class only.** An attribute works as a
key when it is unique to one person and does not change over time.

- **Keys.** A confirmed address in a channel, a confirmed phone number, an internal account
  identifier, a contract or card number. What they share is that either the person or your own
  system confirmed them.
- **Hints.** A device, a browser marker, a matching name, a matching delivery address, two events
  close together in time. A hint raises the probability and never reaches uniqueness.

The difference is operational, not vocabulary. A key merges. A hint **links**: it marks two records
as probably the same person and waits for a key. A link comes apart on demand and a merge may not,
which is the entire reason for keeping two words.

**2. Write down the seniority of keys.** One order, used in every decision: internal account
identifier, then confirmed channel address, then contract or card number, then an unconfirmed
address. Seniority does no work at merge time. It does the work in step 4.

**3. Merge only on a matching key with no contradiction.** Two conditions, both required.

A matching key is necessary. The absence of a contradiction is what makes it sufficient. A
**contradiction** is two non-empty values of one field that cannot both belong to one person: two
different dates of birth, two different surnames against two different delivery addresses, two
active loyalty cards each carrying a balance.

Key matches and a contradiction exists: **the pair goes to manual review, not to a merge.** This is
where an automated merge fails silently, because it reports the same success either way.

**4. Resolve field conflicts by rule, not by recency.** Last write wins produces the wrong answer
precisely where the cost is highest. A conflict is not a contradiction. A contradiction has already
sent the pair to review under step 3, so what reaches this step is the remainder: an empty value
against a filled one, a short name against a full one, two spellings of one street. Resolve by the
kind of field:

- **Contact fields** (addresses, phone numbers) **accumulate rather than compete.** A record can
  carry several, each with its own status and its own provenance. Choosing one to send to is the
  sending system's job, and it happens per message, not once at merge time.
- **Provenance accumulates the same way: keep both, overwrite neither.** The merged record carries
  both intake points and both dates. Drop one and you have dropped the date the older basis is
  counted from, and nothing else in the record holds it.
- **Identifying fields** (name, date of birth) go to the value from the most senior key the record
  carries, not from the key that matched, since both records carry that one. On a tie, take the
  value the person entered themselves over the one a staff member entered for them. Where two
  values are incompatible rather than merely different, this rule does not apply: that is a
  contradiction, and the pair is in review, where the same order of seniority serves whoever
  decides.
- **Accumulating fields** (purchases, events, points) **sum**. Replacing them loses history, and
  that loss stands even where you review the merge itself.
- **State fields** (consents, subscriptions, restrictions) do not merge at all. See step 5.

**5. Name what a merge never pools.** Records about a person combine. Permissions do not. Four
things stay separate, and the fourth behaves differently from the other three:

- **Consent** lives with whoever the person gave it to, and for the purpose they gave it for.
  Merging two records does not carry a consent across and does not widen its purpose. The legal side
  belongs to `consent-and-preferences`; the requirement on the merge operation sits here because the
  merge is where it breaks.
- **A subscription to a specific list** is the same rule one level down. Somebody who read one brand
  does not become a subscriber to three when you join the bases of three brands. This damage
  surfaces as complaints rather than in a report, so look for it before it arrives that way.
- **Loyalty obligations** (balance, tier, expiry) combine under the rules of the program, which
  belong to `loyalty-program-design`. What belongs here is the prohibition on deciding it inside the
  merge.
- **An unsubscribe or a complaint transfers to the merged record, at the scope it was given.**
  Between two states of one scope the forbidding one wins. This is the single state field that does
  merge, and it merges in one direction only. Scope is what the person refused: one list, one
  sender, or everything you send. Losing the scope is the breach this rule exists to prevent, and
  widening it is the same mistake as pooling a subscription, running the other way: join three
  brands and one unsubscribe becomes three.

**6. Make the operation reviewable while that is still possible.** Before merging, store a snapshot
of both records and the reason for the decision: which key matched, what the contradiction check
returned, who reviewed it if anybody did. Where the system cannot separate the histories again, the
snapshot is the only route back, and it converts a wrong merge from a post mortem into a lookup.

**7. Run matching both at intake and in batch.** At intake, on every new contact, before it becomes
a separate record. In batch, across the whole base, on a schedule and always after a migration or a
consolidation. Intake matching alone leaves in place every duplicate that accumulated before you
turned it on. It stops new ones and clears none of the stock.

## Thresholds and timings

- **The automatic merge threshold is a matching key at zero contradictions.** One contradiction
  routes the pair to review. Do not tune this like a sensitivity setting: where the operation does
  not come apart again, a wrong merge costs more than waiting.
- **Batch matching runs once per planning period, and out of turn after any migration or
  consolidation.** Migrations are the largest single producer of duplicates, because two systems
  arrive each with their own keys.
- **The manual review queue has a deadline.** A pair that sits longer than one period either gets
  reviewed or takes the default, which is **do not merge**, and leaves the queue. Write that
  default onto the pair as you drop it. Where you do not, the next batch run finds the same pair
  and raises it again, and the queue refills itself faster than anybody empties it. A queue
  without a deadline grows
  until nobody reads it, at which point the real behavior of your system is already do not merge
  and nobody decided that.
- **The share of pairs routed to review is a working number, not a defect.** Watch its direction: if
  it climbs period over period while intake has not changed, a source changed, not the rule.

## Edge cases

- **One person, two addresses.** A personal one and a work one, both real. The keys match only if an
  internal identifier ties them. Without it these are two records, and linking them without merging
  is the correct outcome. The capture point still has to say which address it is asking for, which
  is `onsite-capture`.
- **One address, two people.** A shared household mailbox, a shared team inbox. The key matches and
  the people differ. The signal is a contradiction in identifying fields under a matching address.
  Always route to review: an automatic merge here fuses two people into one record.
- **An offline buyer arrives on the site for the first time.** Until they present a key these are
  two records: purchases with no address, visits with no name. Only something the person offers
  connects them, such as a card, a number, or an account login. A matching cart is a hint.
- **Two brands are being joined.** Beyond merging rows, there is the question of whose customer the
  person now is. The answer is both, and their subscriptions and consents stay separate under step
  5. The first message from a sender the person has not heard from before needs its own basis, not
  an inherited one.
- **A key changed.** Somebody changed an address or a number. Do not delete the old value: demote it
  to inactive with a date. Historical events still arrive against it, and dropping it breaks the
  history at the point where it changes.
- **The base is small.** Candidate pairs number in the dozens and manual review is cheaper than any
  rule. Write the rule anyway. The first migration will need it, and that is the moment when nobody
  has time to invent one.
- **A merge was wrong and the snapshot exists.** Restore both records, then work out which condition
  let it through: the key was not confirmed, or the contradiction check does not cover the field
  that differed. Restoring without that second half guarantees the same pair merges again.

## Failure modes

- **People receive the same thing twice.** The classic signal, and the latest one available: by the
  time it shows up in complaints the duplicates are numerous. The early version of the same signal
  is the gap between the number of records and the number of distinct keys in the base.
- **Neither an unmerge nor a snapshot exists.** Test this once, before the first batch run: ask
  somebody to reconstruct any past merge. If nobody can, the mechanic is running with no right to
  make a mistake, and that is a countdown rather than a stable state.
- **The review queue is not being reviewed.** The symptom is a queue that only grows. The routing
  threshold is producing more work than there are people, so the system's actual behavior is already
  never merge.
- **Somebody has a subscription they never signed up for.** A direct breach of step 5, and it
  reaches you as a complaint rather than as a report. Check it before that: take the records merged
  during a period and compare the subscriptions on the merged record against those on the two
  originals.
- **Matching runs only at intake.** The duplicate share does not fall even though the rule has been
  running for months. The base holds every duplicate created before the rule existed, and it will
  hold them until a batch run.
- **The rule merges on hints.** The symptom is merged records whose fields contradict each other in
  ways no single person could produce, such as two dates of birth on one row. By the time you see
  it, the merges behind it are already done.
