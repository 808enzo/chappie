## Installation and docs

**Issue:** <!-- "Closes #123", or "none" -->

**What changes:**

- [ ] Installation instructions
- [ ] `README.md`, `ROADMAP.md`, `CONTRIBUTING.md` or `AGENTS.md`
- [ ] The plugin manifests in `.claude-plugin/`
- [ ] `scripts/validate` or the workflow
- [ ] The issue forms, the discussion form or the pull request templates

## Why

<!-- What was wrong, out of date or missing. -->

## How you tested it

<!-- For installation: the method, the agent and its version, your operating system, and the commands
you ran in an empty folder. For the validator: a full run before and after the change. Otherwise
write "not needed". -->

## Checks

- [ ] If I changed installation steps, I ran them start to finish in an empty folder.
- [ ] The anchors other files link to still work: `README.md#install`, `README.md#skills`,
      `ROADMAP.md#on-numbers`, `ROADMAP.md#not-in-version-1`.
- [ ] If I changed a manifest, `claude plugin validate --strict .` passes, and
      `claude plugin validate .claude-plugin/plugin.json` shows no warning beyond the one `AGENTS.md`
      names.
- [ ] If I changed a Limits block in `AGENTS.md` or in `scripts/validate`, I changed it in the other file
      too.
- [ ] I ran the style pass from `AGENTS.md` on the text I changed.
- [ ] `python scripts/validate` shows no new errors.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
