---
name: brandwell-waterfalls
description: "Read and change this project's data providers for any lookup (emails, mobiles, enrichment, companies and domains, Google keyword data, social, web): which providers are on, which to try first, the most per lookup and miss rules, with exact prices at cost. Use when the person wants cheaper or better lookups, asks why a provider was used or skipped, or wants to inspect or test a saved provider key."
allowed-tools: waterfall_list waterfall_get waterfall_update waterfall_reset own_keys_list own_keys_set_use own_keys_test
metadata:
  title: "BrandWell Data provider order"
  service: data
  page: "#/automations/settings/provider-order"
---

# BrandWell Data provider order

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Use `waterfall_list` to identify the exact capability, then `waterfall_get` to read its current version, provider slugs, prices and skip reasons. Do not invent a source or assume the project uses the default order.

Out of the box, use the defaults. A new workflow's data steps use the project's providers, and every provider starts on with nothing tried first. Change the providers only when the person asks, or when a lookup cannot work as asked (for example every provider is over the price they set), and then say what you changed.

Most lookups are routed (`routed: true`): one request asks the providers, lowest cost per find first (the price divided by how often that provider finds one, so a cheap one that rarely finds an answer goes later), and stops at the first that finds it. You pay that provider's own price at cost, and only when it finds the answer, unless the row says it charges per try. Data the person's plan includes is asked first, at no cost. For a routed lookup:
- Turn a provider off or on with `disabled` (send the whole list to keep off). Off means it is never asked in any workflow of this project.
- Try first is `order`: the providers to ask first, in that order, before the rest. `order: []` with `order_mode: best_value` clears the picks.
- The most per lookup is `max_price_usd`.
- `tried`, `found` and `spent_micros` are this project's own runs from the last 90 days; none means No runs yet. Never quote another project's numbers.
- Quote a cost as an "up to" price: the median price of the providers that are on, times the people who still need it. Say it is at cost and charged only when found.
Name providers as `waterfall_get` names them. A step in one workflow can keep its own providers only when the person asks for that on that step (brandwell-automation-edit); otherwise every step follows the project's choice.

For a requested settings change, pass only the requested fields and the version you just read. Use exact USD decimals for `max_price_usd`. Null means Any, so use it only when the person asks to remove the price limit. Email finding and verification accept 0.02, 0.05 and 0.10; phone and enrichment also accept 0.25 and 1. Included data stays first. Own-key sources stay ahead of paid sources. These tools change future routing; they do not run data lookups or spend Workflow Wallet money.

Reset restores Best value and re-enables providers while preserving the price limit and miss rule. On a version conflict, read the latest settings, explain the conflict and apply only the change the person requested. Report the saved result, not the intended result.

Administrators may list masked keys or request a test of a saved key. A provider test may consume the customer's provider credit of unknown cost, even though it costs zero from the Workflow Wallet. Show the server quote and wait for real human approval. A token alone is not approval. Reuse the same confirmed execution on retry; do not request another test after an uncertain result. Replacing or removing the saved key requires a fresh confirmation.

Never ask for, save, reveal, replace or remove a provider key through chat or tool arguments. Direct those actions to Automations › Settings › Your keys (#/automations/settings/keys). The key list contains only masks and status. Read-only members can inspect routing but cannot change it.
