---
name: brandwell-content-opportunities
description: "Find the lowest-hanging existing pages to optimize from first-party search evidence and verified intent."
allowed-tools: whoami get_content_opportunities get_search_console_performance get_serp_results explore_ai_prompt
metadata:
  title: "BrandWell Content Opportunities"
  service: visibility
  page: "#/project"
---

# BrandWell Content Opportunities

Goal: identify the existing pages most likely to gain qualified organic traffic from a focused optimization pass.

Workflow:
1. Call whoami and get_content_opportunities. If Search Console is not connected or has no usable rows, explain that this workflow needs first-party query and page evidence.
2. Call get_search_console_performance for the leading pages. Use Analytics only when page-level business outcome evidence is actually available. Do not treat sitewide sessions as page conversion evidence.
3. Rank opportunities by business fit, query intent, impressions, current position, CTR gap, and the number of related queries. The tool score is a prioritization signal, not a promise of traffic.
4. Inspect each finalist's current public page. Call get_serp_results for up to three primary queries when the ranking page type or intent is unclear.
5. For each recommended page, specify the target query, current clicks, impressions, CTR, position, why it is winnable, the exact title, content, internal-link, or intent-alignment change, and how to verify the result after the next reporting window.
6. Return the best five pages first, followed by lower-confidence candidates and evidence gaps. Do not recommend a new page when the existing page can satisfy the intent with a focused improvement.

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
