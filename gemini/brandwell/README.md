# BrandWell for Gemini CLI

BrandWell lets your AI assistant run your marketing and sales automations in your own BrandWell account. Describe what you want in a sentence and it builds the automation as a draft for you to review, then activates it, tests it on a record and shows you every run. Steps that need you wait for your approval.

It works with the rest of BrandWell too: find people and companies and build audiences, fill in missing details with data tools, see who is in market with MarketPulse and who visits your website with TrafficID, check your AI and search visibility, plan and write content in RankWell, and run email and postcard campaigns.

You sign in with your BrandWell account and choose which projects the assistant may use. Tools that change something, send email or mail, publish, or use credits are labelled that way, so your AI app can ask you before it uses them. What you can use follows your BrandWell plan.

## Sign in

There is no API key to copy. The first time BrandWell connects, your browser opens BrandWell: sign in, tick the projects the AI may use and click Allow.

## What it runs and sends

This package runs nothing on your computer: it has no hooks, scripts or local servers. It contains skills, which are written instructions for your AI, and one MCP server address, `https://portal.brandwell.ai/mcp`. Your AI sends BrandWell's MCP server only the requests it makes with BrandWell's tools, as the signed-in person, and only for the projects you allowed. BrandWell's privacy policy covers what BrandWell keeps: https://brandwell.ai/privacy-policy/.

## Support

Email support@brandwell.ai. Terms of service: https://brandwell.ai/terms/.

Install instructions are in the README of https://github.com/ChainAI-Org/brandwell-plugins.
