---
name: brandwell-automation-triggers
description: "Choose or change what starts an automation: an uploaded list, an audience or Google Sheet (everyone now, then new people as they are added, daily, weekly or on chosen days), a run by hand, an app or agent, a BrandWell event (a visitor, a reply, a meeting booked, a score), or a schedule such as every Monday, Wednesday and Friday. Says what must be installed or connected and gives the link. Use for 'enrich this list', 'when X happens', 'every Monday', 'how does this start'."
allowed-tools: automations_registry automations_get automations_get_graph automations_edit automations_update integrations_status integrations_connect_link
metadata:
  title: "Triggers and schedules"
  service: automations
  page: "#/automations"
---

# Triggers and schedules

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Goal: find the one trigger that matches what the person said, tell them honestly whether it can fire today and what it needs, and set it on the automation.

How to choose:
1. Read `automations_registry` and look through its `triggers`. Every trigger is listed, including ones that cannot fire yet. Each has a `key`, a label, a `product`, the fields a filter may use, and `setup`: what must be installed, connected or set up for it to fire, in plain words, with a link. Use only keys it returned. Never invent one.
2. Match the person's words to the label and fields: "someone books a meeting" is the Outreach meeting trigger, "a lead score passes 80" is the score trigger, "every Monday" is `platform.schedule`, "when my CRM deal changes" needs the webhook or the CRM trigger the registry lists. Say which trigger you chose by its label, never its key.
3. When a trigger has `needs_code` true, it has no source yet. Say so plainly: the automation can be built and saved now and will start once BrandWell connects the source. Offer the nearest trigger that does fire, and ask which they prefer, one question.
4. When `setup` says something must be installed or connected, tell the person how, in one or two sentences, and give the link. For a connection that has a link, call `integrations_status` to see whether it is already connected, and when it is not, `integrations_connect_link` for the link. Only they can connect it. Never claim a trigger will fire when `setup` says its source is missing.
5. Set it. On a new draft, give it as `trigger` in the spec (brandwell-automations). On an existing one, read its graph with `automations_get_graph`, then change it with `automations_edit` and the op `set_trigger` (`event`, `filters`, `once_per`, `schedule`), which works on a branching automation too. Show the change in plain words, and ask before activating it or applying the changes.

How it starts, for work on people, companies, keywords or links the person gives it (enrichment, finding emails or mobiles, company and domain lookups, SEO keyword jobs, social profile jobs). Use `trigger.start` in the spec, or `start` with `set_trigger`; it sets the event and the audience filter, so leave those out. There are four ways, as the trigger shows them:
- Upload a list (`{"how": "list"}`): runs once on the list when it is activated. Pasted values go in `items` (emails, LinkedIn URLs, company websites, keywords, links), one run each. A CSV, Excel file or Google Sheet is uploaded in the trigger: say so and give the workflow's link.
- A sheet or audience (`{"how": "audience", "audience_id", "who", "cadence"}`): people or companies already in BrandWell. A Google Sheet stays in sync through an audience. `who` is `once` (everyone in it now, one time), `now_then_new` (everyone now, then people added later) or `new_only` (only people added after it is activated). For new people, `cadence` is `each` (as each one is added), `day` (once a day), `week` (once a week) or `custom` (chosen days of the week, or one day of the month). Daily, weekly and custom need a `schedule`; only people it has not run on yet run each time.
- Run once by hand (`{"how": "hand"}`): after it is activated, the person presses Run and gives one value. Good for trying a lookup on one record.
- From your app or agent (`{"how": "app"}`): an API call or a webhook starts each run.
Ask which way when the person did not say: a list they have, an audience that keeps getting new people, one at a time, or their own app. Ask for the audience by name, then use its id. When it repeats, ask how often, then the time and the time zone, one question at a time.

Schedules (`platform.schedule`): ask how often, the time and the time zone, one question at a time. A schedule is `{ "every": "hour|day|week|month", "at": "09:00", "weekday": 1, "day_of_month": 1, "timezone": "America/Chicago" }`, where weekday is 0 for Sunday and Monday is 1. The Custom repeat runs on chosen days: every day with `"weekdays": [1, 3, 5]` is Monday, Wednesday and Friday, and `[1, 2, 3, 4, 5]` is weekdays. Several times a day is every day with `"times": ["07:00", "12:00", "17:00"]` (up to 6). Every month with `"months": [1, 4, 7, 10]` runs only in those months. Give it as `schedule` in the spec, or with `set_trigger` on an existing automation. A scheduled automation cannot be activated without one. The trigger shows the dates it runs on a calendar, so point the person to it when they want to check.

Webhooks (`inbound.webhook`): the address is created with the automation. Read it with `automations_get` (`inbound_webhook`) and tell only the person; anyone who has it can start the automation. Say what the other system must send: a POST to that address with the record's fields as JSON.

Filters and repeats:
- Put conditions about the trigger's own fields in `trigger.filters` with the registry's operators, such as `page_url contains "/pricing"`.
- Add `once_per` so one person or company does not run again inside a window, unless the person wants repeats. Ask the window in days.
- A company trigger keeps the company as its record, so a step that acts on a person cannot follow it; choose a trigger whose record is a person, and say so in one sentence.

Rules:
- Ask one question at a time. In the BrandWell app's chat, ask with ask_person, never with a question at the end of a reply.
- The draft is the deliverable. Activating needs the person's confirmation of that exact call, through brandwell-automations. Keep every request scoped to the current BrandWell project.
