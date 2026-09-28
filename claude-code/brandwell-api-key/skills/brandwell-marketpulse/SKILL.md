---
name: brandwell-marketpulse
description: "Find in-market buyers with MarketPulse: build the ICP from who the client sells to, search buyer intent, read the newest buyers from the client's feeds, narrow them by a saved ICP, add, activate, refresh or pause intent feeds, download a feed's buyers, generate, read and share Demand Scans, and check plan usage. Use when the person says who they sell to, asks who is researching a topic, who is in market, about their feeds, ICPs, Demand Scans or MarketPulse limits."
allowed-tools: marketpulse_suggest_icp marketpulse_create_icp marketpulse_list_icps marketpulse_list_feeds marketpulse_get_usage intent_search intent_get_daily_buyers marketpulse_set_default_icp marketpulse_search_topics marketpulse_create_feed marketpulse_update_feed marketpulse_pause_feed marketpulse_export_audience marketpulse_list_demand_scans marketpulse_get_demand_scan marketpulse_generate_demand_scan marketpulse_demand_scan_link marketpulse_email_demand_scan
metadata:
  title: "BrandWell MarketPulse"
  service: marketpulse
  page: "#/reports"
---

# BrandWell MarketPulse

Goal: show the person which buyers are in market for what they sell, narrowed to the people they actually want, using only this client's MarketPulse data.

Setting up MarketPulse (a new customer, or "set up MarketPulse", "help me get started"):
Lead the setup yourself. The person should learn what an ICP is made of and that they can ask you for things, with as little typing as possible. Say one short line between steps; the cards do the work.
1. Call marketpulse_suggest_icp first. Ask nothing before it. Then say one short, warm line, like a person would, and never explain how you worked: "I had a look at acme.com." when basis is website, "I had a look at what you sell." for checkout_research or name_and_topics, "I looked at who's researching your topics." for topic_audience, nothing for none.
2. Call ask_person with the question marketpulse_suggest_icp returned, exactly as it is: its message and its requestedSchema. It walks the person through job titles, company size, industry and location, one at a time, with the guess already ticked. Do not change its fields, their order or its wording.
3. Save their answer with marketpulse_create_icp (icp parts, not description): roles = job titles; employee_min = the lowest chosen size's start and employee_max = the highest chosen size's end (none for "10,000 and over"); industries; locations = the chosen states (the values are state codes) or cities they added, and none when they kept "Anywhere in the US". Then say in one line: "Done. That's your ICP, under Saved ICPs at the top; change it any time."
4. Choose the first topic: call marketpulse_list_feeds. Ask one ask_person single choice (oneOf), "Which buying topic should we start with?", with the topic they bought first as the default and up to two more that fit their ICP from marketpulse_search_topics. Then start it: marketpulse_update_feed to activate and refresh it (the person confirms that card; it is a paid fetch). If they have no feed, marketpulse_create_feed first.
5. Finish in two lines: what happens now ("Your first audience is being found; it shows up on this page, usually within the hour") and three things they can ask you next, as short quoted examples tied to what they just set up, such as "Show me today's new buyers", "Make a postcard for these buyers" and "Email them with Outreach".
During setup, ask nothing else: no competitors, goals or budget. Never ask for something marketpulse_suggest_icp already guessed; show it ticked instead.

Workflow:
1. When the person says who they sell to (titles, company size, industry, location), build the ICP: call marketpulse_create_icp with their words as description. It saves the ICP as the default and fills the empty starting ICP. Then say the rules it made in one or two plain sentences, and name anything it returned in unmapped as not used, with the reason. When they ask to build their ICP but have not said who they sell to, ask that one question first: "Who do you usually sell to? Job titles, company size, industry and location all help." To show the rules before saving, pass preview true.
2. Call marketpulse_list_icps first when the person mentions a kind of buyer. Use a returned id as saved_icp_id. If they named an ICP that is not in the list, say so and show the names that are.
3. For "who is in market now" questions, call marketpulse_list_feeds, then intent_get_daily_buyers for the relevant topic_id, with saved_icp_id when they gave one.
4. For a topic or company the feeds do not cover, call intent_search with a short, specific query.
5. Report buyers as a short list: name, title, company, the topic they researched and when. Say how many there are and whether more pages exist (next_cursor).
6. For questions about limits or what is left this period, call marketpulse_get_usage. A null limit means unlimited.
7. To make a saved ICP the one MarketPulse filters by, call marketpulse_set_default_icp.
8. To watch a new topic, find its topic_id with marketpulse_search_topics and call marketpulse_create_feed; it starts as a draft that fetches nothing. To activate it, refresh it now, set how often it refreshes or change its lead cap, call marketpulse_update_feed. Activating, refreshing and a recurring schedule are paid fetches, so the person confirms those calls; a lead cap change needs no card. To stop it, call marketpulse_pause_feed.
9. When the person wants a feed's buyers as a file, call marketpulse_export_audience and give them the download_url. They open it while signed in, and the rows count toward the export allowance then.
   Pick the feed from marketpulse_list_feeds yourself when the request settles it: the one they named, the biggest by current_record_count when they asked for the biggest, or the only one with people. A feed with no people has nothing to export, so do not ask which empty feed to export: say none has delivered people yet and what would fill them, such as activating or refreshing a feed.
10. For Demand Scans, read them with marketpulse_list_demand_scans and marketpulse_get_demand_scan. Generate one for a website with marketpulse_generate_demand_scan; a website that already has one returns its scan id instead. For a link the person sends themselves, call marketpulse_demand_scan_link. To email it to someone, call marketpulse_email_demand_scan; the person confirms first.

Rules:
- Everything is scoped to the current client. Never combine or compare another workspace's buyers.
- Report exactly what the tools returned. An empty result is an answer: say there are no matching buyers yet and suggest the next useful step, such as widening the ICP or checking the feed's next refresh.
- Reading buyers never contacts them. To act on buyers, hand off to the Outreach, Direct Mail or Automations skill.
- Spend and sends wait for the person's confirmation card: activating, refreshing or scheduling a feed, and emailing a Demand Scan.
