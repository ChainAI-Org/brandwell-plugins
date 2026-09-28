# BrandWell (API key) for Claude Code

BrandWell's skills and MCP server for Claude Code. They let your AI work in your BrandWell projects: AI and search visibility, keyword research, content, links, outreach, direct mail, MarketPulse and TrafficID.

This plugin connects with a BrandWell project API key, for machines without a browser. Create the key in the BrandWell portal under Visibility > MCP > Advanced. Claude Code asks for it when you enable the plugin and keeps it in your system's secure storage. On a machine with a browser, install BrandWell instead.

## What it runs and sends

The plugin runs nothing on your computer: it has no hooks, scripts or local servers. It contains skills, which are written instructions for your AI, and one MCP server address, `https://portal.brandwell.ai/mcp`. Your AI sends BrandWell's MCP server only the requests it makes with BrandWell's tools, as the signed-in person (or the project the API key belongs to), and only for the projects you allowed. Tools that change something, send email or mail, publish, or use credits are labelled that way, so your AI app can ask you before it uses them. BrandWell's privacy policy covers what BrandWell keeps: https://brandwell.ai/privacy-policy/.

Install instructions are in the README of https://github.com/ChainAI-Org/brandwell-plugins.
