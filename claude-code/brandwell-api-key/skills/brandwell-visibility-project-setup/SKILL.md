---
name: brandwell-visibility-project-setup
description: "Establish the domain, market, goals, positioning, competitors, and measurement status for a Company Project."
allowed-tools: whoami get_search_console_performance get_analytics_summary explore_ai_prompt visibility_save_keyword visibility_set_rank_keyword visibility_run_site_audit
metadata:
  title: "BrandWell Visibility Project Setup"
  service: visibility
  page: "#/project"
---

# BrandWell Visibility Project Setup

Goal: orient one Company Project so later visibility work starts from the correct business context.

Workflow:
1. Call whoami and summarize the Company Project, canonical domain, country, language, business description, target audience, brand terms, and competitors already stored.
2. Ask only for missing or disputed context in small batches: the primary business goal, success metric, timeframe, offers, best-fit audience, positioning, important pages, competitors, voice constraints, and topics to avoid.
3. Check get_search_console_performance and get_analytics_summary. Report each connection as connected, not connected, or unavailable based only on the returned status.
4. Project settings are changed in BrandWell, not through these tools, so never claim to have saved them. Give the user a concise, copy-ready settings summary and direct them to BrandWell Company Project settings for those changes. When the person asks, save their key keywords with visibility_save_keyword, rank-track them with visibility_set_rank_keyword, and run a first site audit with visibility_run_site_audit after they confirm its cost.
5. Finish with a status table for domain, market, goal, positioning, competitors, key pages, Search Console, Analytics, and the single best next workflow.

Choose the next workflow from Site Health Audit, Content Opportunities, Content Consolidation, Keyword Research, Keyword Clustering, Competitive Landscape, Competitor Analysis, Local Visibility, Link Prospecting, or AI Citation Analysis.

Data and safety rules:
- In the BrandWell Assistant the Company Project is the one the person is working in, so never ask them to confirm it. Elsewhere, begin with whoami to learn the Company Project and its canonical domain before using any other visibility tool.
- Use only project-bound BrandWell tools. Free stored-data tools include overview, Search Console, Analytics, content opportunities, cannibalization candidates, saved keywords, rank tracking, and stored site audits.
- Research tools include domain overview, domain keywords, domain pages, keyword research, SERP results, backlinks, AI citations, and AI Prompt Explorer. New research may use the Company Project's research allowance; the same request repeated within 24 hours reuses the earlier result.
- Start with stored first-party evidence. Use the smallest focused research call set needed to answer the question, reuse a recent result, and never repeat the same research call.
- State the source, reporting window, connection status, and fetched time when the tool returns them. Separate measured evidence from your interpretation.
- If a connection is missing, a snapshot is stale, or the needed data is unavailable, say exactly what is missing. Ask the user to connect the source or open the matching BrandWell Visibility page when that is the required next step. Never invent a result.
- If research needs its estimated cost accepted, ask the person and show the estimate; in the BrandWell Assistant, call ask_person with confirms set to the same call plus the confirmed_cost_usd the tool named, then run it once they accept. If a project budget rule blocks research, explain the requested research in customer language and wait. Never name the services behind BrandWell's data, and never reveal account balances or credentials.
- Run explore_ai_prompt only when the user explicitly asks to test a current AI answer or approves the proposed prompt and model set. Default to one model unless cross-model comparison is material.
- Keep every request scoped to the Company Project returned by whoami. Never request, combine, infer, or reveal another workspace's data.
- Web research may supplement project data when the user asks for current public evidence. Cite the public source and date. Do not present public estimates as first-party BrandWell measurements.
- Analysis, plans, briefs, and drafts are allowed. Publishing, outreach, purchases, account changes, and other external effects require explicit approval.
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
