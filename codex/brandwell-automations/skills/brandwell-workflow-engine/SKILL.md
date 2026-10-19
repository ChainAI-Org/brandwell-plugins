---
name: brandwell-workflow-engine
description: "How BrandWell's workflow engine works, in every run: what a workflow is (trigger, steps, checks and branches, the Data provider order, outputs, runs), what it costs and how spend is capped, how to find and configure steps from the catalog, when to build a custom step or connect the customer's own tool, and how to start, read and share runs. Always loaded."
allowed-tools: automations_registry automations_list automations_get automations_get_graph automations_edit workflows_preview workflows_estimate workflows_outputs workflows_runs workflows_run_detail tools_search data_tools_search custom_steps_list connections_list
metadata:
  title: "The workflow engine"
  service: automations
  page: "#/automations"
  always_on: true
---

# The workflow engine

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Workflows are how BrandWell does work. Most requests end in one: build it, change it, run it, or read what it did. Reach for a workflow first; a single tool call is for a single lookup.

What a workflow is:
- One trigger: an event (a visitor, a reply, a delivery, a score), a schedule, an incoming webhook, another workflow, or a manual start. `automations_registry` lists every trigger, step, check and lookup this project can use, with what each input takes. Use only its keys.
- Steps in order, each acting on the run's record. Checks (an if/else on a field, a lookup or an AI yes or no question), switches and random splits branch the path. Every path ends at a step with nothing after it or at a stop.
- Data steps follow the Data provider order (Automations › Settings › Data provider order): sources are tried in order and the first hit wins, BrandWell's included source first, then the cheapest partner.
- Outputs: where a run's results go, for each way it can start: Show here, Download CSV, Google Sheet, Save to an audience, API response, Webhook, Post to Slack (`workflows_outputs`).
- Runs: every run, whatever started it (one person, a list, an audience, the API, an agent, a saved tool, a schedule, a webhook, a test), is in its Runs tab and in Workflows › All runs with its source, status and spend (`workflows_runs`, `workflows_run_detail`).

What it costs:
- Paid steps are charged to the Workflow Wallet. Partner data is charged at cost, with nothing added. Search research is at cost. AI steps cost nothing extra: they run on AIMEE, included, or on the customer's own model key.
- A source that costs BrandWell nothing is charged $0.0001 under the first paid option for the same lookup, and only for a match; a miss is free. The customer's own keys cost $0. On plans that include the Lead Database, its lookups are free.
- Say a workflow's price as "From $N per 100" and its unit: the workflow's lowest price, from the estimate or the recipe's cost hint. Never compute a price yourself, and never say "at most" or "up to" for a workflow's price. When the cost hint excludes Intent Scans, add: "Intent Scan price not included (varies by plan)." A run's approval quote is different: it is that run's amount, bounded by the customer's caps.
- The customer controls spend with a daily cap on any paid step and the Workflow cap, the workflow's daily spending limit. There is no per-lookup cap unless they set one. A paid workflow needs a finite Workflow cap before it is activated or an agent starts it. At a cap, paid steps hold, go on with included steps only, or pause, as the customer chose.

Building and changing:
- From a goal, start with a recipe (brandwell-growth-workflows); from a sentence, brandwell-automations. To change one that exists, branches included, read it with `automations_get_graph` and change it with `automations_edit` and its `draft_revision` (brandwell-automation-edit). Triggers are in brandwell-automation-triggers.
- To find a step, search with `tools_search`; for data, search the full Tools catalog with `data_tools_search` (its sorts and the Proven filter match the Tools tab). A data job joins a workflow as Run any data tool with the inputs it declares.
- When no step does it, build a custom step (brandwell-custom-steps): Combine steps, Call an API through a saved connection, an AI step with typed outputs, or a Transform. It passes a test before it is ready, then joins the workflow as a step.
- To use the customer's own tool: a saved connection (the person adds its key in Automations settings, Your keys; you never take, ask for or repeat a key) and a Call an API custom step. A CRM uses its own sync step, or sends to the workflow's incoming webhook trigger. Slack uses the Post to Slack step or output (brandwell-integrations).

Running and sharing:
- Test a draft first: a test sends nothing and spends nothing.
- Start an active workflow on one person or value, a list or an audience with `workflows_start_with`, or run a saved tool (both in brandwell-automation-runs); each is quoted and runs only after the person confirms. Read the result with `workflows_run_detail`. Watching, pausing and approvals are in brandwell-automation-runs and brandwell-automation-approvals.
- Share with the team, with people by email, or as a public page through brandwell-workflow-sharing.

Rules:
- Draft and change drafts freely. Activating, starting a run, sending, sharing outside the account and spending wait for the person's confirmation on the card.
- Name triggers, steps and outputs by their labels, never their keys.
