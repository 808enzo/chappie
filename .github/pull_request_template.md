<!--
Pick the template for your change: add `?template=` and one of these file names to the end of this
page's address, then press Enter. If the address already contains a `?`, add `&template=` instead.

  rule-update.md       a legal or channel rule no longer matches its source
  skill-fix.md         a skill gets something wrong
  install-and-docs.md  installation, the root files, the validator or the workflow
  new-mechanic.md      a new section or a new file in references/ in an existing skill
  new-skill.md         a new skill, after the maintainer accepts the request in an issue

If you would rather not reload, fill in the form below. CONTRIBUTING.md describes each type.
-->

## What changes

<!-- The skill or file, and the change in one or two sentences. -->

## Why

<!-- What was wrong or missing. Link the issue if there is one: "Closes #123". -->

## Type

- [ ] Rule update
- [ ] Skill fix
- [ ] Installation and docs
- [ ] New mechanic
- [ ] New skill

## Checks

- [ ] I ran the three passes in `AGENTS.md` (market neutrality, evidence, style) on every file I changed.
- [ ] I ran `python scripts/validate` and read every error and warning.
- [ ] The change adds no market benchmark and no number offered as proof that a mechanic works.
- [ ] Nothing here identifies a customer, an employee or a company that hasn't agreed to be named.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
