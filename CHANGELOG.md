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

## [1.1.0] - Unreleased

Each skill now takes less of the agent's context: a short description in the list the agent picks
skills from, the rules that must hold at the top, and a body short enough to come back whole after
a long session is compacted. No skill is renamed, so commands such as `/chappie:deliverability`
keep working.

### Added

- A program context file, in beta. Every skill reads `.agents/chappie-context.md` in your project
  before its first step, takes what it records as given, and asks only for what it lacks.
  [README.md](README.md#program-context-beta) has the template and what never goes in the file.
- `references/control-metric.md` in every skill, and `references/legal-regimes.md` in every skill
  that quotes a legal rule.
- Worked examples on made-up numbers in five reference files, for `metric-definitions`,
  `experiments-and-holdouts`, `lapse-and-winback`, `rfm-segments` and `contact-orchestration`:
  the input fields, sample rows, the steps in order, and what the procedure returns when there is
  too little data.
- Advice for Claude Code with a 200K context window, where the agent sees skill names without
  descriptions. [README.md](README.md#with-npx-skills-for-any-agent) has the setting.

### Changed

- `Limits` is now the first section of every `SKILL.md`, right after the opening.
- Every description is 350 characters or less, in three parts: what the skill decides, when to
  use it, and which neighbor takes a nearby question.
- Quoted legal rules, the people each rule does not bind and the source addresses moved from
  `SKILL.md` to `references/legal-regimes.md`. Details of the control metric moved to
  `references/control-metric.md`. `SKILL.md` keeps the metric's definition, the answer to "what is
  normal", and why this metric and not a nearby one.
- A skill hands part of a question to a neighbor in one form: what it settled, the question it
  passes on, and whether the neighbor is installed. If the neighbor is not installed, the skill
  leaves that part unanswered and gives the command that installs it. Each row in the neighbor
  tables now routes a question the skill's own work leads to, one that users bring to the wrong
  skill, or a question that belongs to one of the skills most others hand work to.
- The first block of `Limits` also rules out quoting a figure that circulates as a norm, even to
  reject it.

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

[1.1.0]: https://github.com/808enzo/chappie/releases/tag/v1.1.0
[1.0.0]: https://github.com/808enzo/chappie/releases/tag/v1.0.0
