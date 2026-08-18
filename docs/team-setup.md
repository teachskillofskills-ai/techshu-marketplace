# Team setup

## Option A - per-project auto-registration

Add to `.claude/settings.json` in a TechShu project repository. Team members get
the marketplace registered once they trust the folder, with no separate prompt.

```json
{
  "extraKnownMarketplaces": {
    "techshu": {
      "source": {
        "source": "github",
        "repo": "teachskillofskills-ai/techshu-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "techshu-standard@techshu": true
  }
}
```

## Option B - organisation-wide

Distribute through **Organization settings > Plugins**. Organisation sync reads
the marketplace through the Claude GitHub App, so team members never need direct
access to this repository.

Constraint: under org sync, every plugin source must be a **relative path inside
this repository**, or a `github` / `url` / `git-subdir` source under the same
owner. Sources under a different owner must be public. This is why plugins are
vendored into `plugins/` rather than referenced from elsewhere.

## Private repository notes

Background auto-update disables git credential helpers by default, so HTTPS
pulls against a private marketplace can fail intermittently. On team machines:

```
gh auth setup-git
```

And set:

```
CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE=1
```

This keeps the existing clone when a background pull fails instead of deleting
and re-cloning. Manual `/plugin marketplace update` still pulls with stored
credentials.

## CI

Export a token with read access to this repository as `GH_TOKEN`, then run
`gh auth setup-git` before installing plugins. The default GitHub Actions
workflow token can only reach its own repository.
