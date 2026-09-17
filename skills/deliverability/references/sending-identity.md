---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# The sending identity: who the provider thinks you are

The unit here is **the sending identity**: a domain or subdomain, the signatures that prove mail
under it is yours, the Return-Path it answers on, and the IP or pool it leaves through. A provider
does not form an opinion about your company. It forms one about an identity, and it forms a
separate one for each provider you send to.

This file covers building an identity and auditing one. It does not send anything: the first send
is authorized by `warmup-and-volume.md`.

## Entry conditions

You own a domain rather than sending from a free mailbox, you can edit its DNS, and you have a
sending platform. You know, or are about to find out, which systems send mail under your name.

## Exit conditions

A written register of sending identities: for each one the domain or subdomain, the class of mail
it carries, its signatures, its Return-Path, its IP or pool, the provider postmaster tools it is
enrolled in, and one named owner. Authentication passes end to end on a message you have received
and inspected. Nothing has been sent in volume yet.

## Steps

**1. List every system that sends under your domain, not every campaign.** The sending platform,
the order system, the CRM, the helpdesk, the delivery contractor, the recruiting tool, ordinary
corporate mail. Each of them will one day put your domain in a From header, and each will fall
under your DMARC policy. The system nobody remembered is the most common reason a strict
policy gets rolled back a week after it is set.

**2. Separate streams into identities by the cost of failure, not by convenience.** A message
somebody needs in order to receive the service must not depend on a reputation that a promotion can
damage. The minimum split is two identities, service and marketing. Split with a subdomain always,
and with a separate IP only where volume justifies it (step 6).

**3. Set up authentication, then verify the result rather than the record.** Three records, each
answering its own question: SPF says which servers may send, DKIM says the message was not altered
in transit and who signed it, DMARC says what a provider should do when the first two do not line
up. What you check is the authentication result in a message you received, not the configuration
screen that produced it.

**4. Check alignment separately, because this is the step that fails.** The domain in the From
header has to match the domain that signed the message or the domain in the Return-Path. Sending
through a platform puts the platform's domain in the Return-Path by default, and then SPF passes
while alignment does not. The fix is your own subdomain in the Return-Path. Providers state the
requirement as alignment with SPF or DKIM, so passing one of the two is enough, and passing neither
means DMARC fails whatever the individual records say.

**5. Build the exit route the way providers require it, not only the way the law does.** A
one-click unsubscribe header plus a visible unsubscribe link in the body. This is a provider
requirement, and in both regimes named in `SKILL.md` its deadline for honoring a request is the
shorter one, which makes the provider rule the binding one. The legal side is in `SKILL.md`; the
operational consequence is that your suppression list has to refresh faster than the shortest
applicable window.

**6. Choose a shared or a dedicated IP deliberately.** A dedicated IP means you build a reputation
from nothing, which is an advantage only at a volume large enough that the provider sees you
regularly and steadily. Below that volume a dedicated IP is worse than a shared one: infrequent
sending from a single address looks stranger than a steady flow from a large platform. Derive the
volume where that flips from your own sending, and revisit it when your rhythm changes.

**7. Enroll in the postmaster tools of every provider with real weight in your base.** Each tool
reports only its own domains, and the picture differs between them, which is the raw material of
the control metric. Enrollment needs proof that you own the domain, through a DNS record or a file
the provider names.
Some providers offer no tool at all; say that out loud in reporting rather than treating missing
data as a healthy signal.

**8. Turn on complaint feedback where the provider offers it.** A complaint that never reaches your
system never becomes a suppression, so the person receives the next message and complains again.
Where a feedback loop is tied to your DKIM signing domain, adding a new signing domain later means
enrolling it too.

**9. Write the register and name an owner per identity.** Domain, class of mail, signatures,
Return-Path, IP, postmaster enrollment, owner. Without a named owner, one day somebody edits DNS
without knowing what they are breaking, and the change surfaces weeks later as a fall nobody can
explain.

## Thresholds and timings

Every figure below is a provider or protocol requirement rather than a norm of practice. Each is
dictated by the party named beside it, each moves when that party moves it, and the primary source
and the date it was opened are in `SKILL.md`.

| Quantity | Value | Whose, and where it stops |
|---|---|---|
| Bulk sender threshold | more than 5,000 messages a day to that provider's domains | Google and Microsoft; Yahoo publishes no figure |
| Authentication, all senders | SPF or DKIM | Google, Yahoo |
| Authentication, bulk senders | SPF and DKIM and DMARC at a policy of at least none | Google, Yahoo, Microsoft |
| Alignment | From domain aligned with the SPF or the DKIM domain | Google, Yahoo, Microsoft; Yahoo accepts relaxed alignment |
| DKIM key length | 1024 bits or longer | Google for personal Gmail accounts, Yahoo |
| DNS lookups inside an SPF record | at most 10 | a limit of the protocol itself; exceeding it breaks the check |
| Forward and reverse DNS | required, and the sending IP must match the host named in the PTR record | Google, Yahoo |
| Transport | TLS | Google |
| Message format | RFC 5322; Yahoo adds RFC 5321 | Google, Yahoo |
| One-click unsubscribe | required on marketing and subscribed messages | Google and Yahoo, for bulk senders only |
| Spam complaint rate | below 0.30%, with 0.10% as the level to hold | Google; Yahoo requires below 0.3%, computed on mail delivered to the inbox |

**A number that does not exist: an acceptable bounce rate.** No provider publishes one. Figures of
that shape come from individual sending platforms measuring their own customers. Set your own
threshold from your own history and read it per provider, which is `placement-recovery.md`.

## Edge cases

- **The platform's domain sits in your Return-Path.** SPF passes on the platform's domain and
  alignment fails on yours. Recipients may also see the message marked as sent through another
  domain. Nothing looks wrong until volume rises.
- **One domain, several sending platforms.** DKIM is fine: each platform signs with its own
  selector and they do not collide. SPF is not: a domain must publish exactly **one** SPF record
  listing every source. Two records beginning `v=spf1` break the check entirely.
- **The SPF record grew past the lookup limit.** Every `include:` costs lookups, and adding one
  more platform silently pushes the record over the limit, at which point the check fails for
  everybody. Count the lookups when you add a sender, not when mail stops.
- **A strict DMARC policy with forwarding in play.** Forwarding breaks alignment, so a policy
  stricter than monitoring starts discarding legitimate mail. Move past monitoring only after the
  reports have shown you the full list of senders, which is the same list as step 1 and is longer
  than it.
- **The company owns domains it does not send from.** Configure them too. An unused domain with no
  policy is a ready-made tool for somebody to impersonate you, and the damage lands on the brand
  and eventually on the domains you do send from.
- **A brand logo beside the message.** The mechanism sits on top of DMARC, requires a policy
  stricter than monitoring, and is honored by some providers and ignored by others. It affects
  recognition rather than acceptance, so treat it as a step after the basics rather than part of
  them.
- **A service message with a promotional block in it.** It breaks the separation the two identities
  exist for, and in several regimes it costs the message its exemption. What must be in a service
  message is `transactional-messaging`; the identity rule is here.
- **Mail sent from a free mailbox domain.** It cannot be aligned or authenticated as yours, and
  bulk mail from one is refused by providers as a matter of course. Move to your own domain before
  anything else in this file applies.

## Failure modes

**Alignment fails while SPF and DKIM both pass.** The sign: recipients see the message attributed
to another domain, DMARC reports show failures you cannot place, and complaint rates drift upward
with no change in content. It is visible only in the authentication result of a received message,
which is why step 3 asks for one.

**The policy was tightened and legitimate mail vanished.** The sign: the complaints arrive from
inside the company rather than from a provider, and they are about invoices and password resets.
The cause is always a system missed in step 1. Roll the policy back to monitoring, finish reading
the reports, then tighten again.

**Nobody owns DNS.** The sign: a record was changed, nobody remembers when, and the previous value
was not kept. This one is invisible until something else goes wrong, and then it removes your
ability to date the change against the fall.

**Every stream shares one identity.** The sign: an order confirmation and a promotion cannot be
told apart by the provider, so a bad promotional week degrades delivery of messages people are
waiting for. It is cheap to prevent and expensive to fix afterwards, because separating identities
later means warming the new one from nothing.
