---
name: brandwell-competitor-analysis
description: "Analyze one confirmed competitor using public evidence and the project's stored BrandWell baseline."
allowed-tools: whoami get_search_console_performance get_visibility_overview get_rank_tracking get_analytics_summary get_domain_overview get_domain_keywords get_domain_pages get_backlinks_overview get_serp_results explore_ai_prompt
metadata:
  title: "BrandWell Competitor Analysis"
  service: visibility
  page: "#/project"
---

# BrandWell Competitor Analysis

Goal: turn one competitor comparison into a practical page, content, distribution, or citation plan.

Workflow:
1. Call whoami and confirm the competitor domain, market, comparison goal, and whether it appears in the stored competitor list.
2. Build the Company's baseline from get_search_console_performance, get_visibility_overview, get_rank_tracking, and get_analytics_summary as relevant.
3. Call get_domain_overview, get_domain_keywords, and get_domain_pages for the competitor. Use get_backlinks_overview when authority matters and get_serp_results for the most important shared terms.
4. Inspect the competitor's public pages before making content-depth, positioning, structured-data, or page-type claims. Third-party market estimates are not the competitor's private analytics or conversion data.
5. Group competitor strengths by query ownership, content themes, page formats, positioning, authority signals, local signals, and AI citation sources.
6. Separate confirmed evidence, reasonable inference, and unknowns.
7. Return an executive summary, evidence table, overlapping opportunities, gaps the Company can credibly own, pages to improve or create, and a prioritized 30-day plan.

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
