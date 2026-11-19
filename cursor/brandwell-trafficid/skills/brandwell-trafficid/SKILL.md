---
name: brandwell-trafficid
description: "Read TrafficID's identified website visitors, one visitor's full detail and the site's form completions, score visitors against a saved ICP, and download the visitor list. Use when the person asks who visited the site, which companies or people are showing interest, who filled in a form, or whether a visitor fits their ICP."
allowed-tools: trafficid_get_visitors trafficid_get_new_visitor_count trafficid_get_visitor trafficid_qualify_visitor trafficid_list_form_fillouts trafficid_export_visitors trafficid_setup_get trafficid_setup_check trafficid_setup_provision trafficid_settings_get trafficid_settings_update marketpulse_list_icps account_plan_status onboarding_status onboarding_start_task
metadata:
  title: "BrandWell TrafficID"
  service: trafficid
  page: "#/trafficid"
---

# BrandWell TrafficID

Goal: tell the person who is visiting their website, what they looked at, and which visitors fit the buyers they want.

Workflow:
1. Call trafficid_get_visitors. Pass since for a time window the person gave ("this week"), and saved_icp_id to narrow to an ICP (read the ids with marketpulse_list_icps).
2. If the answer says TrafficID is not available (for example, the tracking tag is not installed or TrafficID is not set up for this project), say that plainly and stop. Do not guess visitors.
3. Summarize by company first, then people: company, number of visitors, the pages that signal intent (pricing, demo, product pages), and the latest visit.
4. To judge one visitor against an ICP, call trafficid_qualify_visitor with its visitor_id and report the score and the reasons it returned.
5. For everything about one visitor, as the visitor drawer shows it, call trafficid_get_visitor with its visitor_id.
6. For who filled in a form on the site, call trafficid_list_form_fillouts. It has the form, page, time and any attributed postcard campaign, not the submitted values.
7. When the person wants the visitor list as a file, call trafficid_export_visitors and give them the download_url. They open it while signed in, and the rows count toward the export allowance then.

Setting up the tracking tag:
1. Call trafficid_setup_get. If tracking is not on yet, call trafficid_setup_provision. The person approves it: the approval says "no extra cost, included in your plan". If TrafficID is not in the plan it creates nothing and returns a link: give it to the person to add TrafficID in BrandWell, then try again. Agents never create a billable property. If it says the project needs a domain, ask the person to add one in project settings.
2. Give the person project.tracking_code to paste before the closing head tag of every page of the site. If AIMEE is running on their computer, AIMEE can add it to the site files or theme with their OK.
3. Once it is added and published, call trafficid_setup_check. If it is not seen yet, say so, ask them to confirm the change is live, and check again.
4. To keep pages out of tracking, or to show visitors without a job title, use trafficid_settings_get and trafficid_settings_update.

Rules:
- For counts of newly recorded visitors between two timestamps, use trafficid_get_new_visitor_count with since and until. It reads retained, plan-admitted events without reading profiles or recording exports or usage. If complete is false, say "at least" before the count; if available is false, say the count is unavailable. This is newly recorded data, not proof of what someone viewed or a lifetime first visit.
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- Only the contact fields the tool returns may be shown. Never infer or look up personal details elsewhere.
- Reading and scoring never send outreach or mail. To follow up on visitors, hand off to the Outreach, Direct Mail or Automations skill.
- Plan status: call account_plan_status when the person asks when their plan renews or ends, or whether it is cancelled. Answer from its state, ends_at and renews_at exactly as returned, and if can_keep is true say they can reverse the cancellation with Keep My Subscription in Billing. Never guess a date.

Onboarding and the next workflow:
When onboarding_status is available, check script and visit evidence. Installation verification alone is not a captured visit. After the first real visitor arrives, suggest the next approved follow-up workflow for interested companies. Never invent identified visitors or replies.
