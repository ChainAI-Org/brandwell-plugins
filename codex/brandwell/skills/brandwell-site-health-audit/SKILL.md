---
name: brandwell-site-health-audit
description: "Turn the latest site crawl and first-party search evidence into a concise, prioritized audit, running a fresh crawl when the person confirms it."
allowed-tools: whoami list_site_audits get_search_console_performance get_site_audit visibility_run_site_audit get_domain_overview get_backlinks_overview explore_ai_prompt
metadata:
  title: "BrandWell Site Health Audit"
  service: visibility
  page: "#/project"
---

# BrandWell Site Health Audit

Goal: produce a plain-language site health report centered on one action the user can take this week.

Workflow:
1. Call whoami, list_site_audits, and get_search_console_performance.
2. Select the newest completed audit for the canonical domain. If none exists, or the person wants a fresh one, offer to run one with visibility_run_site_audit. It spends research budget, so the person confirms its estimated cost on a card first.
3. Call get_site_audit with that audit ID. Group page findings by impact: blocking access or indexing, broken responses and redirects, missing or conflicting page signals, thin or duplicate content, and performance evidence.
4. Cross-check priorities against Search Console. Favor issues affecting pages or queries with meaningful impressions, clicks, or business importance.
5. When authority or market footprint determines the priority, call get_domain_overview and get_backlinks_overview once for the canonical domain. Reuse fresh results.
6. Report the audit date, pages crawled, scope limits, evidence, the one recommended action, three supporting fixes, affected URLs, expected outcome, and a verification checklist.
7. Start a crawl only after the person confirms it. Do not claim a live page was checked, or infer an issue outside the stored audit, unless you separately inspect the public page and label that evidence.

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
