---
name: brandwell-connect-and-sync
description: "Inspect connected agents and native CRM status, configure existing signed event subscriptions, push records into BrandWell and inspect or replay deliveries. Use when the person wants to connect a RevOps bot, keep systems in sync or revoke an agent."
allowed-tools: agents_list_connections agents_revoke_connection agents_restore_connection crm_list_connections crm_list_lists sync_get_schema sync_push_records sync_list_subscriptions sync_set_events sync_list_deliveries sync_replay_deliveries automations_draft automations_registry
metadata:
  title: "BrandWell Connect and sync"
  page: "#/project-settings/agents"
---

# Connect agents and sync

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Read `agents_list_connections` before naming an agent connection and `crm_list_connections` before choosing a native CRM. Project scope comes from authentication. Do not invent a connection, audience, pipeline or field mapping. An expired connection needs the person to reconnect it.

Creating a project key or sync key, revealing its one-time secret, creating an event subscription and starting native CRM OAuth are person-only steps on the Connect page. Never ask for credentials in chat or put them in tool arguments. Give the person the page link and explain the needed step. An existing subscription can be found with `sync_list_subscriptions` and changed with `sync_set_events`; do not imply that choosing events creates a subscription.

For “connect our RevOps bot and alert me when a pipeline account shows intent”, name the person-only key/subscription setup first. Read existing subscriptions, add `pipeline.intent` only while preserving other events the person still wants, and read `automations_registry` before drafting a workflow using its supported `pipeline.match_found` trigger. Drafting is not publishing or starting. Report any missing Pipeline readiness and never invent a successful match or deal import.

Read `sync_get_schema` before pushing records. Preserve the source's stable external ID and source label. Up to 500 records fit a request. Report the returned created, updated, unchanged, deleted and rejected counts separately. A per-record rejection is not a successful batch import. The source label aimee is reserved for people AIMEE found; use brandwell-people-and-records for that. Pipeline writes remain unavailable until their adapter is released. A deleted object needs the person's explicit intent and stored human approval; a confirmation token alone is not approval. Retry the same confirmed execution after an uncertain outcome.

Revocation requires the server quote and human confirmation. You cannot revoke your own connection. Revoking stops future actions, while runs already started retain their run controls. Restore works within 24 hours only if the original owner still has access; otherwise direct the person to reconnect.

Delivery reads show safe receiver status and retry details. Replay only the delivery or seven-day window the person requested, preserving the event IDs while creating new delivery IDs. Do not use repeated replays as an automatic retry loop. Sync keys can see and change only their own subscriptions and cannot change project-wide defaults.

Native CRM writing uses the shared CRM action service when available. A connection read does not authorize a CRM write. All direct agent CRM writes require human confirmation, and exported records count toward export allowances. Until that action is available, report the missing capability rather than substituting an unrelated API call.
