---
name: brandwell-data-tools
description: "Run BrandWell data jobs on people or companies the person already has: find emails and mobile numbers, verify an email, enrich a person or company, scrape reviews or a web page (such as a company's reviews on G2), compare data sources, see the per-hit price before running, and check an asynchronous result. Use for 'find mobile numbers for these people', 'scrape the reviews of this company', 'enrich this list'. To find new people who match a profile use brandwell-lead-database."
allowed-tools: data_tools_search data_tools_describe data_tools_request data_tools_estimate data_capability_run data_tools_run data_call_get enrich_person enrich_company
metadata:
  title: "BrandWell data tools"
  service: data
  page: "#/tools"
---

# BrandWell data tools

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

1. Search for the job in the person's words. When the Tools library is enabled, categories, sources, price, sort, group and cursor match its page exactly. Preserve the returned job id for describe; a routed job id is a capability and a product job links to its product workflows. The list price ignores saved keys, while detail shows the selected project's key sources at zero Workflow Wallet cost. The catalog is discovered through search and describe, not thousands of separate tool definitions.
2. Describe the selected tool or capability. Check required identity combinations, filters, output fields, billing terms and current prices. Never invent an identifier, price or accepted input.
3. Prefer a routed capability with the project waterfall enabled. It tries the project's sources and stops when a result is found. Use a specific tool only when the person needs that source or there is no routed capability.
4. Estimate before spending and explain the maximum. "Charged only on a hit" means that source charges when it finds a result. Other sources may charge even for a miss; the receipt records those attempts too. An unknown estimate is not free.
5. Run with an explicit maximum the person requested or approved. A small data-only spend can use an administrator's enabled budget. Any send, publishing or CRM write needs human confirmation regardless of price. A quote token is not approval. When the result needs confirmation, show the approval flow and wait for the person's real approval; never supply a confirmed flag or claim approval yourself.
6. If a result is pending or uncertain, show its call reference and use data_call_get. Do not make a second paid request to obtain the same result. Protected reservations remain until an authoritative receipt settles them.
7. Explain the actual price, source, cached or included status and meaningful misses. Surface structured Workflow Wallet, permission, plan and identity errors as given. Do not conceal a failure or suggest bypassing a limit.

For a list of people, prefer an audience enrichment column and its batch workflow when those tools are available. Ask for the audience and desired fields instead of issuing hundreds of individual calls. If audience tools are not offered, explain that the batch integration is not available in this session.

When the person asks for a missing source, use data_tools_request with their description and an optional public website. It saves a request without spending money or contacting the source. Report the saved receipt or daily-limit error; do not promise availability or send a duplicate.

Provider key values never belong in chat or tool arguments. Direct the person to the Enrichment page to enter a key. Do not save, reveal or delete one through an agent tool.
