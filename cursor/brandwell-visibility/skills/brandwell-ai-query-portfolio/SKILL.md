---
name: brandwell-ai-query-portfolio
description: "Build and manage a measured portfolio of buyer questions for AI visibility strategy."
allowed-tools: whoami list_tracked_ai_queries suggest_ai_queries track_ai_queries check_tracked_ai_query update_tracked_ai_query get_rankwell_strategy get_rankwell_generation_job list_rankwell_generation_jobs get_ai_answer_history
metadata:
  title: "BrandWell AI Query Portfolio"
  service: visibility
  page: "#/project"
---

# BrandWell AI Query Portfolio

Goal: combine historical citation discovery with a controlled set of live buyer questions that can guide content strategy and measure change.

Workflow:
1. Call whoami and list_tracked_ai_queries. Report the active count, plan limit, latest checks, model coverage, brand mentions, citations, and next scheduled checks.
2. Call suggest_ai_queries. Compare suggestions with Search Console queries, saved keyword research, content opportunities, cannibalization candidates, historical AI citations, and current RankWell content when those sources are relevant.
3. Normalize and deduplicate candidate questions. Remove questions already tracked, already answered by a strong existing page, outside the project's audience or offers, or too similar to another prompt.
4. Return a proposed portfolio with question, buyer intent, evidence source, related keyword or GSC query, current ranking page when present, citation gap, recommended content or optimization action, and priority.
5. Ask the user which questions to track, unless the person already named them. Only then call track_ai_queries. Do not exceed the remaining plan capacity.
6. Tracked questions recheck automatically. Call check_tracked_ai_query only when the user explicitly requests an immediate check. Use update_tracked_ai_query only for a requested pause, resume, archive, or model change.
7. For a question that needs content, call get_rankwell_strategy before recommending a brief or article. Connect the result to the prompt portfolio, baseline, citation gap, proposed action, and 7, 14, and 28 day review points.
- get_ai_answer_history shows saved answers, mention and citation trends, competitors and content gaps for tracked questions; pass run_id to read one check's answer text and citations before recommending changes. These measurements can differ from consumer AI apps.

RankWell data and safety rules:
- In the BrandWell Assistant the Company Project is the one the person is working in, so never ask them to confirm it. Elsewhere, begin with whoami to learn the Company Project and its canonical domain before using any RankWell or tracked-query tool.
- Keep every request scoped to that Company Project. Never request, combine, infer, or reveal another workspace's prompts, rankings, briefs, articles, sources, or revisions.
- Start with stored first-party evidence. Reuse Search Console, saved keyword, tracked AI query, and existing RankWell evidence before making a focused research call.
- Always call get_rankwell_strategy before proposing a new article. Respect its create, optimize, merge, or no-action recommendation and explain the supporting evidence.
- Treat Search Console measurements, keyword market estimates, historical AI citation data, and live model checks as different datasets. Historical citation lookup targets the project brand or domain, while tracked AI queries provide keyword-level buyer-question evidence. Label each source and never imply that one proves another.
- Creating a brief, drafting an article, and refining a draft are allowed only when the user asks for that work. These actions create editable BrandWell records and never publish.
- Adding, changing, or manually checking tracked AI queries requires a clear user request. BrandWell enforces the plan limit and project budget. Never name the services behind BrandWell's data, and never reveal credentials, account balances or internal costs.
- Publishing, WordPress changes, outreach, payments, and other external effects require explicit approval. This skill publishes nothing; to publish a finished article, load brandwell-rankwell-content-studio.
- Article generation returns a durable job. Read get_rankwell_generation_job using its job ID until completed, failed, or interrupted. Report the current phase while it runs. Do not report an article as written while its job is queued or running.
- After a timeout or uncertain response, use list_rankwell_generation_jobs before retrying. Preserve an explicit request_key when retrying the same request. Never start duplicate paid work to check status.
- Keyword targets and usage ranges come from BrandWell's content analysis. Preserve the returned targets and counts. Do not substitute a generated keyword list.
- After completion, read the article and report its BrandWell ID, draft status, SEO score, keyword coverage, featured image, evidence gaps, and next review step. Keep saved draft text and image warnings distinct. Never claim completion without the returned result.
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
