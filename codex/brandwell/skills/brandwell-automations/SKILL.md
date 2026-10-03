---
name: brandwell-automations
description: "Turn a person's sentence into a BrandWell Automation draft they can review, then publish and run it with their approval. Also read one automation in full, test it, run it now on a record, pause, resume or archive it, and retry, skip or stop a run."
allowed-tools: automations_registry automations_draft automations_update automations_publish automations_list automations_runs automations_decide automations_get automations_set_state automations_test_run automations_run_now automations_run_action
metadata:
  title: "BrandWell Automations"
  service: automations
  page: "#/automations"
---

# BrandWell Automations

Goal: turn what a person says should happen automatically into a BrandWell Automation: one trigger, the conditions that narrow it, and steps in the order they described, created as a draft they can open in the builder, and published only when they say so.

Workflow:
1. Call automations_registry first, every time, before composing anything. It returns the triggers, condition fields, lookups and actions this project can use (each with key, label and product; actions also carry inputs, outputs, tags, done_by and aimee_instructions) and the names BrandWell can resolve (outreach_campaigns, direct_mail_campaigns, saved_icps). Use only keys it returned. Never invent a trigger, lookup or action key, and never use a product the registry did not list.
2. Choose exactly one trigger: the event that starts the automation. "Identified leads that visited the pricing page" is trafficid.visitor.page_viewed. Put conditions about the trigger's own fields in trigger.filters using the registry's operators (page_url contains "/pricing"). Add once_per so one person or company is not run again inside a window unless the person wants repeats.
3. Add conditions for everything else the person required. Use kind "field" for more of the trigger's fields, kind "lookup" for another product's answer through one of the registry's lookups (trafficid.visited_page with a pattern, marketpulse.matches_saved_icp with args { "icp_id": { "name": "..." } } or no args when any saved ICP will do, outreach.in_campaign, direct_mail.mailed_recently), and kind "ask_ai" only for a judgement no field or lookup covers, phrased as a yes or no question.
4. Write the steps in the order the person said them. Prefer the native product action whenever the registry has one. A native product action is a non-AIMEE product action: outreach.*, direct_mail.*, link_builder.* and the other products' actions, such as outreach.enroll_contacts and direct_mail.mail_postcard. Anything the products cannot do natively becomes one aimee.* step, with an instruction that contains the person's own words in quotes, says exactly what to do and what not to do, and uses personalization fields, written as {{first_name}}, {{last_name}}, {{company}} or {{title}}, so each run is personal. Keep every placeholder as written; BrandWell substitutes them for each record. Give an aimee.* step executor.seat "record_owner" and mode "review" unless the person named who does it or asked for it to run without review.
   Choose an aimee.* action by what AIMEE will do, as its aimee_instruction in the registry says, not by channel words such as "LinkedIn" or "send" in its label:
   - aimee.write_and_send always writes a message and sends it. Use it only when the person wants a written message sent.
   - A connection request without a note, a profile visit, a like or a follow goes in aimee.ask.
   - Engaging with a SocialStreams post goes in aimee.engage_social_result.
   Every step acts on the record the trigger starts the run on (see "Records and people" below). Build the first draft so it already fits:
   - New people from MarketPulse into an Outreach campaign: use the recipe below (marketpulse.batch.delivered, then marketpulse.enroll_in_outreach_campaign). Do not put outreach.enroll_contacts after a feed trigger.
   - A company trigger (trafficid.company.surge, marketpulse.account.matched, trafficid.stakeholders.ready) keeps the company as its record, and no step changes it, so a person step after it cannot run. Choose a trigger whose record is a person instead, and say so in one sentence.
5. Approval: set approval "approval_required" on the automation, or on each step tagged sends or spend (enrolling, mailing, posting, connection requests), unless the person said sends may go out on their own. Reads, research and drafting can be "auto". When the person says steps may run without approval, set approval "auto" on those steps (or on the automation): BrandWell keeps that choice and lists them as runs_without_approval, so say which steps run on their own. A sending or spending step left to inherit under an automation that is not "auto" is set to "approval_required" for you.
6. Name things instead of guessing ids: { "campaign_id": { "name": "XYZ Outreach" } } and { "icp_id": { "name": "Enterprise buyers" } }. BrandWell resolves them and reports anything ambiguous or missing as problems.
7. Call automations_draft with the spec. Read back name, summary, steps, builder_url and problems. After automations_draft or automations_update, read the returned summary against the person's own words. If a step would do anything they did not ask for, or ruled out (a note they said not to write, a message they did not want sent), fix it with automations_update before you reply. Tell the person what you built, step by step, in plain words, naming each trigger and step by its label, never its key. In the BrandWell Assistant the draft's card opens it in the builder, so never paste the builder_url; elsewhere, give them the builder_url to review it. Fix a problem you can settle yourself (a typo in a name, a field the registry spells differently, a step a problem offers that the person's goal needs, such as the delivery version of a person step after a MarketPulse delivery trigger) with automations_update, then say in one sentence what you changed. Ask the person only about real ambiguities: a name with several options, a campaign that does not exist, a step you could not map to any action. In the BrandWell Assistant, ask with ask_person (a oneOf choice with the options the problem lists), never with a question at the end of your reply.
8. Publish with automations_publish only when the person says to publish, turn it on or make it live, and report the returned version and status. BrandWell refuses to publish while problems remain, so resolve them first. Never publish on your own initiative, and never say an automation is live until the tool confirmed it.
9. Publishing and deciding an approval need the person's confirmation of that exact call. In the BrandWell Assistant, get it with ask_person: set confirms to the exact call, for example { "tool": "automations_publish", "arguments": { "workflow_id": "<the draft's workflow_id>" } }, and say in message what will go live. The person's click on that card is the confirmation; then call the tool with exactly those arguments. Never ask them to type "yes" or a confirmation: typed words are not one, and the tool refuses them.

Runs and approvals:
- automations_list shows the project's automations with status, trigger, products and approval mode. When the person asks what automations they have, list every one it returned by name, with its status and trigger label. automations_runs shows recent runs with status, waiting_on, subject and pending approvals. Report what each run is waiting on, and name anything waiting for a person by its automation and step; keep its approval_id for automations_decide.
- automations_decide approves, approves with edited content, or skips one pending approval. Use it only when the person gave an explicit decision for that approval, and pass their edited text as content when they changed it. Never decide an approval because it looks fine. Like publishing, the decision is confirmed with ask_person, confirms set to the exact automations_decide call.

Controlling an automation:
- automations_get reads one automation in full: status, steps with their approval modes, its spec, the live version and earlier versions. unapproved_send_steps lists the steps that would send, spend or act for the person without waiting for approval.
- automations_test_run runs the current draft as a test against the latest matching event, or an event_id, or a subject and payload. A test has no side effects; report the trace step by step, by each step's label. Test before publishing when the person is unsure.
- automations_run_now runs it for real on one record (subject). When it has unapproved_send_steps, confirm that exact call with ask_person first.
- automations_set_state pauses a live automation, resumes a paused one, or archives one, which stops its open runs. Resuming and archiving need the person's confirmation on a card; pausing does not.
- automations_run_action retries the step a run is paused on, skips it, or stops the run. Name the run from automations_runs.

Example. The person says: "I want TrafficID identified leads that visited the pricing page and fit one of our saved ICPs from MarketPulse to be enrolled into the XYZ Outreach campaign, sent a postcard through the Direct Mail campaign ABC, then have AIMEE visit their LinkedIn profile, engage their latest content and send a connection request with a personal note."
After reading the registry, the spec is:
{
  "name": "Pricing page visitors in an ICP: Outreach, postcard, LinkedIn touch",
  "approval": "approval_required",
  "trigger": {
    "event": "trafficid.visitor.page_viewed",
    "filters": [
      {
        "field": "page_url",
        "operator": "contains",
        "value": "/pricing"
      }
    ],
    "once_per": {
      "subject": "person",
      "window_days": 90
    }
  },
  "conditions": [
    {
      "kind": "lookup",
      "lookup": "marketpulse.matches_saved_icp"
    }
  ],
  "steps": [
    {
      "action": "outreach.enroll_contacts",
      "inputs": {
        "campaign_id": {
          "name": "XYZ Outreach"
        }
      }
    },
    {
      "action": "direct_mail.mail_postcard",
      "inputs": {
        "campaign_id": {
          "name": "ABC"
        }
      }
    },
    {
      "action": "aimee.ask",
      "approval": "approval_required",
      "executor": {
        "seat": "record_owner",
        "mode": "review"
      },
      "inputs": {
        "instruction": "The person asked: 'have AIMEE visit their LinkedIn profile, engage their latest content and send a connection request with a personal note.' Find {{first_name}} {{last_name}} at {{company}} on LinkedIn. Read their latest post and leave a short, specific comment that adds something useful and does not pitch. Then send a connection request with a personal note under 300 characters that mentions what they looked at on our pricing page. Draft the comment and the note for review before anything is posted."
      }
    }
  ]
}
Then: create the draft, read back the summary and problems (an ABC campaign that matches two Direct Mail campaigns comes back with options; ask which one), point them to the draft to review (the builder_url outside the BrandWell Assistant), and publish only when they say so.

Each step acts on the record the trigger starts the run on, from the first step to the last. No step changes that record: trafficid.find_stakeholders returns people as a list output, and the run still acts on the company. So a person step (outreach.enroll_contacts, direct_mail.mail_postcard, aimee.write_and_send) needs a trigger whose record is a person. When a problem says a step acts on a person but the automation runs on something else, use the option it offers; never put a stakeholder step in front of a person step to fix it.

Recipe: follow up with new people from MarketPulse through an Outreach campaign ("follow up with new MarketPulse buyers using my Q3 campaign", "enroll each new intent batch in Outreach").
- The trigger is marketpulse.batch.delivered (New intent records delivered), with the filter new_people gt 0. Its record is the delivery, not a person. MarketPulse delivers people with their emails, so no stakeholder lookup is needed.
- The step is marketpulse.enroll_in_outreach_campaign (Enroll delivered people in an Outreach campaign) with the campaign named. It enrolls everyone in the delivery, up to 2,000 a run, and skips people already in the campaign, suppressed or without an email. Never follow this trigger with outreach.enroll_contacts.
- Choose the MarketPulse step by what the person names. They name an Outreach campaign ("my Q3 campaign", "enroll them in", "follow up with them"): marketpulse.enroll_in_outreach_campaign with campaign_id, which puts the people in that campaign's sequence. They name an Outreach intake list, source or tag ("add them to my intent-leads list", "tag them abm-intent"): marketpulse.send_to_outreach with source_id, which only adds them to that list and enrolls no one; a feed set up in Outreach decides whether that list goes into a campaign. When they name neither, ask which campaign.
- For a postcard to each delivered person, the step is marketpulse.send_to_postcard_campaign.
- When the person said it runs without approval, set approval "auto" on the automation.
{
  "name": "New people from MarketPulse to the Q3 campaign",
  "approval": "auto",
  "trigger": {
    "event": "marketpulse.batch.delivered",
    "filters": [{ "field": "new_people", "operator": "gt", "value": 0 }]
  },
  "steps": [
    {
      "action": "marketpulse.enroll_in_outreach_campaign",
      "inputs": { "campaign_id": { "name": "Q3 launch" } }
    }
  ]
}

Rules:
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- Keep every request scoped to the current BrandWell project. Never request, combine or reveal another workspace's automations, runs, campaigns or people.
- The draft is the deliverable. Creating, updating and testing drafts is allowed. Publishing, deciding approvals, running, resuming, archiving, sending, mailing, posting and spending require the person's explicit request, and the tools that do them ask for the person's confirmation.
- Report exactly what BrandWell returned. If a tool failed or returned problems, say so; never claim a draft, publish or decision succeeded without the returned result.
