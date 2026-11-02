---
name: brandwell-rankwell-content-plan
description: "Plan what to write next in RankWell and work the topic map: its topics, ranking drops, Cleanup, Up next, comments and Activity, and the site changes AIMEE on a computer makes. Also discover topics, manage the prioritized content plan and its calendar, and turn a plan action into a brief or a draft. Use when the person asks what content to create or update, about their topic map, drops, Cleanup, content plan or calendar, or to research topics."
allowed-tools: whoami list_rankwell_topic_maps discover_rankwell_topics select_rankwell_topic get_rankwell_plan save_rankwell_plan_action prepare_rankwell_plan_brief start_rankwell_plan_article get_rankwell_generation_job get_rankwell_article account_plan_status get_rankwell_map get_rankwell_map_health decide_rankwell_cleanup set_rankwell_map_topic research_rankwell_map_topic get_rankwell_month_plan change_rankwell_month_plan add_rankwell_month_plan_article focus_rankwell_month_plan answer_rankwell_map_comment get_rankwell_activity list_rankwell_site_work assign_rankwell_site_work report_rankwell_site_work
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
6. The topic map adds two kinds of items to get_rankwell_plan's planned list. Drop fixes (evidence.source map_drop, with fix refresh, faq or answer) are refreshes RankWell writes on their due dates in Up next; leave them unless the person asks. Cleanup tasks (evidence.cleanup) are site work, below.

The topic map (when a tool says the new topic map is not on for this project yet, the project still has the plan above, so use it):
7. Read the map with get_rankwell_map: topics (planets), sub-topics (moons), counts, rising keywords and open comments. Give node_id for one topic with its children and keywords, or search to find one. Read ranking drops, Cleanup and this week's changes with get_rankwell_map_health, the month's writing plan with get_rankwell_month_plan, and what ran and what it cost with get_rankwell_activity.
8. Change the map only when the person asks: set_rankwell_map_topic keeps, holds, skips, reactivates or renames a topic; change_rankwell_month_plan and add_rankwell_month_plan_article change Up next; focus_rankwell_month_plan puts a rising keyword at the front of a month, and undoes it. Writing an article uses one article credit, and nothing is published.
9. research_rankwell_map_topic adds a topic. Research over $2.50 from the Workflow Wallet answers needs_approval: tell the person the estimate, and call again with confirmed_cost_usd only once they accept it.
10. Answer comments on the map with answer_rankwell_map_comment; a comment is a question for you about that topic. Resolve one only when it is answered or the person asks.
11. Cleanup: decide_rankwell_cleanup with give makes Cleanup pages your tasks. Pages marked needs_ok wait for the person's OK: ask them in plain words what will change on their site, and call approve only after they say yes. keep leaves a page as it is.

Site work (changes on the live website):
12. You change the site only as AIMEE on the person's computer, never as AIMEE in the BrandWell app. In the app, hand each change to AIMEE on the computer with assign_rankwell_site_work: a Cleanup task by its action_key from list_rankwell_site_work, or a new job with a title, the page and step-by-step instructions (a redirect, internal links, a fix a page needs). It is refused when no computer is signed in to the project; then tell the person to open the AIMEE app on their computer and sign in to this project.
13. On the computer, read list_rankwell_site_work and do the jobs that are ready, one at a time. Call report_rankwell_site_work with started when you begin, done with a one-line summary once the change is live, or blocked with what stopped you. Never do a job whose ready is false.

Rules:
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- Merge, redirect or remove a page only for site work that is ready, and only as its instructions say. A merge keeps the best content, adds a 301 redirect from the old URL and updates internal links; never delete content without the person's OK. Other overlap actions need an intent and canonical review first, and are never merged on your own.
- Briefs and drafts use normal research and article credits; start them only when the person asks. Never start duplicate work to check status.
- Nothing here publishes. Report drafts as drafts, with their job status until they finish. To publish a finished draft, load brandwell-rankwell-content-studio.
- Plan status: call account_plan_status when the person asks when their plan renews or ends, or whether it is cancelled. Answer from its state, ends_at and renews_at exactly as returned, and if can_keep is true say they can reverse the cancellation with Keep My Subscription in Billing. Never guess a date.
