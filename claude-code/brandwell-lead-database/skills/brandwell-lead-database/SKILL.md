---
name: brandwell-lead-database
description: "Search the Lead Database for people and companies that match a description or filters: count first, search, stream the next new people, save a recurring search, and export a file. Use for 'find VPs of sales in Texas at 50 to 200 person SaaS companies', 'how many people match', 'export these'. Building a list from the results is brandwell-audiences, finding an email or phone for people you already have is brandwell-data-tools."
allowed-tools: lead_lookup_search lead_lookup_count lead_lookup_filter_values lead_lookup_save_search lead_lookup_export platform_capabilities audiences_add_people
metadata:
  title: "Lead Database search"
  service: records
  page: "#/marketpulse/people"
---

# Lead Database

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Lead Database finds people in included data. Read platform_capabilities first: when Lead Database is coming soon, say so and offer enrichment or intent audiences instead. Count first with lead_lookup_count, pass the person's plain words as description, and read lead_lookup_filter_values before using exact filter values. Search shows at most 1,000 rows a search; to go deeper, set stream to true on lead_lookup_search, which returns the next new people each call and never the same ones twice. Over API or MCP, people returned count toward exports, so say how many exports a call uses. Save recurring needs with lead_lookup_save_search instead of repeating searches, and add a search's people to an audience with audiences_add_people and from_lookup_search_id, which uses no exports. Filters cover every MarketPulse ICP field: the main groups have their own keys, and filters.profile holds the rest (gender, household, personal and company addresses, SIC and NAICS and more) keyed by field name, each with include, exclude, match and presence. lead_lookup_export writes a CSV or Excel file (format csv or xlsx; Excel holds up to 25,000 people), always needs the person's approval, runs partly when fewer exports are left than selected, and skips people already delivered.

Rules:
- Go one step at a time and ask one question at a time. In the BrandWell Assistant, ask with ask_person; never put a question at the end of a reply.
- Show the price before anything that spends: a column fill, a postcard, an export or a paid lookup. Name how many exports a call uses.
- When the Workflow Wallet is short, load brandwell-wallet and give the add-funds link. Never say funds were added. Keep every request scoped to the current BrandWell project.
