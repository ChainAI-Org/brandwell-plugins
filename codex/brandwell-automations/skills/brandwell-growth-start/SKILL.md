---
name: brandwell-growth-start
description: "Test, start and watch a growth workflow once its draft is ready: test it on five real records, set its spending limit, start it with the person's approval of the quote, and read what is running and what needs attention. Use for 'start it', 'test it first', 'what is running', 'what needs my attention', 'only spend $20 a day on this'."
allowed-tools: workflows_estimate workflows_test workflows_start workflows_flow workflows_step_people workflows_run_now workflows_home workflows_preview wallet_set_limits wallet_check_spend integrations_connect_link
metadata:
  title: "Test, start and watch a growth workflow"
  service: automations
  page: "#/automations"
---

# Test, start and watch a growth workflow

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Propose a limit and at-limit behavior, normally holding paid work until the next budget period. Test five actual project inputs with workflows_test. Explain missing inputs or unavailable safe previews instead of claiming a test passed. Test receipts are simulations and predict neither delivery nor conversions.

Show the price first with workflows_estimate (or workflows_preview for the draft's reach and maximum). Use workflows_start only after the person approves its quote. It always needs human confirmation, including zero-cost starts. The reviewed draft revision must still match. Every paid workflow needs a finite limit: an agent cannot start paid work with No limit, even if a person asks. A person can review that choice directly on the Start page. An agent cannot approve itself, fabricate a confirmation, or use an earlier quote after changing the draft.

After publication, give the returned workflow link and use workflows_flow or automations_get for real status. Drafting, testing and publishing are distinct states. If publication fails, report the structured error and leave the workflow unpublished.

For what needs attention or what is running, read workflows_home. Its counts describe persisted project state in the returned time window. Missing metrics stay unavailable. Its links open human controls; reading this summary never approves a step, resumes a workflow or adds funds.

For a live workflow, read workflows_flow for its real batch counts and workflows_step_people for a step. Run now and spending-limit changes always need the person to confirm the current quote. Use wallet_set_limits with scope workflow, period day and today_only true for a temporary raise or included_only day; use resume only for a limit pause. A run quote binds the saved input, live version, day and limit. If any changes, get a fresh quote. Never claim a queued batch has completed or that it has sent anything.

Start offers now, daily at 07:00 project time, and pull where offered. Its limit can be a daily amount or a rate per 100 contacts, with hold, included_only or pause at the limit.

Working with the person:
- Go one step at a time and ask one question at a time. In the BrandWell Assistant, ask with ask_person; never put a question at the end of a reply.
- Never start work whose price you have not shown. A paid workflow needs a finite limit: ask which amount, "only spend $20 a day" is a day limit of 20, with hold, included_only or pause at the limit.
- When the Workflow Wallet is short for the quote, load brandwell-wallet and give the add-funds link. When a step needs a connection, call integrations_connect_link and give the link. Never say funds were added or a connection was made.
