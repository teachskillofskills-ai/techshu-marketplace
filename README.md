# TechShu Plugin Marketplace

Internal plugin marketplace for Indus Net TechShu Digital Pvt. Ltd.

## Plugins

| Plugin | Source | Purpose |
| --- | --- | --- |
| `digital-marketing-pro` | `teachskillofskills-ai/digital-marketing-pro` | Marketing OS: strategy, SEO, AEO/GEO, paid media, content, CRM, analytics |
| `contentforge` | `teachskillofskills-ai/contentforge` | Editorial production: research, verification, drafting, delivery |
| `socialforge` | `teachskillofskills-ai/socialforge` | Social production: calendar to on-brand copy, images, video |
| `techshu-brand` | `./plugins/techshu-brand` | TechShu voice, delivery SOPs, compliance guardrails |
| `techshu-standard` | `./plugins/techshu-standard` | Bundle - installs the whole set in one step |

## Install

```
/plugin marketplace add teachskillofskills-ai/techshu-marketplace
/plugin install techshu-standard@techshu
```

If the install summary says `Run /reload-plugins to activate.`, run that.

For team-wide setup, see [docs/team-setup.md](docs/team-setup.md).

## Agent environments

Four manifests are maintained so the suite installs across environments:

| Manifest | Environment |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code, Claude Cowork |
| `.cursor-plugin/marketplace.json` | Cursor |
| `.grok-plugin/marketplace.json` | Grok |
| `.agents/plugins/marketplace.json` | OpenAI Codex, Antigravity, Hermes |

`techshu-brand` and `techshu-standard` are listed in the Claude manifest only,
because they resolve by relative path inside this repository. To make them
installable on Cursor, Grok and Codex, move each into its own repository and
reference it by URL, the way the three marketing plugins are referenced.

## Provenance and licence

`digital-marketing-pro`, `contentforge` and `socialforge` are MIT-licensed
open-source projects by Indranil Banerjee, upstream at
[github.com/indranilbanerjee](https://github.com/indranilbanerjee) and published
through [neels-plugins](https://github.com/indranilbanerjee/neels-plugins).

The repositories here are **imports, not forks** - independent copies with full
history and no upstream link, so TechShu customisation never flows back to the
originals. The MIT LICENSE file must remain in each copy; that is a condition of
the licence, not a courtesy.

## Architecture

TechShu-specific customisation belongs in **`techshu-brand`**, not in edits to
the three imported plugins.

- The imported plugins keep taking upstream improvements with no merge conflicts.
- TechShu proprietary content - methodology, SOPs, brand data, client
  configuration - versions independently and can be permission-controlled
  independently.
- A client-vertical layer can be added or dropped per engagement without
  touching the base.

If a TechShu need cannot be expressed as configuration or a skill in
`techshu-brand`, raise it rather than patching an imported plugin.

## Adding a plugin

1. Create `plugins/<name>/` with `.claude-plugin/plugin.json`, or import a repo.
2. Add an entry to each manifest you want it available in.
3. Validate: `claude plugin validate`
4. Tag the release: `claude plugin tag --push`

## Visibility

This repository and the three plugin repositories are **private**. They hold
TechShu delivery SOPs and brand data. Keep them private.
