---
name: brandwell-people-and-records
description: "Look up the people already in the project: find one, read where they came from and what changed since yesterday, keep or release saved records, export records, and sync them to a CRM or push records in from another system. Use for 'who is this person', 'why is this person in my project', 'what is new since yesterday', 'sync these to HubSpot'."
allowed-tools: people_search people_get people_save people_unsave records_export enrich_list crm_list_connections crm_list_pipelines crm_sync_records sync_get_schema sync_push_records
metadata:
  title: "People and records"
  service: records
  page: "#/marketpulse/people"
---

# People and records

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Read people_search before choosing a person. An origin is the source that created the record, not every later source that enriched it. Use origin workflow and new_since 24h for the same view as Found by workflows with Show what's new. Keep a returned cursor with the same filters. The summary counts describe the whole project and are not the filtered result count.

Read people_get for current field status, provenance and timeline. Emails and phone values stay on the person page. Give the returned Open person link instead of trying another tool to reveal contact values. A missing value and a recorded failed lookup are different states. Do not claim a new enrichment or CRM sync happened from a read.

Use people_save when the person wants to retain existing records beyond the normal retention window; the saved-record allowance still applies. Use people_unsave only to release that marker. It does not delete the person or remove audience membership. Changes require the caller's stable idempotency key. Never retry a changed selection with a key from another operation.

Read crm_list_connections and crm_list_pipelines for current CRM destinations. A live connection does not authorize a write. Use crm_sync_records with exact saved person IDs and a stable request key. Direct CRM writes always require the shared server quote and stored human confirmation, including on AIMEE and MCP. Show its real count, operations, destination, and export meters before approval. A quote alone syncs nothing. Keep pending and partial outcomes explicit and use the returned run link; never claim that queued records have already synced.

When AIMEE finds people worth a conversation (a research spike, funding, hiring or a job change at an account that fits), push them with sync_push_records so they appear in the Opportunities from AIMEE audience. Do not create that audience; BrandWell makes it when the first find arrives. Send each person as type person with source aimee, external_id aimee:<your stable id for the find>, and whatever you know of first_name, last_name, title, email, linkedin_url and company with domain and name. A person needs an email, a LinkedIn URL, or a name with a company domain. Put fields.aimee_signal as one of research_spike, funding, hiring, job_change or other, and fields.aimee_reason as one plain sentence of at most 300 characters on why this person matters now. Set occurred_at to when you found them. Send up to 500 per call with one stable request key per batch, so a retry never repeats a batch. Pushing runs no paid lookup and sends nothing to anyone. Report the created, updated, unchanged and rejected counts, and name any rejected find and its code rather than calling the batch a success. Only AIMEE may use the aimee source.

Rules:
- Go one step at a time and ask one question at a time. In the BrandWell Assistant, ask with ask_person; never put a question at the end of a reply.
- Show the price before anything that spends: a column fill, a postcard, an export or a paid lookup. Name how many exports a call uses.
- When the Workflow Wallet is short, load brandwell-wallet and give the add-funds link. Never say funds were added. Keep every request scoped to the current BrandWell project.
