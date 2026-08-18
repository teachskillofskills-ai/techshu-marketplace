# TechShu Plugin Marketplace

Internal Claude Code / Cowork plugin marketplace for Indus Net TechShu Digital Pvt. Ltd.

## What is here

| Plugin | Purpose |
| --- | --- |
| `techshu-brand` | TechShu house voice, delivery SOPs, compliance guardrails |
| `techshu-standard` | Bundle - installs the standard TechShu toolchain in one step |

## Install

```
/plugin marketplace add teachskillofskills-ai/techshu-marketplace
/plugin install techshu-standard@techshu
```

If the install summary says `Run /reload-plugins to activate.`, run that.

For automatic setup across the team, see [docs/team-setup.md](docs/team-setup.md).

## Architecture

TechShu-specific customisation lives in **its own plugin layer** (`techshu-brand`),
not as edits to the base content and marketing plugins.

This is deliberate:

- Base plugins keep taking upstream improvements with no merge conflicts.
- TechShu proprietary content - methodology, SOPs, brand data, client
  configuration - versions independently and can be permission-controlled
  independently.
- A client-vertical layer can be added or dropped per engagement without
  touching the base.

**Do not** edit vendored base plugins in place to add TechShu behaviour. If a
TechShu need cannot be expressed as configuration or a skill in `techshu-brand`,
raise it rather than patching the base.

## Adding a plugin

1. Create `plugins/<name>/` with `.claude-plugin/plugin.json`.
2. Add an entry to `.claude-plugin/marketplace.json` (sources resolve against
   `./plugins` via `metadata.pluginRoot`).
3. Validate: `claude plugin validate`
4. Tag the release: `claude plugin tag --push`

## Versioning

Releases are tagged `{plugin-name}--v{version}`, matching the `version` field in
that plugin's `plugin.json`. `claude plugin tag --push` derives the tag and
validates the two agree before creating it.

## Visibility

This repository is **private**. It contains TechShu delivery SOPs and brand
data. Keep it private.
