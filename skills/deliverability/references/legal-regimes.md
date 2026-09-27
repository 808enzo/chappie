---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Legal regimes: the envelope, quoted and dated

`SKILL.md` names the regimes and what this skill leaves to you. This file states each rule, ends it with
the people it does not bind, and lists every source it rests on at the end. This is not legal advice.

## The rules

- **United States.** Header information in From, To, Reply-To and the routing must be accurate, the
  subject line must reflect the content, the commercial nature of the message must be disclosed
  clearly and conspicuously, and the message must carry a valid physical postal address. The
  message must explain how to opt out; the opt-out mechanism must be able to process requests for
  at least thirty days after the message goes out, and an opt-out is honored within ten business
  days. Hiring somebody to run your email does not move the legal responsibility onto them. The
  CAN-SPAM Act sets all of this.
  **Who this does not bind:** the narrow categories of transactional and relationship message,
  which sit outside most of the requirements.
- **United Kingdom.** You must not disguise or hide your identity in a marketing message, and you
  must give a valid contact address for opting out. PECR regulations 22 and 23 apply both rules to
  individual and corporate subscribers, and whether the message was asked for makes no difference.
  **Who this does not bind:** these are not the consent rules. Whether you may send at all, and to
  whom, is a separate question that belongs to `consent-and-preferences`.
- **Google, for personal Gmail accounts.** Every sender needs SPF or DKIM, valid forward and
  reverse DNS records, TLS, messages formatted to RFC 5322, and spam rates in Postmaster Tools
  below 0.30%. A sender of more than 5,000 messages a day to Gmail also needs SPF and DKIM and
  DMARC with a policy of at least none, the From domain aligned with either the SPF or the DKIM
  domain, and one-click unsubscribe on marketing and subscribed messages. Google names 0.10% as
  the level to hold and 0.30% as the level never to reach.
  **Who this does not bind:** this is a platform rule enforced by a company, not a statute, and it
  covers mail to personal Gmail accounts.
- **Yahoo.** Every sender needs SPF or DKIM, valid forward and reverse DNS, compliance with RFC
  5321 and RFC 5322, and a spam rate below 0.3%. A bulk sender needs SPF and DKIM, a DMARC policy
  of at least none that passes, From alignment with SPF or DKIM, a list-unsubscribe header
  supporting one click, a visible unsubscribe link in the body, and unsubscribes honored within two
  days. Yahoo computes the spam rate on mail delivered to the inbox, which is not how your own
  system computes it.
  **Who this does not bind:** a platform rule, and Yahoo publishes no volume figure defining a bulk
  sender.
- **Microsoft, for consumer Outlook.com domains.** Since 5 May 2025, a domain sending more than
  5,000 messages a day must pass SPF and DKIM and publish DMARC at a policy of at least none,
  aligned with SPF or DKIM. Messages that fail are rejected with `550 5.7.515`.
  **Who this does not bind:** a platform rule, scoped to the consumer domains Outlook.com, Hotmail
  and Live.
- **One-click unsubscribe, RFC 8058.** The mechanism is a `List-Unsubscribe-Post:
  List-Unsubscribe=One-Click` header alongside a `List-Unsubscribe` header carrying an HTTPS
  address, both covered by the DKIM signature. The address must carry enough information for the
  unsubscribe to complete automatically, and the recipient is asked for no further confirmation.
  **Who this does not bind:** the specification describes a mechanism and imposes no obligation. It
  is the platform rules above that make it mandatory.
- **Public blocklists.** These are private organizations, and their operators publish their own
  removal rules. For the IP list, only the network or hosting company responsible for the address
  can request removal, so an ordinary sender goes through their provider. For the domain list, most
  listings expire on their own once the behavior stops, and a removal is requested through the
  operator's own checker; an approved request is processed within minutes, though local systems can
  lag up to a day. No listing removal ever costs money, and an offer to remove one for a fee is a
  fraud.
  **Who this does not bind:** a blocklist decision is not a legal finding, and nothing obliges a
  mailbox provider to use any particular list.

## Where the law and the platforms disagree

**Where the law and the platforms disagree, the shortest window wins.** An opt-out has ten business
days under the United States statute and two days under one provider's rules. Refresh your
suppression list faster than the shortest window that applies to you, or you will comply with the
law and break a provider requirement at the same time, losing reputation while looking compliant.

## Sources

**Sources, each opened 2026-09-12.**

- FTC, *CAN-SPAM Act: A Compliance Guide for Business*:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- ICO, *How do we comply with the PECR electronic mail marketing rules?* (regulations 22 and 23):
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/
- Google, *Email sender guidelines*: https://support.google.com/a/answer/81126
- Google, *Postmaster Tools dashboards*: https://support.google.com/a/answer/14668346
- Yahoo, *Sender Requirements and Recommendations*: https://senders.yahooinc.com/best-practices/
- Microsoft, Outlook Postmaster, *Requirements for High-Volume Senders*:
  https://sendersupport.olc.protection.outlook.com/pm/policies.aspx
- IETF, RFC 8058, *Signaling One-Click Functionality for List Email Headers*:
  https://www.rfc-editor.org/rfc/rfc8058.txt
- Spamhaus, *Spamhaus Blocklist (SBL)*, listing removal:
  https://www.spamhaus.org/blocklists/spamhaus-blocklist/
- Spamhaus, *Domain Blocklist (DBL)*, removal:
  https://www.spamhaus.org/blocklists/domain-blocklist/
