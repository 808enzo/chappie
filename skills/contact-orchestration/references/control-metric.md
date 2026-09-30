---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Control metric: how to count reachability loss

`SKILL.md` defines the rate: loss events over people addressed, per planning period, and who sits in the
numerator and the denominator. It says that an empty denominator leaves the rate undefined, why the person
and the period rather than channel revenue or per campaign unsubscribes, what the rate is read against and
why the two run on different populations, and what to answer when someone asks what is normal. This file
holds three more rules to settle before the count means anything: which refusals are not loss events, the
rate per channel and in total, and one loss per person per channel.

## Three more rules for the count

- **A refusal that is a property of the sending origin is not a loss event.** When a mailbox
  provider blocks a flow, refusals arrive for every address at that provider at once, live ones
  included, and the platform files them as bounces. Count them as losses and you get a spike this
  metric reads as contact load and answers by cutting frequency, which does nothing for an incident
  that belongs to `deliverability`. That skill sets the class of an unreachable address; only the
  classes that are properties of the address count here, and the block class is excluded until the
  incident closes and then reassessed. Texts refused as unregistered or filtered traffic are the
  same case in `messaging-channels`: a property of the origin, never a loss event.
- **Per channel first, then total.** Losing email is not losing the person. Compute the rate per
  channel against the people you addressed in that channel, then compute a separate total rate
  whose numerator is people who finished the period reachable in no channel at all. Someone whose
  email hard bounced while push still works belongs in the first number and stays out of the
  second.
- **One person, one loss per channel.** An unsubscribe followed by a complaint in the same channel
  in the same period is one channel lost, not two. Deduplicate by person and channel before you
  divide, or the rate counts reasons instead of people.
