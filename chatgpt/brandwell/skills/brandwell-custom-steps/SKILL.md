---
name: brandwell-custom-steps
description: "Build a custom step when no BrandWell step does the job, and connect the customer's own tools: combine BrandWell steps, call the customer's API through a saved connection, an AI step with typed outputs, or a transform; test it, make it ready and add it to a workflow. Lists and tests saved connections without ever handling a key. Use for 'call our billing API in this workflow', 'score each lead with our rubric', 'add a step that does X', 'use my own AI model key for this step', 'is my API connection working'."
allowed-tools: custom_steps_list custom_steps_get custom_steps_draft custom_steps_create custom_steps_update custom_steps_test custom_steps_ready connections_list connections_test automations_registry automations_get_graph automations_edit
metadata:
  title: "Custom steps and connections"
  service: automations
  page: "#/project-settings/custom-steps"
---

# Custom steps and connections

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

First check that no BrandWell step already does it: read `automations_registry` and search the catalog. A CRM write is the CRM sync step, a Slack message is Post to Slack, a data lookup is a data job. Build a custom step only for what is left.

The four kinds, all built from a spec, never code:
- Combine steps: up to ten BrandWell steps that run in the portal, each reading the ones before it, with typed outputs. A step in it that sends makes the node wait for approval.
- Call an API: one request to the customer's own API through a saved Your API connection, on its own host, with typed outputs read from the reply.
- AI step: instructions with the inputs in them and typed outputs. It runs on AIMEE, included at no charge, or on an AI model connection with the customer's own key.
- Transform: a formula for each output over the inputs.

How to build one:
1. `custom_steps_list` shows what exists; reuse a ready step before building another.
2. Draft the spec from the person's words with `custom_steps_draft`, or write it yourself. Inputs name where each value comes from, such as the record's domain. Outputs are typed.
3. Save it with `custom_steps_create`. BrandWell checks it: no secrets in it, no loops, its size, and that its connection belongs to this project and answers at a public address. Fix what the problems say with `custom_steps_update`.
4. Test it on a sample record with `custom_steps_test`. A Call an API test calls the customer's API and an AI step on their own key uses that key, so those tests wait for the person's confirmation. Only a passing test of the current spec lets it be made ready; any change puts it back to draft.
5. Make it ready with `custom_steps_ready`, then add it to the workflow with `automations_edit`: an `add_step` with action `custom.run_step` and inputs `step_id` and `input` (the values for its inputs, such as a record field), after the step it follows. `custom_steps_get` returns that change for a ready step.
6. Say in plain words what it reads, what it returns and where it sits in the workflow.

Connections:
- `connections_list` shows the saved connections, each masked, with its status, last test and what uses it. `connections_test` tests one with its stored key; a webhook receives a test event and a data provider key may use its provider credit, so those wait for the person's confirmation.
- Only the person adds, replaces or removes a key, in Automations settings, Your keys: give them the link and say what to choose there. Never ask for a key, token or password, never put one in a spec, and never repeat one.

Rules:
- A step that tries twice and fails waits for a person; say so when it matters.
- Ask one question at a time. In the BrandWell app's chat, ask with ask_person, never with a question at the end of a reply.
- The step is the deliverable. Activating the workflow that uses it is separate and needs the person's confirmation.
