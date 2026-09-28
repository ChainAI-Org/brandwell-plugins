---
name: brandwell-rankwell-content-plan
description: "Plan what to write next in RankWell: discover topic maps, choose topics, read and manage the prioritized content plan and its calendar, and turn a plan action into a brief or a draft. Use when the person asks what content to create or update, about their content plan or calendar, or to research topics."
allowed-tools: whoami list_rankwell_topic_maps discover_rankwell_topics select_rankwell_topic get_rankwell_plan save_rankwell_plan_action prepare_rankwell_plan_brief start_rankwell_plan_article get_rankwell_generation_job get_rankwell_article
metadata:
  title: "BrandWell RankWell Content Plan"
  service: rankwell
  page: "#/rankwell"
---

# BrandWell RankWell Content Plan

Goal: decide what to write or update next from measured evidence, and move the chosen work into the RankWell calendar, a brief or a draft, without publishing anything.

Workflow:
1. Call whoami, then get_rankwell_plan for the prioritized actions, equal-period Search Console changes, topic coverage and saved due dates. Missing report rows are not zero traffic.
2. For new topics, read list_rankwell_topic_maps first. Start discover_rankwell_topics only when the person asks for topic research and no fresh map covers it; it runs in the background and uses the research allowance, so read list_rankwell_topic_maps for its progress rather than starting another.
3. A cluster is shared intent only when the map compared it. Use select_rankwell_topic with an exact cluster from a finished map; it saves the primary keyword as a candidate and keeps its supporting phrases with the brief.
4. To schedule or track work, call save_rankwell_plan_action with an action_key read from get_rankwell_plan: add it to the calendar, change its due date or notes, or mark it in progress, done or dismissed.
5. When the person wants to proceed with an action, call prepare_rankwell_plan_brief and let them review the outline. Only when they ask for the draft, call start_rankwell_plan_article, then follow its job with get_rankwell_generation_job and read the finished draft with get_rankwell_article.

Rules:
- Overlap actions need an intent and canonical review before any merge; never merge, redirect or remove a page.
- Briefs and drafts use normal research and article credits; start them only when the person asks. Never start duplicate work to check status.
- Nothing here publishes. Report drafts as drafts, with their job status until they finish. To publish a finished draft, load brandwell-rankwell-content-studio.
