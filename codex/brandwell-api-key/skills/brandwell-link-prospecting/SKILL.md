---
name: brandwell-link-prospecting
description: "Find relevant public link and citation prospects for a verified BrandWell asset without sending outreach."
allowed-tools: link_builder_workspace link_builder_suggestions link_builder_sources link_builder_import link_builder_add link_builder_task link_builder_details link_builder_update link_builder_verify whoami explore_ai_prompt link_builder_network link_builder_publisher link_builder_contact link_builder_site_access link_builder_relationship_note link_builder_qualify link_builder_contact_for_placement link_builder_placement_context
metadata:
  writes: true
  title: "BrandWell Link Prospecting"
  service: link_builder
  page: "#/link-builder"
---

# BrandWell Link Prospecting

Goal: build a qualified prospect list and a truthful outreach angle for a page, tool, study, template, dataset, or expert point of view that deserves a reference.

Workflow:
1. Call link_builder_workspace and link_builder_suggestions. Prioritize GSC pages with traction, then Rankwell articles. A new article is a suggestion only; never start paid research merely because it exists.
2. Read link_builder_sources for saved AI-cited pages and backlinks. Import selected evidence with link_builder_import or record a known publisher with link_builder_add. If more research is needed, prepare a few specific listicle, alternative, resource, or digital PR searches for the user to review in Link Builder.
3. Qualify topical fit, audience, freshness, editorial responsibility and contact evidence. A domain contact is not automatically the author. Never invent an email or label an unverified address as verified.
4. Claim the due task with link_builder_task. Read link_builder_details and update the current version with link_builder_update. Respect campaign pauses, declines, suppression and the follow-up limit. Record replies, commitments and the next action before completing or snoozing the task. Complete a task only when its requested work is done; keep blocked work pending or snoozed with a concrete next action, and never contact a publisher again after the follow-up limit.
5. Draft the next publisher follow-up for approval. Link Builder preparation does not authorize sending, paid discovery, free-account grants or campaign enrollment. The user can set the offer later.
6. Use link_builder_verify to confirm the exact target link or brand mention. Inspect anchor, relationship attributes and retained history. Unavailable pages are not lost links. Never call a placement live without a successful verification. Follow up on a missing commitment, and coordinate a repair when a verified placement is lost or changed. A placement does not prove an AI citation or a ranking gain.
7. For publishers and people, read link_builder_network (search it by name, domain, topic or email) and link_builder_placement_context for one placement. Keep records current with link_builder_publisher, link_builder_contact and link_builder_site_access, log notes with link_builder_relationship_note, score a publisher 1 to 5 from evidence with link_builder_qualify, and attach a qualified contact with confirmed site access using link_builder_contact_for_placement. None of these sends a message, and enrichment alone never verifies an address or restores revoked access.

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
