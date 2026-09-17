# Changelog

This file records every release of Chappie. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and version numbers follow
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

All 35 skills share one version number. No skill has a version of its own.

## How the version number changes

- **Major.** A skill is renamed, merged or removed. Anything that calls it by its old name stops
  working, starting with commands such as `/chappie:deliverability`.
- **Minor.** A new skill, a new file in `references/`, or a new mechanic inside an existing skill.
- **Patch.** A correction inside a skill: a legal or channel rule updated to match its current
  source, or a step rewritten to read more clearly.

## [1.0.0] - 2026-09-17

First public release.

### Added

- 35 skills in six blocks:
  - **Program, data and segments:** `crm-program-design`, `scenario-map`, `segmentation`,
    `rfm-segments`, `list-building`, `martech-stack`
  - **Lifecycle mechanics:** `welcome-and-activation`, `triggered-messages`, `repeat-purchase`,
    `lapse-and-winback`, `offer-design`, `promo-calendar`, `loyalty-program-design`,
    `loyalty-program-launch`, `personalization`
  - **Channels:** `email-program`, `email-copy`, `email-design`, `deliverability`,
    `onsite-capture`, `push-notifications`, `in-product-messaging`, `chat-and-bots`,
    `messaging-channels`, `transactional-messaging`
  - **Orchestration and consent:** `contact-orchestration`, `consent-and-preferences`
  - **Measurement and customer voice:** `metric-definitions`, `experiments-and-holdouts`,
    `crm-reporting`, `program-audit-and-ops`, `voice-of-customer`
  - **B2B and subscription:** `b2b-lifecycle`, `b2b-retention`, `subscription-retention`
- The same six sections in every `SKILL.md`: When to use this, When to use something else,
  Reference map, Control metric, Legal regime this skill assumes, and Limits.
- 146 reference files in the skills' `references/` folders. The agent loads one only when the
  task needs it.
- Four ways to install: `npx skills` for any supported agent, the Claude Code plugin, a ZIP upload
  in the Claude app, or copying the folders by hand.
  [README.md](README.md#install) has the commands.
- [ROADMAP.md](ROADMAP.md): what version 1 leaves out, and why the library carries no market
  benchmarks.
- The [MIT license](LICENSE).

Version 2 takes two topics this release leaves out: calls and voice, and AI inside the program.
[ROADMAP.md](ROADMAP.md#not-in-version-1) gives the reason for each.

[1.0.0]: https://github.com/808enzo/chappie/releases/tag/v1.0.0
