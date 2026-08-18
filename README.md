# TechShu Plugin Marketplace

Installation hub for the marketing plugins used at Indus Net TechShu.
Works on Claude Code, Claude Cowork, OpenAI Codex, Cursor, Grok, Hermes and OpenClaw.

## Plugins

| Plugin | What it does |
| --- | --- |
| `digital-marketing-pro` | Marketing OS - strategy, SEO, AEO/GEO, paid media, content, CRM, analytics. 163 skills, 24 agents. |
| `contentforge` | Editorial pipeline - research, fact-check, draft, humanize, deliver. 22 skills, 13 agents, 10 quality gates. |
| `socialforge` | Social production - content calendar in, on-brand copy, images and video out. |

## Install

### Claude Code / Claude Cowork

```
/plugin marketplace add teachskillofskills-ai/techshu-marketplace
/plugin install digital-marketing-pro@techshu
/plugin install contentforge@techshu
/plugin install socialforge@techshu
```

If the install summary says `Run /reload-plugins to activate.`, run that.

### Codex, Cursor, Grok, Hermes, OpenClaw

Add this repository as a marketplace in your agent, then install the plugins.
Each environment reads its own manifest from this repo:

| Manifest | Environment |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code, Claude Cowork |
| `.cursor-plugin/marketplace.json` | Cursor |
| `.grok-plugin/marketplace.json` | Grok |
| `.agents/plugins/marketplace.json` | Codex, Antigravity, Hermes, OpenClaw |

No GitHub account or authentication is needed. Anyone on the team can install
from their own individual agent account.

## Source and licence

These are MIT-licensed open-source plugins by Indranil Banerjee, maintained at
[github.com/indranilbanerjee](https://github.com/indranilbanerjee) and also
published through [neels-plugins](https://github.com/indranilbanerjee/neels-plugins).

This marketplace points at those upstream repositories, so the team always gets
the current release with no copies to keep in sync.

## Configuration

Brand voice, terminology, audience and compliance rules are configured inside
the plugins themselves, per brand, using their own setup skills:

```
/digital-marketing-pro:brand-setup
/contentforge:brand-setup
```

Configuration lives in the account where the plugin is installed. Nothing about
a brand or a client is stored in this repository.
