---
name: brandwell-ai-citation-analysis
description: "Analyze stored AI mentions and cited pages, then prioritize changes that can improve brand discoverability."
allowed-tools: whoami get_ai_citations get_search_console_performance list_saved_keywords explore_ai_prompt get_ai_answer_history get_gsc_generative_ai_performance
metadata:
  title: "BrandWell AI Citation Analysis"
  service: visibility
  page: "#/project"
---

# BrandWell AI Citation Analysis

Goal: explain where the brand appears in AI search, which project pages earn citations, and what evidence-backed work could improve discoverability.

Workflow:
1. Call whoami and get_ai_citations. Historical citation lookup targets a brand or domain, so use the canonical domain and saved competitors unless the user supplies another brand name. A domain must be the project's or a saved competitor's. Never pass a buyer keyword as the historical lookup target. Filter the returned questions for topic relevance instead.
2. Explain that historical citation discovery and live prompt testing are different datasets. Report fetched time, market scope, platform coverage, missing metrics, and the exact questions and sources returned by the citation index.
3. Rank questions and cited pages by mentions and known AI search volume. Group them by page type, topic, buyer intent, and whether the canonical domain is cited.
4. Identify coverage gaps by comparing cited topics with the business goal, Search Console queries, saved keywords, and the project's important offers. Use get_search_console_performance and list_saved_keywords when those comparisons help.
5. When the user explicitly asks to test a current answer, propose the exact prompt and smallest useful model set, then call explore_ai_prompt after approval. Report each model separately, including answer text, citations, fan-out queries, web-search state, and whether the brand was actually mentioned.
6. Never infer that a historical question is continuously tracked or that a citation equals a recommendation. Use the tracked AI query portfolio for keyword-level and buyer-question measurement. If a historical lookup needs a fresh paid request, explain that approval is required and do not supply confirmed_cost_usd until the user explicitly approves the current lookup. Never claim a prompt was tested unless the live tool returned a result in the current session.
7. Return total mentions, platform mix, share of voice when competitors were supplied, top questions, top cited pages, citation gaps, source-quality observations, content or technical actions, and a prioritized measurement plan.
- get_gsc_generative_ai_performance is Google's imported AI Overviews and AI Mode subset of Search Console; its rows are already inside the normal web totals, never added to them. get_ai_answer_history shows tracked questions' saved answers and trends.

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
