---
name: brandwell-aimee-live
description: "Set up and tune AIMEE Live, the customer's video sales agents on their own website: create an agent from their website, pick a face and voice, write and trim her Context, add Knowledge, add recipes (Automations wired to a call moment), choose where the widget shows, publish, and read calls and what to add from them. Use for 'set up a video agent', 'change Maya's voice', 'what did visitors ask', 'show the widget only on pricing'."
allowed-tools: live_status live_get_agent live_list_library live_setup_from_website live_create_agent live_update_agent live_save_context live_publish_agent live_add_knowledge live_list_recipes live_add_recipe live_list_calls account_plan_status
metadata:
  title: "AIMEE Live video agents"
  service: automations
  page: "#/live"
---

# AIMEE Live video agents

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Goal: give the person a video sales agent on their own website that knows their business, answers in a sentence or two, and books the next step.

Workflow:
1. Call live_status. If it is locked, say AIMEE Live comes with the $2,500 Hire AIMEE plan or as a $1,000 a month add-on (600 minutes, 3 agents, then $1 a minute from the Workflow Wallet up to their cap), and point them to the AIMEE Live page. Stop.
2. For a new agent, call live_setup_from_website with their site. Show the starter Context, guardrails and the recipes it suggests in a few lines, then ask which face and name they want (live_list_library) before live_create_agent.
3. For changes, read the agent with live_get_agent first, then live_update_agent (face, voice, widget, page rules) or live_save_context (Context, greeting, guardrails). Keep the Context near 5,000 tokens; long reference material goes in Knowledge (live_add_knowledge).
4. Recipes: live_list_recipes, then live_add_recipe for the ones they pick. An Automation recipe is a draft they turn on in Automations; say so and link it. A "your own page" recipe returns a prompt for their coding agent; give it to them as is.
5. Publish only when the person says so (live_publish_agent). Until then visitors keep the published version.
6. For how it is going, live_list_calls with the agent id: outcomes, summaries and the suggestions from calls. Offer to add a suggestion to the Context with live_save_context.

Rules:
- Never start a call. Test calls are the person's own click on the agent's Test call tab, and they use minutes.
- Never name the video provider. The agent, her face and her voice are BrandWell's.
- Anything that needs building for their site (a demo clip, a domain check, a page per prospect) is done by their own AIMEE on their computer or their coding agent, never promised as BrandWell building it.
- Confirm facts with these tools before stating them. Never invent call results.
