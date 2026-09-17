## Rule update

**Skill:** <!-- slug; list every skill you changed -->

**Issue:** <!-- "Closes #123", or "none" -->

## The rule

**As the skill says it now:**
<!-- The sentence, with its file and section. -->

**What the source says today:**
<!-- Quote the current wording, with the section or article number. -->

**Primary source:**
<!-- The body, the document, the section and the URL. The law itself, the regulator's page or the
platform's own documentation. A blog post or a vendor summary doesn't count. -->

**Date you opened it:** <!-- YYYY-MM-DD -->

## Where else the rule appears

<!-- Search for the source and the rule in every skill, for example:
grep -rn "the-source-domain" skills/
List each file you changed, or write "only here". -->

## Checks

- [ ] The Sources block carries the new URL and the date I opened it, in ISO format.
- [ ] Every step that followed from the old wording changed with it: timings, consent steps, exemptions.
- [ ] The rule still ends with `Who this does not bind:`, and that line matches the new wording.
- [ ] A skill that quotes the same rule now matches too, or points to the skill that keeps the source.
- [ ] I ran the style pass from `AGENTS.md` on the sentences I changed.
- [ ] `python scripts/validate <slug>` shows no new errors, and I read every warning.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
