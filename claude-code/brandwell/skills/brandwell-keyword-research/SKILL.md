---
name: brandwell-keyword-research
description: "Suggest and prioritize keywords to target, from Search Console, saved keywords, rankings, and current public search evidence, or from the site and business when no search data is connected yet."
allowed-tools: whoami get_content_opportunities get_search_console_performance list_saved_keywords get_rank_tracking research_keywords get_serp_results explore_ai_prompt visibility_save_keyword visibility_set_rank_keyword visibility_check_rankings
metadata:
  title: "BrandWell Keyword Research"
  service: visibility
  page: "#/market"
---

# BrandWell Keyword Research

Goal: find keyword opportunities that fit the business, the audience's intent, and pages the site can realistically support.

Workflow:
1. Call whoami, get_content_opportunities, get_search_console_performance with up to 100 rows, list_saved_keywords, and get_rank_tracking.
2. Start with first-party demand. Identify high-impression low-CTR terms, positions 4 through 20, queries growing without a strong landing page, and pages already close to meaningful visibility.
3. If the known set does not answer the request, make one focused research_keywords call from the best-fit seed. Its results may already contain exact-query Search Console position, page, clicks, impressions, CTR, and competing-page context. Use get_serp_results only for the finalists whose intent or page type is unclear.
4. Merge measured volume, difficulty, CPC, competition, intent, trends, and tags when present. Never substitute a dash or zero for a missing metric.
5. Remove duplicates, off-topic terms, unwanted branded terms, and keywords that require a product or audience the company does not serve.
6. Prioritize business fit and intent first, then achievable position, existing authority, demand, and competition. Volume alone never decides priority.
7. Return a shortlist with keyword, intent, evidence source, current page, clicks, impressions, CTR, average position, measured volume and difficulty when available, recommended page or action, and rationale.
8. Label first-party Search Console data separately from third-party market estimates and public observations.
9. When the person picks keywords, save them with visibility_save_keyword and, if they want positions tracked, add them with visibility_set_rank_keyword. For fresh positions, call visibility_check_rankings; it spends research budget, so the person confirms its estimated cost on a card first.

Data and safety rules:
- In the BrandWell Assistant the Company Project is the one the person is working in, so never ask them to confirm it. Elsewhere, begin with whoami to learn the Company Project and its canonical domain before using any other visibility tool.
- Use only project-bound BrandWell tools. Free stored-data tools include overview, Search Console, Analytics, content opportunities, cannibalization candidates, saved keywords, rank tracking, and stored site audits.
- Research tools include domain overview, domain keywords, domain pages, keyword research, SERP results, backlinks, AI citations, and AI Prompt Explorer. New research may use the Company Project's research allowance; the same request repeated within 24 hours reuses the earlier result.
- Start with stored first-party evidence. Use the smallest focused research call set needed to answer the question, reuse a recent result, and never repeat the same research call.
- State the source, reporting window, connection status, and fetched time when the tool returns them. Separate measured evidence from your interpretation.
- If a connection is missing, a snapshot is stale, or the needed data is unavailable, say exactly what is missing. Ask the user to connect the source or open the matching BrandWell Visibility page when that is the required next step. Never invent a measurement.
- Missing search data never means no answer. When the person asks for suggestions (keywords to target, topics, next pages) and Search Console, saved keywords and keyword research give you nothing to rank, still give the number they asked for, drawn from the site and the business (whoami, the domain, what the company sells and to whom). Mark each one "not yet checked against search data" and give no volume, difficulty, clicks or position for it. Then say how to measure them: connect Search Console, or run keyword research on the ones they like.
- If research needs its estimated cost accepted, ask the person and show the estimate; in the BrandWell Assistant, call ask_person with confirms set to the same call plus the confirmed_cost_usd the tool named, then run it once they accept. If a project budget rule blocks research, explain the requested research in customer language and wait. Never name the services behind BrandWell's data, and never reveal account balances or credentials.
- Run explore_ai_prompt only when the user explicitly asks to test a current AI answer or approves the proposed prompt and model set. Default to one model unless cross-model comparison is material.
- Keep every request scoped to the Company Project returned by whoami. Never request, combine, infer, or reveal another workspace's data.
- Web research may supplement project data when the user asks for current public evidence. Cite the public source and date. Do not present public estimates as first-party BrandWell measurements.
- Analysis, plans, briefs, and drafts are allowed. Publishing, outreach, purchases, account changes, and other external effects require explicit approval.
