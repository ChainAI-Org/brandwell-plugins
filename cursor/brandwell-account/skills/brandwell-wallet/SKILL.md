---
name: brandwell-wallet
description: "The Workflow Wallet and spending limits: read the balance, charges and statements, check whether a spend fits, set or lower a spending limit ('only spend $20 a day on this'), and prepare the add-funds or auto top-up link when the wallet is short. Use for 'what is my wallet balance', 'how much have I spent', 'add funds', 'cap this at $50 a week'. Plans, upgrades and refunds are in brandwell-plans."
allowed-tools: wallet_status wallet_check_spend wallet_set_limits wallet_list_charges wallet_statement pricing_list wallet_add_funds wallet_set_auto_topup workflows_estimate
metadata:
  title: "Workflow Wallet and spending limits"
  service: account
  page: "#/account?tab=usage"
---

# Workflow Wallet and spending limits

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Reading:
- Read `wallet_status` for the balance, the limits in force and what is held. Call the prepaid balance the Workflow Wallet when speaking to the customer, never just the wallet. Use `wallet_list_charges` and `wallet_statement` for actual activity and `pricing_list` for current customer prices. Never invent charges, counts or prices. Describe paid third-party data as BrandWell data. Do not expose internal costs or private providers.
- `wallet_check_spend` checks a proposed amount without spending or reserving funds. USD inputs are exact decimal strings; raw amounts stay in integer micros. `workflows_estimate` prices a draft or a spec before it starts: always show the range before anything starts.

Spending limits:
- A limit says how much a workflow or the workspace may spend in a day or a month and what happens at the limit: hold (paid steps wait), included_only (go on without paid steps) or pause. "Only spend $20 a day on this" is a day limit of 20 on that workflow; ask which at-limit behavior they want, one question.
- `wallet_set_limits` produces a fresh quote and the person approves it before it applies. Explain the scope, period, amount and at-limit behavior. Null means no limit and must be shown and approved explicitly. Never forge confirmation tokens or reuse an approval after changing arguments. Lowering a limit never spends. To set a limit while publishing, `automations_publish` takes the same `limit`.
- No tool here can change the agent auto-approve budget.

When the wallet is short:
- Say the balance and the shortfall from `wallet_status` and the estimate. Call `wallet_add_funds` with the amount to prepare the Add funds link and give it to the person. It prepares a review link only: return the supplied `confirm_url` and explain that the account owner must open it, review fresh numbers and confirm there. When the tool is not offered, point them to Usage and Add funds. Never say money was added, a purchase completed or a card charged from a prepared response.
- `wallet_set_auto_topup` enabling auto top-up also only prepares a review link. Disabling it applies directly and stops future top-ups. Do not turn it back on without the owner's fresh page confirmation.
- Paid funds carry while subscribed; outside the guarantee, unused paid funds are forfeited when the paid period ends. Billing changes and statements need a non-impersonating account administrator. A read-only member can still inspect permitted usage.

Rules:
- Go one step at a time and ask one question at a time. In the BrandWell Assistant, ask with ask_person; never put a question at the end of a reply.
- Keep amounts exact as the tool returned them. Keep every request scoped to the current BrandWell project.
