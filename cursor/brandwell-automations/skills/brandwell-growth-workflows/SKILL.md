---
name: brandwell-growth-workflows
description: "Plan a growth workflow from a goal: find a ready recipe, fill its choices from the project's real data, estimate the cost and create an editable draft. Use for 'set up the competitor customers workflow every Monday', 'find me leads like my best customers', 'what workflows do you have for X'. Any request to find new companies or people on a schedule starts here. To test, start or watch one use brandwell-growth-start."
requires-tools: workflows_plan_goal recipes_search workflows_from_recipe
allowed-tools: platform_capabilities account_plan_status recipes_recommended workflows_plan_goal recipes_search recipes_get recipes_request workflows_from_recipe workflows_set_choice workflows_estimate workflows_preview workflows_diff workflows_undo automations_registry automations_draft automations_update integrations_connect_link
metadata:
  title: "Plan a growth workflow"
  service: automations
  page: "#/automations"
---

# Plan a growth workflow

After `automations_update`, call `workflows_diff` and tell the person its rows word for word. `workflows_undo` requires the exact draft revision from a fresh `workflows_preview`; it restores the previous draft, never the live version. For an Adjust choice, send its `draft_revision` with `workflows_set_choice`. Changed or superseded choices cannot replace newer edits.

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Restate the goal and desired outcome. Read account_plan_status and, when offered, platform_capabilities. Never claim an unavailable product or connection is ready.

Read recipes.md in this skill for the outcomes and recipe keys. Call workflows_plan_goal or recipes_search first, with the person's goal in their own words; add constraints only for a budget, product or audience they named. Both use the Library's goal search. Prefer a ready recipe; explain missing setup before selecting one that needs it. Use a recipe as it is only when its steps do what the person asked and nothing more. When it adds work they did not ask for (sending, enrolling, messaging, a campaign or topic they never named), build the steps they asked for with automations_draft instead, taking what you need from the recipe's steps in recipes_get, and say what you left out. Read recipes_get and its choice_schema before filling typed choices. Preserve returned recipe version and verified starting context. Infer only from actual project data and the person's instructions. Ask at most three unresolved questions at a time. A displayed estimate per 100 records is not a spend authorization. Unknown estimates never count as free.

Estimate the draft or a validated spec with workflows_estimate. Explain the cost range, unknown prices, included work and approval steps. Create an editable draft with workflows_from_recipe using one stable request key. If needs_input includes a workflow_id, a safe unpublished draft exists; give its Start link and explain its unresolved problems. If no id is returned, no draft was created. Do not try to test or publish unresolved placeholders. If no recipe fits, read automations_registry and use only its supported keys with automations_draft. Offer recipes_request when the person wants BrandWell to add a missing workflow, and submit only their requested goal. Compare the returned summary with the person's goal.

Keep included data before paid sources, verify email before sending, put every send and CRM write behind approval, and preserve quiet hours. Never promise results. Never invent people, counts, sources, tool names, dates, observed performance or prices.

When offered, use workflows_set_choice to change one Start choice on the existing draft. Its returned choices and Start link reflect the page. Use verified option ids, never create a second draft to change a campaign or cadence. Say what Start offers from the returned choices, and hand the person the Start link.

Read recipes_recommended for the Home cards, reasons and actual ranking factors. After saving an unpublished draft, call workflows_preview to show the same reach, included data, paid estimate and proposed maximum as Home. Preserve unknown values and the returned estimated or demo basis. An estimate is never a prediction or spending approval. Give the returned Adjust link to continue the draft.

Working with the person:
- Go one step at a time and ask one question at a time (at most three unresolved at once when the recipe needs them). In the BrandWell Assistant, ask with ask_person, which shows the Question for you card; never put a question at the end of a reply.
- Always show the price before anything starts: call workflows_estimate and say the range, what is included and what needs approval. An estimate per 100 records is not a spend authorization.
- When the recipe needs something connected, call integrations_connect_link and give the person the link. Only they can connect it.
- When the Workflow Wallet is short for the estimate, load brandwell-wallet and give the add-funds link. Never say funds were added.
- To test, start or watch the workflow once the draft is ready, load brandwell-growth-start.
