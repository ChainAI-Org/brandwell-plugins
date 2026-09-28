# BrandWell plugins for Claude Code and Codex

BrandWell's skills and MCP server as plugins for Claude Code and Codex. They let your AI work in your BrandWell projects: AI and search visibility, keyword research, content, links, outreach, direct mail, MarketPulse and TrafficID. You need a BrandWell account.

## Install

Claude Code (version 2.1.275 or later), in a session:

```
/plugin install brandwell --marketplace ChainAI-Org/brandwell-plugins
```

Or from a shell: `claude plugin marketplace add ChainAI-Org/brandwell-plugins`, then `claude plugin install brandwell@brandwell`.

Codex:

```
codex plugin marketplace add ChainAI-Org/brandwell-plugins && codex plugin add brandwell@brandwell
```

## Sign in

There is no API key to copy. The first time BrandWell connects, your browser opens BrandWell: sign in, tick the projects the AI may use and click Allow.

- Claude Code: if the browser does not open, type `/mcp`, choose brandwell and sign in.
- Codex: run `codex mcp login brandwell`.

## Machines without a browser: BrandWell (API key)

Install **BrandWell (API key)** (`brandwell-api-key`) instead of BrandWell, not as well. It has the same skills and tools and uses a project API key, which you create in the BrandWell portal under Visibility > MCP > Advanced.

- Claude Code: `/plugin install brandwell-api-key --marketplace ChainAI-Org/brandwell-plugins`. Claude Code asks for the key when you enable the plugin and keeps it in your system's secure storage.
- Codex: set the `BRANDWELL_MCP_TOKEN` environment variable to the key, then `codex plugin add brandwell-api-key@brandwell`. Codex has no field for the key, so it reads that variable.

Without a plugin, for CI jobs and scripts, keep the key in `BRANDWELL_MCP_TOKEN` and add the server directly (the single quotes keep the variable a reference, so the key is read when the client connects):

```
claude mcp add --transport http brandwell https://portal.brandwell.ai/mcp --header 'Authorization: Bearer ${BRANDWELL_MCP_TOKEN}'
codex mcp add brandwell --url https://portal.brandwell.ai/mcp --bearer-token-env-var BRANDWELL_MCP_TOKEN
```

## What is in this repository

- `claude-code/brandwell/`: BrandWell for Claude Code
- `codex/brandwell/`: BrandWell for Codex
- `claude-code/brandwell-api-key/`: BrandWell (API key) for Claude Code
- `codex/brandwell-api-key/`: BrandWell (API key) for Codex
- `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`: the marketplace files for each client

This repository is built from BrandWell's portal source; changes made here by hand are overwritten by the next release. See CHANGELOG.md for what changed in each version.
