---
name: brandwell-pipeline-match
description: "See which open deals, customers and closed-lost deals have people researching your topics, alert the deal owner, and queue new contacts for the CRM. Use when the person asks which deals are heating up, who at a deal is researching, or to send deal data to Pipeline."
allowed-tools: pipeline_summary pipeline_list_deals pipeline_get_deal pipeline_alert_owner pipeline_add_to_crm pipeline_deliver_contact pipeline_update_settings pipeline_set_automation pipeline_list_sources pipeline_connect_native pipeline_sync_now pipeline_upsert_deals pipeline_list_updates pipeline_ack_updates crm_list_connections crm_list_pipelines crm_sync_records people_get
metadata:
  title: "BrandWell Pipeline"
  service: marketpulse
  page: "#/market"
---

# BrandWell Pipeline

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Read pipeline_summary first. It shows the tiles, the last sync, the matching settings and which ways of sending deals are available. With no source connected there are no deals, so say that and offer pipeline_connect_native where it is available, or a webhook. Do not claim a way is ready when the summary says coming_soon.

Read pipeline_list_deals for the ranked deals and pipeline_get_deal for who researched. These reads never return email addresses or phone numbers, so do not try to reveal them. A deal appears only while someone at its account researches a topic, and an identity match alone is not research.

pipeline_alert_owner and pipeline_add_to_crm always need a person to approve the quote. Show its summary word for word. An alert emails the owner when they are on the team and queues a CRM task for the CRM agent. pipeline_add_to_crm queues new contacts and an intent note; it never writes to a CRM itself. For a deal read from a connected CRM, use crm_sync_records with that deal and the operations upsert_contact and add_note, which has its own quote.

pipeline_deliver_contact returns the contact details of people queued by pipeline_add_to_crm, only after a person approves its quote; each person uses one export once per period. Use it to create the contact in the CRM, then report it with pipeline_ack_updates.

The agent way: pipeline_upsert_deals pushes up to 500 flat deals, pipeline_list_updates lists what is waiting for the CRM, and pipeline_ack_updates reports each as done or failed. Write each update to the CRM only as listed, then acknowledge it once. These three are offered only when the agent way is on.

pipeline_update_settings and pipeline_sync_now change matching and re-read a source; every change needs a stable idempotency key. A failed sync keeps the existing deals. pipeline_set_automation turns the owner alert workflow on only after the person approves. With nothing linked it installs the Pipeline owner alert recipe, which has no paid steps; a linked draft workflow must be started with workflows_start first.

Never invent deals, amounts, owners, people or counts. Report the structured error when a call fails.
