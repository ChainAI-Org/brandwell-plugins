---
name: brandwell-integrations
description: "See what is connected (Slack, Discord, a CRM, Google Sheets, the TrafficID snippet, AIMEE, WordPress), give the person the link to connect what is missing, and post to Slack from a workflow: a Post to Slack step with the record's name, company and title and a button to the person in BrandWell, or a workflow's results posted to a channel. Use for 'add a Slack alert to my hot accounts workflow', 'post the results to #sales', 'connect Slack', 'is HubSpot connected', 'which Slack channels can it post to'."
allowed-tools: integrations_status integrations_connect_link slack_channels workflows_outputs workflows_set_outputs integrations_chat_connections integrations_test_chat_message automations_registry automations_get automations_get_graph automations_edit
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

Slack is one connection for the project (Project settings, Slack), on every plan. Post to it with the Post to Slack step or the Post to Slack output, one step at a time and one question at a time (in the BrandWell app's chat ask with ask_person):
1. Call `slack_channels`. It lists the channels BrandWell can post to. When Slack is not connected it says so and gives the link: give it to the person, since only they can connect it, and continue once they have.
2. Ask which channel, offering the real ones.
3. A message for each record: read the workflow with `automations_get_graph` and the step in `automations_registry`, then add it with `automations_edit`: `add_step` with action `integration.slack_post` and inputs `channel` (#name or its id), `message` written with the record's fields such as `{{subject.label}} at {{payload.company}} just asked about pricing.`, `style` card (the record's name, company and title with a button that opens the person in BrandWell) or plain, `title` and `link`. To reply in the thread of an earlier Slack step, give `thread_ts` that step's ts output. Put it after the step it follows, or on the branch it belongs to.
4. A run's results in a channel: `workflows_set_outputs` with `slack` in the targets for the way the workflow starts and `slack_channel`. `workflows_outputs` shows what is set now.
5. Say what it will look like and which runs it applies to, and ask before publishing (brandwell-automation-edit).

Discord, or a chat app reached only through an incoming webhook address, uses the `integration.chat_message` step: `integrations_chat_connections` lists the Slack and Discord apps connected through Outreach. A webhook address is a secret: the person types it into the step on the page; never repeat it. `integrations_test_chat_message` posts a sample to such a step's channel, only when the person asks.

Rules:
- Post to Slack posts to the team's own channel and runs without approval by default; set approval_required on the step when the person wants to review each post, and say which. Posting results to Slack, or changing where a live workflow's results go, needs the person's confirmation.
- Never print a webhook address, token or key. Keep every request scoped to the current BrandWell project.
