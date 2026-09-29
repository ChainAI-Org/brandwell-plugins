---
name: brandwell-keyword-clustering
description: "Group stored keywords and Search Console queries by intent, page type, and landing-page fit."
allowed-tools: whoami list_saved_keywords get_search_console_performance get_cannibalization_candidates get_serp_results explore_ai_prompt visibility_save_keyword visibility_set_rank_keyword
metadata:
  title: "BrandWell Keyword Clustering"
  service: visibility
  page: "#/market"
---

# BrandWell Keyword Clustering

Goal: turn a known keyword set into page groups, priorities, and cannibalization checks.

Workflow:
1. Call whoami, list_saved_keywords, get_search_console_performance with up to 100 rows, and get_cannibalization_candidates.
2. Normalize case and whitespace, remove duplicates, and retain each term's measured clicks, impressions, CTR, position, volume, difficulty, intent, and current page when present.
3. Cluster by shared search intent and page type, not by word overlap alone. Separate informational, commercial investigation, comparison, transactional, navigational, and local intent when the evidence supports it.
4. Map every useful cluster to an existing important page, a proposed new page, or a no-target decision.
5. Treat the cannibalization tool as an exact-query conflict detector, not an automatic merge decision. For meaningful candidates, inspect both pages and call get_serp_results for the shared query to verify intent and ranking-page overlap.
6. Recommend keep separate, retarget, canonicalize, or merge and redirect only after comparing purpose, content overlap, backlinks, conversions when available, and the SERP. Show the supporting query and URL rows.
7. Return a table with cluster, primary keyword, supporting terms, combined known demand, intent, current URLs, recommended target, action, priority, and evidence gaps.
8. Provide copy-ready tags and mapping recommendations for user review. When the person asks, save a cluster's keywords with visibility_save_keyword or rank-track its primary keywords with visibility_set_rank_keyword. Never change pages.

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
