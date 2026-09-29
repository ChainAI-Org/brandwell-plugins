---
name: brandwell-competitive-landscape
description: "Map the search and AI visibility landscape around the project's confirmed market and competitors."
allowed-tools: whoami get_visibility_overview get_search_console_performance get_rank_tracking get_serp_results get_domain_overview get_domain_keywords get_backlinks_overview explore_ai_prompt
metadata:
  title: "BrandWell Competitive Landscape"
  service: visibility
  page: "#/project"
---

# BrandWell Competitive Landscape

Goal: identify who consistently wins the searches and AI citations that matter, then show where the Company Project has a credible opening.

Workflow:
1. Call whoami and get_visibility_overview. Use the stored competitor list as the starting roster and confirm which competitors matter to the user.
2. Anchor the project's own position with get_search_console_performance, get_rank_tracking, and AI visibility evidence from get_visibility_overview.
3. Use get_serp_results for a representative query set. Group recurring winners as direct competitors, publishers, directories, marketplaces, communities, or unrelated domains.
4. Call get_domain_overview for the three to five strongest recurring domains, then get_domain_keywords for direct competitors that warrant deeper theme analysis. Use get_backlinks_overview only when authority may explain the gap.
5. Compare measured organic footprint, ranking themes, visible content types, positioning, link authority, and AI citation patterns. Label estimates, first-party evidence, and public observations separately.
6. Return the query set, recurring domains, why each wins, the project's current evidence, underserved angles, and the top three actions.

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
