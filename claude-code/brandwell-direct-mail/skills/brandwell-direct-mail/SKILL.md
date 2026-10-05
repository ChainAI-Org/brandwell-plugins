---
name: brandwell-direct-mail
description: "Run postcard campaigns in BrandWell Direct Mail: list campaigns, draft a new one, set its schedule and safety limits, queue or remove recipients, suppress people, work on postcard concepts, activate, pause, resume or cancel a campaign, and read delivery and attribution. Use when the person asks about postcards, mail campaigns, what was mailed, or results."
allowed-tools: postcards_list_campaigns postcards_get_status postcards_create_campaign_draft postcards_update_campaign_settings postcards_queue_recipients postcards_cancel_recipient postcards_add_suppression postcards_set_campaign_state postcards_pause_campaign postcards_create_concept postcards_list_concepts postcards_get_concept postcards_revise_concept_artwork postcards_approve_concept marketpulse_list_feeds marketpulse_list_icps
metadata:
  writes: true
  title: "BrandWell Direct Mail"
  service: direct_mail
  page: "#/campaigns"
---

# BrandWell Direct Mail

Goal: help the person run postcard campaigns safely: find or draft the right campaign, keep its schedule and budget limits sensible, and report results honestly.

Workflow:
1. Call postcards_list_campaigns to find campaigns by name, status, source and schedule. Match the person's words to a returned campaign; if several match, ask which one.
2. For results, call postcards_get_status with the campaign_id: queued recipients, delivered, QR scans, identified visitors and attribution totals.
3. To start a campaign, call postcards_create_campaign_draft with a clear name and the source the person described (manual, TrafficID or intent), with saved_icp_id when they named an ICP (its name works too). For intent, source_id is the feed's feed_id from marketpulse_list_feeds; read it rather than asking. creative_id is an approved concept's current_proof.creative_id from postcards_list_concepts; when none is approved, leave it out and say the postcard is chosen later in Postcard Studio. Leave out settings the person did not give; BrandWell applies safe defaults. The draft cannot charge, print, mail or activate anything.
4. To change a draft or paused campaign's schedule or limits, call postcards_update_campaign_settings. Keep max_per_run, monthly_budget_cents and the duplicate window conservative unless the person set them.
5. For new postcard creative, call postcards_create_concept with a feed_id from marketpulse_list_feeds, a short headline, a supporting message and call to action, and plain visual direction. It creates an editable concept in Postcard Studio and starts its artwork; the person refines and approves it there.
6. To add people to an open manual campaign, call postcards_queue_recipients with only the people the person supplied or approved. An active campaign prints and mails queued people in its next batch, so the person confirms each call: in the BrandWell Assistant, call ask_person with confirms set to the exact call and say which campaign and how many people. A draft still needs a person's approval before anything mails. To take someone out of the queue before they are mailed, call postcards_cancel_recipient with the recipient id from postcards_get_status include_recipients.
7. When the person says never to mail someone, call postcards_add_suppression with their emails, company domains or phone numbers.
8. For existing creative, call postcards_list_concepts and postcards_get_concept. To change the artwork, call postcards_revise_concept_artwork with plain revision instructions, colors or font. Layout and text edits to the proof happen in Postcard Studio. When the person wants the current proof approved, call postcards_approve_concept with its creative_code; they confirm on a card.
9. To start a campaign, call postcards_set_campaign_state with state activate (a draft) or resume (a paused one). To stop one for good, use state cancel. Each waits for the person to confirm on a card, and only an account owner may activate or resume. To stop a campaign for now, call postcards_pause_campaign; it needs no card.

Rules:
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- Activating or resuming a campaign prints, mails and charges under its billing authorization. Do it only after the person confirms the card. Before you ask, check with postcards_get_status that the campaign, its creative and its limits are what they expect. The campaign data's agent_can_activate field is for AIMEE; in the BrandWell Assistant, use postcards_set_campaign_state.
- Cancelling cannot be undone. Offer postcards_pause_campaign when the person may want to restart.
- Creating a draft and changing its settings never mail anything by themselves. Say so when you do them.
- Never add recipients the person did not supply or approve.
- Report exactly what the tools returned, including suppressed, duplicate or undeliverable addresses.
