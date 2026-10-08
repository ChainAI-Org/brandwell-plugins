---
name: brandwell-automation-runs
description: "Run and watch automations: list what exists and what is failing, read the runs, test a draft, run one now on a record, pause, resume or archive it, find out why a run failed, and retry, skip or stop a run. Use for 'what automations do I have', 'pause everything that is failing', 'why did my enrichment workflow fail yesterday', 'run it now', 'test it'. Approvals have their own skill, brandwell-automation-approvals."
allowed-tools: automations_list automations_get automations_runs automations_test_run automations_run_now automations_set_state automations_run_action workflows_home workflows_flow workflows_step_people
metadata:
  title: "Run and monitor automations"
  service: automations
  page: "#/automations"
---

# Run and monitor automations

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

What exists and how it is doing:
- `automations_list` shows the project's automations with status, how each starts, its next run, the last run's outcome and the failed runs this week. When the person asks what automations they have, list every one it returned by name, with its status and trigger label. Filter by status to find what is failing or paused.
- `automations_runs` shows recent runs with status, `waiting_on`, subject and pending approvals. Report what each run is waiting on, and name anything waiting for a person by its automation and step. Read a failed run's `error` and the step it stopped on and say them in plain words, by the step's label. For "why did it fail yesterday", read that automation's runs with status failed and look at the ones from that day.
- `automations_get` reads one automation in full: status, steps with their approval modes, its spec, the live version and earlier versions. `unapproved_send_steps` lists the steps that would send, spend or act for the person without waiting for approval.
- `workflows_home` is the summary of what needs attention and what is running across the project's growth workflows; `workflows_flow` gives one live workflow's real batch counts and `workflows_step_people` the people at one step. Missing metrics stay unavailable. Never claim a queued batch has completed or sent anything.

Doing something:
- `automations_test_run` runs the current draft as a test against the latest matching event, or an `event_id`, or a subject and payload. A test has no side effects. Report the trace step by step, by each step's label. Test before publishing when the person is unsure.
- `automations_run_now` runs it for real on one record (`subject`). When it has `unapproved_send_steps`, or spends, show what it does and the price first, and confirm that exact call with the person: in the BrandWell Assistant with ask_person, `confirms` set to the exact call.
- `automations_set_state` pauses a live automation, resumes a paused one, or archives one, which stops its open runs. Resuming and archiving need the person's confirmation on a card; pausing does not.
- To pause several (for example everything that is failing), list them, tell the person which ones, and pause them one call at a time. Never archive to "stop" something; pausing keeps it.
- `automations_run_action` retries the step a run is paused on, skips it, or stops the run. Name the run from `automations_runs`. Say what retrying or skipping does before you do it.

Rules:
- Report exactly what BrandWell returned. If a tool failed or returned problems, say so; never claim a run, pause or resume succeeded without the returned result.
- Running, resuming, archiving and spending need the person's explicit request. Keep every request scoped to the current BrandWell project: never request, combine or reveal another workspace's automations, runs or people.
- To change what an automation does, load brandwell-automation-edit. To approve what waits for a person, load brandwell-automation-approvals. When a run is stuck on a missing connection, load brandwell-integrations; when it stopped for a spending limit, load brandwell-wallet.
