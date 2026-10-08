---
name: brandwell-integrations
description: "See what is connected (Slack, Discord, a CRM, Google Sheets, the TrafficID snippet, AIMEE, WordPress), give the person the link to connect what is missing, and send automation alerts to Slack or Discord with the record's name, company, title and a button to the person in BrandWell. Use for 'add a Slack alert to my hot accounts workflow', 'connect Slack', 'is HubSpot connected', 'send a test message'."
allowed-tools: integrations_status integrations_connect_link integrations_chat_connections integrations_test_chat_message automations_registry automations_get automations_get_graph automations_edit
metadata:
  title: "Integrations and Slack alerts"
  service: automations
  page: "#/project-settings/agents"
---

# Integrations and Slack alerts

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

What is connected:
- `integrations_status` reads each integration as connected, not_connected, needs_attention or unknown, with a `connect_url` for anything missing. It returns no credentials. Say plainly what is missing, never "it should work".
- `integrations_connect_link` returns the link for HubSpot, Salesforce, Pipedrive, Close, Slack, Discord or Google Sheets, and what the person does there. Connecting asks them to sign in and approve access, so only they can do it: give them the link and say so. Never ask for a token or password in chat.

Add a Slack or Discord alert to an automation (one step at a time, one question at a time; in the BrandWell Assistant ask with ask_person):
1. Find the automation (the page's, or by name) and read it with `automations_get_graph`. Read `automations_registry` and use the action `integration.chat_message` (Slack or Discord message).
2. Find where it posts. `integrations_chat_connections` lists the Slack and Discord apps connected through Outreach, each with a `connection_id`, and with a `connection_id` given, that connection's Slack channels. Ask which channel, offering the real ones.
3. When nothing is connected, there are two ways, and the person chooses: connect Slack (`integrations_connect_link` with `slack`, and give the link), or paste an incoming webhook address. A webhook address is a secret: the person types it into the step on the page, or you put it in the step's `webhook_url` input and never repeat it back; tools return it hidden. It must start with https://.
4. Add the step with `automations_edit` (`add_step`, action `integration.chat_message`, inputs `provider`, `connection_id` and `channel` or `webhook_url`, `message`, `style` card, `title`, `link`), after the step it should follow or on the branch it belongs to. A card shows the record's name, company and title with a button that opens the person in BrandWell; a plain-text line is sent where cards are not supported. Write the message with the record's fields, such as `{{first_name}} at {{company}} just asked about pricing.` Say what it will look like.
5. Offer a test with `integrations_test_chat_message` (give `workflow_id` and the step's `node_id`, or the webhook address). It posts a sample card to their channel, so do it only when they ask. Report the result as returned.
6. Show what changed in plain words, and ask before publishing (brandwell-automation-edit).

Rules:
- A step that sends to a channel waits for approval unless the person chose otherwise; say which. Never print a webhook address, token or key.
- Ask one question at a time. Keep every request scoped to the current BrandWell project.
