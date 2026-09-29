---
name: brandwell-trafficid
description: "Read TrafficID's identified website visitors, one visitor's full detail and the site's form completions, score visitors against a saved ICP, and download the visitor list. Use when the person asks who visited the site, which companies or people are showing interest, who filled in a form, or whether a visitor fits their ICP."
allowed-tools: trafficid_get_visitors trafficid_get_visitor trafficid_qualify_visitor trafficid_list_form_fillouts trafficid_export_visitors marketpulse_list_icps account_plan_status
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

Rules:
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- Only the contact fields the tool returns may be shown. Never infer or look up personal details elsewhere.
- Reading and scoring never send outreach or mail. To follow up on visitors, hand off to the Outreach, Direct Mail or Automations skill.
- Plan status: call account_plan_status when the person asks when their plan renews or ends, or whether it is cancelled. Answer from its state, ends_at and renews_at exactly as returned, and if can_keep is true say they can reverse the cancellation with Keep My Subscription in Billing. Never guess a date.
