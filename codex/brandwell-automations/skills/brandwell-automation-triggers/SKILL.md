---
name: brandwell-automation-triggers
description: "Choose or change what starts an automation: a BrandWell event (a visitor, a reply, a meeting booked, a score, a delivery), a schedule such as every Monday, an incoming webhook, or another workflow. Says what must be installed or connected for the trigger to fire and gives the link. Use for 'when X happens', 'every Monday', 'trigger when someone books a meeting', 'how does this start'."
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
5. Set it. On a new draft, give it as `trigger` in the spec (brandwell-automations). On an existing one, read its graph with `automations_get_graph`, then change it with `automations_edit` and the op `set_trigger` (`event`, `filters`, `once_per`, `schedule`), which works on a branching automation too. Show the change in plain words, and ask before publishing.

Schedules (`platform.schedule`): ask how often, the time and the time zone, one question at a time. A schedule is `{ "every": "hour|day|week|month", "at": "09:00", "weekday": 1, "day_of_month": 1, "timezone": "America/Chicago" }`, where weekday is 0 for Sunday and Monday is 1. Give it as `schedule` in the spec, or with `set_trigger` on an existing automation. A scheduled automation cannot publish without one.

Webhooks (`inbound.webhook`): the address is created with the automation. Read it with `automations_get` (`inbound_webhook`) and tell only the person; anyone who has it can start the automation. Say what the other system must send: a POST to that address with the record's fields as JSON.

Filters and repeats:
- Put conditions about the trigger's own fields in `trigger.filters` with the registry's operators, such as `page_url contains "/pricing"`.
- Add `once_per` so one person or company does not run again inside a window, unless the person wants repeats. Ask the window in days.
- A company trigger keeps the company as its record, so a step that acts on a person cannot follow it; choose a trigger whose record is a person, and say so in one sentence.

Rules:
- Ask one question at a time. In the BrandWell Assistant, ask with ask_person, never with a question at the end of a reply.
- The draft is the deliverable. Publishing needs the person's confirmation of that exact call, through brandwell-automations. Keep every request scoped to the current BrandWell project.
