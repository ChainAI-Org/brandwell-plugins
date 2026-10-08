# BrandWell plugins for Claude Code, Codex and Cursor

BrandWell's skills and MCP server as plugins for Claude Code, Codex and Cursor, one plugin per BrandWell product. They let your AI work in your BrandWell projects. Install the products you use. You need a BrandWell account.

- BrandWell Visibility (`brandwell-visibility`): AI and search visibility in BrandWell
- BrandWell RankWell (`brandwell-rankwell`): Plan and write content with RankWell
- BrandWell Link Builder (`brandwell-link-builder`): Link Builder campaigns and prospects
- BrandWell MarketPulse (`brandwell-marketpulse`): Find who is in market with MarketPulse
- BrandWell Outreach (`brandwell-outreach`): Email campaigns with BrandWell Outreach
- BrandWell Direct Mail (`brandwell-direct-mail`): Postcard campaigns with BrandWell
- BrandWell TrafficID (`brandwell-trafficid`): Who visits your site, with TrafficID
- BrandWell SocialStreams (`brandwell-socialstreams`): Social opportunities with SocialStreams
- BrandWell Lead Database (`brandwell-lead-database`): Find, enrich and organize leads in BrandWell
- BrandWell Usage and plans (`brandwell-account`): Usage, plans, wallet and connected agents
- BrandWell Automations (`brandwell-automations`): Automate work across BrandWell

## Install

Claude Code (version 2.1.275 or later), in a session, one command per plugin:

```
/plugin install brandwell-visibility --marketplace ChainAI-Org/brandwell-plugins
```

Or from a shell: `claude plugin marketplace add ChainAI-Org/brandwell-plugins`, then `claude plugin install brandwell-visibility@brandwell`.

Codex:

```
codex plugin marketplace add ChainAI-Org/brandwell-plugins && codex plugin add brandwell-visibility@brandwell
```

Cursor: open Customize, find the BrandWell plugins in the marketplace and click Install. Until they are listed there, copy a plugin's folder, such as `cursor/brandwell-visibility/`, to `~/.cursor/plugins/local/brandwell-visibility` and reload Cursor.

## Sign in

There is no API key to copy. The first time a plugin connects, your browser opens BrandWell: sign in, tick the projects the AI may use and click Allow. The tools you can use follow your BrandWell plan, whichever plugins you install.

- Claude Code: if the browser does not open, type `/mcp`, choose the plugin's brandwell server and sign in.
- Codex: run `codex mcp login brandwell`.

## Machines without a browser

The plugins sign in through the browser. For CI jobs, scripts and machines without a browser, use a project API key instead, which you create in the BrandWell portal under Visibility > MCP > Advanced. Keep it in `BRANDWELL_MCP_TOKEN` and add the server directly (the single quotes keep the variable a reference, so the key is read when the client connects):

```
claude mcp add --transport http brandwell https://portal.brandwell.ai/mcp --header 'Authorization: Bearer ${BRANDWELL_MCP_TOKEN}'
codex mcp add brandwell --url https://portal.brandwell.ai/mcp --bearer-token-env-var BRANDWELL_MCP_TOKEN
```

## What is in this repository

- `claude-code/brandwell-visibility/`: BrandWell Visibility for Claude Code
- `codex/brandwell-visibility/`: BrandWell Visibility for Codex
- `cursor/brandwell-visibility/`: BrandWell Visibility for Cursor
- `claude-code/brandwell-rankwell/`: BrandWell RankWell for Claude Code
- `codex/brandwell-rankwell/`: BrandWell RankWell for Codex
- `cursor/brandwell-rankwell/`: BrandWell RankWell for Cursor
- `claude-code/brandwell-link-builder/`: BrandWell Link Builder for Claude Code
- `codex/brandwell-link-builder/`: BrandWell Link Builder for Codex
- `cursor/brandwell-link-builder/`: BrandWell Link Builder for Cursor
- `claude-code/brandwell-marketpulse/`: BrandWell MarketPulse for Claude Code
- `codex/brandwell-marketpulse/`: BrandWell MarketPulse for Codex
- `cursor/brandwell-marketpulse/`: BrandWell MarketPulse for Cursor
- `claude-code/brandwell-outreach/`: BrandWell Outreach for Claude Code
- `codex/brandwell-outreach/`: BrandWell Outreach for Codex
- `cursor/brandwell-outreach/`: BrandWell Outreach for Cursor
- `claude-code/brandwell-direct-mail/`: BrandWell Direct Mail for Claude Code
- `codex/brandwell-direct-mail/`: BrandWell Direct Mail for Codex
- `cursor/brandwell-direct-mail/`: BrandWell Direct Mail for Cursor
- `claude-code/brandwell-trafficid/`: BrandWell TrafficID for Claude Code
- `codex/brandwell-trafficid/`: BrandWell TrafficID for Codex
- `cursor/brandwell-trafficid/`: BrandWell TrafficID for Cursor
- `claude-code/brandwell-socialstreams/`: BrandWell SocialStreams for Claude Code
- `codex/brandwell-socialstreams/`: BrandWell SocialStreams for Codex
- `cursor/brandwell-socialstreams/`: BrandWell SocialStreams for Cursor
- `claude-code/brandwell-lead-database/`: BrandWell Lead Database for Claude Code
- `codex/brandwell-lead-database/`: BrandWell Lead Database for Codex
- `cursor/brandwell-lead-database/`: BrandWell Lead Database for Cursor
- `claude-code/brandwell-account/`: BrandWell Usage and plans for Claude Code
- `codex/brandwell-account/`: BrandWell Usage and plans for Codex
- `cursor/brandwell-account/`: BrandWell Usage and plans for Cursor
- `claude-code/brandwell-automations/`: BrandWell Automations for Claude Code
- `codex/brandwell-automations/`: BrandWell Automations for Codex
- `cursor/brandwell-automations/`: BrandWell Automations for Cursor
- `.claude-plugin/marketplace.json`, `.agents/plugins/marketplace.json` and `.cursor-plugin/marketplace.json`: the marketplace files for each client
- `server.json`: BrandWell's MCP server for the MCP Registry

This repository is built from BrandWell's portal source; changes made here by hand are overwritten by the next release. See CHANGELOG.md for what changed in each version.
