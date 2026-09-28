---
name: brandwell-content-consolidation
description: "Identify pages competing for the same queries and decide whether to separate, retarget, canonicalize, or merge them."
allowed-tools: whoami get_cannibalization_candidates get_serp_results get_backlinks_overview explore_ai_prompt
metadata:
  title: "BrandWell Content Consolidation"
  service: visibility
  page: "#/project"
---

# BrandWell Content Consolidation

Goal: resolve genuine page competition without merging useful pages that serve different intent.

Workflow:
1. Call whoami and get_cannibalization_candidates. Start with strong candidates that have meaningful impressions across at least two URLs.
2. For each candidate, compare the page purpose, primary intent, content overlap, clicks, impressions, CTR, position, and any known backlinks or business role. Inspect the live pages when accessible.
3. Call get_serp_results for the shared query. If the SERP supports multiple page types or intents, prefer differentiation and retargeting. If the pages answer the same intent and split authority, consider consolidation.
4. Use get_backlinks_overview for exact pages only when link equity could change the destination decision.
5. Classify every pair as keep separate, differentiate, retarget one page, canonicalize, or merge and redirect. Include confidence, evidence, destination URL, content to preserve, internal links to update, redirect requirement, and post-change validation.
6. Never instruct a merge from the exact-query signal alone. Mark cases with unclear intent, conversion value, or canonical evidence for manual review.

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
