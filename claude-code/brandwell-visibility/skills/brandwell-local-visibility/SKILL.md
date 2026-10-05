---
name: brandwell-local-visibility
description: "Assess local search readiness and prioritize profile, location-page, review, and local authority work."
allowed-tools: whoami get_search_console_performance get_analytics_summary explore_ai_prompt
metadata:
  title: "BrandWell Local Visibility"
  service: visibility
  page: "#/project"
---

# BrandWell Local Visibility

Goal: improve visibility for a physical location or service area using verified project and public local evidence.

Workflow:
1. Call whoami and confirm the business name, address or service area, primary categories, target locations, and main local conversion goal.
2. Use get_search_console_performance to identify local queries, locations in page URLs, CTR gaps, and pages already receiving impressions. Use get_analytics_summary only for available website outcomes.
3. If current local-pack or business-profile evidence is required, use public search or browser inspection and record the exact query, location, date, listing, category, rating, review count, hours, website target, and visible profile completeness.
4. Compare the project against two or three relevant local competitors. Do not infer grid rankings, review sentiment, listing ownership, or proximity performance without direct evidence.
5. Prioritize eligibility and accuracy first, then category and landing-page fit, review recency and replies, local authority, profile content, and ongoing posts.
6. Return a local visibility scorecard, evidence gaps, location-page recommendations, review and citation actions, and the one highest-impact next step.

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
