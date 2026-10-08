---
name: brandwell-automation-approvals
description: "Approve, edit or skip what an automation holds for a person (an email, a postcard, a post, a connection request), and do the writing and judgment tasks workflows hand to the connected agent. Use for 'what is waiting for me', 'approve it', 'skip that one', 'edit the email before it goes'."
allowed-tools: automations_runs automations_decide automations_get automations_agent_tasks automations_agent_task_complete
metadata:
  title: "Approvals and agent tasks"
  service: automations
  page: "#/automations"
---

# Approvals and agent tasks

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

What is waiting:
- `automations_runs` with `status` waiting lists the runs waiting for a person. Each pending approval names its automation, step and what would be sent, mailed or posted, and has an `approval_id`. Read the proposed content to the person in plain words, by the step's label, before asking anything. Keep the `approval_id` for `automations_decide`.

Deciding:
- `automations_decide` approves, approves with edited content, or skips one pending approval. Use it only when the person gave an explicit decision for that approval, and pass their edited text as `content` when they changed it. Never decide an approval because it looks fine, and never decide several on one answer unless they named them.
- Like publishing, the decision is confirmed with the person on that exact call. In the BrandWell Assistant, get it with ask_person, `confirms` set to the exact `automations_decide` call, and say in the message what will go out. Their click on that card is the confirmation; then call the tool with exactly those arguments. Never ask them to type "yes": typed words are not a confirmation and the tool refuses them.
- After a decision, say what happened from the returned result: approved and sent on, edited and approved, or skipped.

Tasks for the connected agent:
- `automations_agent_tasks` lists the writing and judgment tasks workflows handed to you as the connected agent. Answer each with `automations_agent_task_complete`, putting each field the task asks for in `answer` with the type it names. Decline with a reason if you cannot, and AIMEE takes it. Sending and publishing still wait for the person's approval.

Rules:
- Report exactly what BrandWell returned. Keep every request scoped to the current BrandWell project.
- Sending, mailing, posting and spending always need the person's approval. To change what an automation does, load brandwell-automation-edit.
