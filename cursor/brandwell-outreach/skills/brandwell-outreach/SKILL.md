---
name: brandwell-outreach
description: "Work with BrandWell Outreach: read email campaigns and what one campaign sends, continuous feeds and intake lists, add contacts to a tagged intake list, write or rewrite an email campaign as a saved draft, change a saved campaign's settings and emails, send a test, start, pause or resume a campaign, enroll chosen people, and create or switch feeds. Use when the person asks about their email campaigns, where contacts flow in, wants people added, or wants an email campaign created, rewritten, changed, tested, started or paused."
allowed-tools: outreach_campaigns outreach_campaign outreach_feeds outreach_intake_sources outreach_add_contacts outreach_workspace outreach_fields outreach_create_campaign_draft outreach_import_status outreach_import_contacts outreach_update_campaign outreach_update_steps outreach_send_test_email outreach_set_campaign_state outreach_enroll_preview outreach_enroll_confirm outreach_create_feed outreach_set_feed_state
metadata:
  writes: true
  title: "BrandWell Outreach"
  service: outreach
  page: "#/outreach"
---

# BrandWell Outreach

Goal: explain how contacts reach the person's email campaigns, add contacts where they asked, and change or run their campaigns as they ask. Nothing sends until the person confirms it.

Workflow:
1. Call outreach_campaigns for the email campaigns and their status (follow pagination.next_cursor for more).

Reviewing one campaign (its readiness, its emails, a follow-up for it): read it with outreach_campaign first; use the campaign the person has open, or the one they named from outreach_campaigns. Judge it on what it returned. Ready to start means it has emails, enabled senders, a sending window and a way for contacts to arrive (a feed mapping an intake tag to it, or leads); say what is missing. A follow-up builds on the emails it already sends: say what the next email adds, its wait and its subject, and draft it only when asked. Its results are empty until it has sent.

2. Call outreach_feeds for the continuous feeds, the saved ICPs and Intent Scans that feed them, and outreach_intake_sources for the tagged intake lists and their counts.
3. Explain the path plainly: an intake list's tag is mapped by a feed to a campaign; contacts in a list are not emailed until a feed maps its tag.
4. To add a few people, call outreach_add_contacts with a lowercase tag and up to 200 contacts per call. For a supplied lead list, use outreach_import_contacts: a source tag and at most 10000 contacts or 8 MB per page. BrandWell names each page for a safe retry when you leave request_id out; set queue=true to run a page of 500 or fewer as a background import too. Put job_title, seniority_level, department or company_employee_count in custom_fields when known; they are used for ICP matching. Read queued progress and every rejected row with outreach_import_status; a finished import is not proof of enrollment or sending.
   Contacts can be emailed once an enabled feed enrolls them, so an add or import to a tag an enabled feed reads needs the person's confirmation, and the tool says so when it does: then call ask_person with confirms set to the exact call, say which tag and how many contacts, and run it after their click. A tag no enabled feed reads only stores the contacts: when the person asked for them to be added, add them without asking first.

Drafting or rewriting a campaign (whenever the person wants campaign emails written, changed or saved, such as "rewrite my campaign with spintax"; a question about a campaign gets an answer, and you may offer a draft):
1. Call outreach_workspace for the campaigns, sender accounts, timezone and merge fields, and follow authoring.next_cursor with outreach_fields until it is null. Use only those exact merge-field tokens; never invent one.
2. Write the copy: each email's subject and body, with the merge fields, spintax and company-group branches below. Follow the brandwell-cold-email playbook and only facts the person supplied or the workspace shows: one offer and one clear call to action. When the person gives their own copy, or asks for a change to a campaign (read it with outreach_campaign first), keep their words and change only what they asked for, such as adding spintax. Prose alone creates nothing; the draft exists only once the tool saves it. Give optional personal fields a fallback, for example {{.FirstName | default "there"}}; custom fields use {{index . "job_title" | default "your role"}}.
3. Spintax is {option one|option two}: natural, meaning-preserving, never empty ({hello|} is invalid), never on factual claims, and never {{RANDOM|...}}. An option may be a merge field with a nonempty default, such as {Hi {{.FirstName | default "there"}}|Hello}; keep {{if}} template logic outside spintax. When the person asks for a number of variations ("5 to 10 ways"), give each spun phrase at least the smallest number they named; otherwise use three. The recipient-count IF below is template logic, separate from spintax. Keep merge-token braces intact. Never use em dashes anywhere; use a hyphen or other punctuation.
4. Defaults unless the person says otherwise: two emails three days apart, 06:00 to 18:00 every day (days 127; 31 is Monday to Friday) in the Outreach workspace timezone, and 20 emails per mailbox per day. Follow-ups wait at least one day. The workspace sets the timezone; if it is unavailable, ask before creating, and never promise another one.
5. Company grouping (multi_recipient true, max_recipients 2, 3 or 4) sends one shared To message to 2 to 4 people at a business domain, not separate emails and not CC or BCC. Set max_recipients to the largest group the person mentioned ("2 and 3 people" is 3); use 4 only when they said four or gave no size. The first email must branch three ways: {{if .MultiRecipient}}{{if eq .RecipientCount "2"}}two-person introduction{{else}}three-or-more introduction{{end}}{{else}}one-person introduction{{end}}, with each introduction written for its audience, not the same sentence with a different greeting: two people are addressed as a pair ("since you both look after..."), a larger group as a team ("for the three of you across..."), and one person directly. Do not repeat the introduction in follow-ups.
6. Human replies stop follow-ups; out-of-office replies do not. Return-date rescheduling (reschedule_ooo) is opt-in; when on, start every follow-up with {{.OOOFollowup}} and keep ooo_followup_text a neutral paragraph.
7. Use mailbox IDs only from the workspace and only ones the person chose. With none chosen, the draft uses all eligible senders ("rotate through all our mailboxes" means none chosen); tell the person to review senders before starting.
   Nothing missing blocks a draft, because a draft never sends: no connected mailboxes, no intake contacts and no feed are things to connect before starting it, so save the draft and list them. If a campaign with the same name already exists, change it with outreach_update_campaign and outreach_update_steps instead of saving a second one, unless the person wants a new one.
8. Call outreach_create_campaign_draft once. Before saving, BrandWell previews every email exactly as it will be sent: to one person, with missing data, to groups of 2, 3 and 4, and as an out-of-office follow-up. Claim a saved draft only from its result. The chat shows the draft's card with its schedule, senders and email previews, so do not list them again: say in a sentence that it is saved, not started or sent, and what it needs before it can start (senders, contacts, a feed). If the result is uncertain, retry the same call rather than creating another.
9. Existing running feeds for an intake tag can email imported contacts through active campaigns, so check where a tag leads before adding contacts to it. For webhooks, point the person to Outreach > Campaign sources and workflows > Contact sources; Project Settings > MCP creates the intake key.

Changing a saved campaign (read it with outreach_campaign first):
1. Settings: outreach_update_campaign with only what changes: name, description, daily limit, sending window and days, the workspace timezone, company grouping, out-of-office handling, or senders (mailbox_ids from outreach_workspace; an empty list rotates all eligible senders).
2. Emails: outreach_update_steps with each email to change by its number from outreach_campaign (1 is the first), and its new subject, body or wait_days. Write the copy as for a draft (steps 2, 3 and 5 above): the cold-email playbook, exact merge fields, the spintax rules and the company-group introductions. Every email is checked and previewed before anything is saved. Adding or removing emails is done in Outreach; say so.
3. Neither tool sends or starts anything. When a running campaign is changed, say that the change applies to emails it has not sent yet.

Testing, starting and pausing:
1. outreach_send_test_email sends one email of the campaign (step, from 1) to the addresses the person gives, up to five, from one of its senders or the mailbox they chose. Only those addresses receive it.
2. outreach_set_campaign_state starts a draft, pauses a running campaign or resumes a paused one. Check readiness first with outreach_campaign (emails, enabled senders, a sending window, contacts or a feed) and say what is missing. Outreach checks again and says why when it refuses; report its reason. Use acknowledge_list_risk only when the person read Outreach's bounce-risk warning and chose to start anyway.
3. Sending a test, starting and resuming send real email, so each needs the person's confirmation of that exact call: in the BrandWell Assistant, call ask_person with confirms set to the exact call and a message that says what will be sent to whom. Their click on the card is the confirmation; typed words are not. Pausing needs no confirmation.

Enrolling people and feeds:
1. To put chosen people into a campaign, call outreach_enroll_preview with the campaign, their emails and the source they are in (an intake list by its tag, TrafficID, form completions, stakeholders, Direct Mail or an Intent Scan). Report who can be enrolled, who is suppressed, invalid or already in it, anyone not found in the source, and whether it uses the export allowance.
2. Enroll them with outreach_enroll_confirm and the preview's enrollment_id, after the person confirms that call on a card. A running campaign emails them on its schedule; a draft sends nothing until it starts.
3. outreach_create_feed maps a source, optionally narrowed by a saved ICP, to a campaign and keeps enrolling new matching people each day; it is off unless enabled is true. outreach_set_feed_state turns a feed on or off. Turning on a feed into a running campaign emails real people, so it needs the person's confirmation; creating a feed that is off, or turning one off, does not.

Following up on engagement (an open, a click or a reply from a campaign, or an automation instruction for one contact):
1. An email open is inferred and does not prove the person read it. Conversation-level opens and clicks cannot identify which recipient engaged.
2. For a LinkedIn follow-up, find or verify the contact's LinkedIn profile from their name, company and business email domain. Explain any uncertainty and never guess an identity. Return the verified profile URL, brief identity evidence and a concise draft connection note, and ask the person to review the identity and approve any connection or message.
3. When an instruction asks for several actions (a like, a comment, a connection request), track which ones completed. Never repeat a completed one when continuing, and skip a conditional action when its condition is not met.

Rules:
- Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.
- A draft never sends and never starts a campaign. Sending a test, starting or resuming it, enrolling people and turning on a feed into it are separate steps, and each needs the person's confirmation first.
- Add only contacts the person supplied or approved, with their email.
- Adding contacts never sends email by itself; say whether a feed will pick up the tag.
- If Outreach is not connected for this project, the tools say so. Report it and stop.
