---
name: brandwell-automation-edit
description: "Change an automation that already exists: add, remove, move or change a step, add an if/else, a switch or a random split, add a Slack alert, or change what a step does. Reads the workflow, applies the change, shows what changed and asks before publishing. Use for 'edit', 'change', 'add a step', 'add a branch', 'remove the email step'. To start a new one use brandwell-automations."
allowed-tools: automations_get automations_get_graph automations_edit automations_update_graph automations_update automations_registry automations_test_run automations_publish workflows_diff workflows_undo workflows_preview
metadata:
  title: "Edit an automation's steps"
  service: automations
  page: "#/automations"
---

# Edit an automation's steps

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Goal: make the change the person asked for on the workflow they named, show them what changed, and leave publishing to them.

How to edit:
1. Find the workflow. When the page has one open, that is the one. Otherwise read the person's words against `automations_get` or the list the setup skill reads; ask which one only when two match.
2. Read it with `automations_get_graph`. It returns every node with its id and label, every path, an `outline` in plain words, and the `draft_revision`. Read `automations_registry` before adding a step, and use only the action keys it returned.
3. Change it with `automations_edit` (small changes) or `automations_update_graph` (the whole graph). Both take the `draft_revision` you last read and refuse a draft that changed since: read it again and redo the change. Each answer returns the new `draft_revision`, the `summary` and `problems`.
4. Show the result before you move on: `workflows_diff` after `automations_update`, and for a graph change the returned `summary`, in plain words, naming each step by its label and never its key or id. Say what changed, what stayed and what it now does on each path.
5. Test it when the person is unsure (`automations_test_run`). Publishing is separate: `automations_publish` only when they say publish or turn it on, and it needs their confirmation of that exact call. Never say an edit is live until the tool confirmed it.

Step edits (`automations_edit`, ops applied together or not at all, up to 25):
- `add_step` puts an `action`, a `check` (an if/else) or a `stop` after a node (`after`) on one of its outcomes (`when`). Left out, `after` is the end of the straight line. A step added to a path that already continues is inserted and the old way carries on after it. An if/else inserted that way keeps the old way on yes and ends the run on no.
- `remove_step` takes a step out and joins its neighbours. `move_step` puts an existing step after another node.
- `set_step_inputs` changes a step's inputs (null removes one; `replace` swaps them all), or an if/else's own check (key, operator, value, prompt). `approval` and `on_error` change how the step waits and fails.
- `set_trigger` changes what starts it: `event`, `filters`, `once_per` and, for a scheduled automation, `schedule`. brandwell-automation-triggers says how to choose one.
- A new node gets an `id` you choose, so a later op in the same call can name it.

Branches in a graph:
- An if/else is a condition node with edges `true` and `false`. A switch is `logic.branch` with `kind` switch (by value) or ai_switch (by an AI question), one `label:<case>` edge per case and `label:default` for the rest. A random split is `logic.random_split` with `percent`, edges `true` and `false`. A check can also ask AI a yes or no question (`{"field": "ai", "prompt": "..."}`).
- Every path should end at a step with nothing after it or at a stop. Say so when a branch ends the run.
- To start a branching automation from nothing, draft its first steps with `automations_draft` (brandwell-automations), read it with `automations_get_graph`, then add the branches here.

Rules that hold on every edit:
- Name campaigns and ICPs as `{ "name": "..." }`, never guess an id. A step that sends, mails, posts or spends waits for approval unless the person chose otherwise; say which steps run without approval.
- `limit` on an edit saves the workflow's spending limit with it. Paid steps need a finite limit: ask which amount, one question at a time, and show the price first (workflows_estimate in brandwell-automations).
- A step that needs a connection (Slack, a CRM) needs it connected first: load brandwell-integrations, which also has the Slack alert steps.
- Read the returned `problems` and fix what you can settle yourself, then say in one sentence what you changed. Ask only about real ambiguities, one question at a time. In the BrandWell Assistant, ask with ask_person, never with a question at the end of a reply.
- Undo needs the current `draft_revision` from `workflows_preview`; it restores the prior draft and never the live version.
- The draft is the deliverable. Publishing, running, resuming, archiving, sending and spending need the person's explicit request, and the tools that do them ask for their confirmation. Keep every request scoped to the current BrandWell project.
