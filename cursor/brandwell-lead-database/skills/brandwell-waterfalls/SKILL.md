---
name: brandwell-waterfalls
description: "Read and change how enrichment looks up data for this project: source order, maximum lookup prices and miss rules. Use when the person wants cheaper email finding, verification or enrichment, asks why a provider was skipped, or wants to inspect or test an already saved provider key."
allowed-tools: waterfall_list waterfall_get waterfall_update waterfall_reset own_keys_list own_keys_set_use own_keys_test
metadata:
  title: "BrandWell Enrichment"
  service: data
  page: "#/tools/waterfalls"
---

# BrandWell Enrichment

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Use `waterfall_list` to identify the exact capability, then `waterfall_get` to read its current version, provider slugs, prices and skip reasons. Do not invent a source or assume the project uses the default order.

For a requested settings change, pass only the requested fields and the version you just read. Use exact USD decimals for `max_price_usd`. Null means Any, so use it only when the person asks to remove the price limit. Email finding and verification accept 0.02, 0.05 and 0.10; phone and enrichment also accept 0.25 and 1. Included data stays first. Own-key sources stay ahead of paid sources. These tools change future routing; they do not run data lookups or spend Workflow Wallet money.

Reset restores Cheapest per found contact and re-enables providers while preserving the price limit and miss rule. On a version conflict, read the latest settings, explain the conflict and apply only the change the person requested. Report the saved result, not the intended result.

Administrators may list masked keys or request a test of a saved key. A provider test may consume the customer's provider credit of unknown cost, even though it costs zero from the Workflow Wallet. Show the server quote and wait for real human approval. A token alone is not approval. Reuse the same confirmed execution on retry; do not request another test after an uncertain result. Replacing or removing the saved key requires a fresh confirmation.

Never ask for, save, reveal, replace or remove a provider key through chat or tool arguments. Direct those actions to the Enrichment page. The key list contains only masks and status. Read-only members can inspect routing but cannot change it.
