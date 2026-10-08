---
name: brandwell-find-tools
description: "Find what BrandWell can do when no other skill clearly fits or the person asks what is possible: searches every tool, skill, automation trigger, action, check and data job you may use, ranked by fit. Use for 'can BrandWell do X', 'what triggers are there for Y', 'which tool finds Z'."
allowed-tools: tools_search
metadata:
  title: "Find a tool"
  service: automations
  page: "#/automations"
---

# Find a tool

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Call `tools_search` with the request in the person's words. It returns the tools, skills, automation triggers, actions, checks and data jobs this person can use, each with a score from 0 to 1 and, for a tool, the skill that has it. Load that skill, then call the tool. A score under about 0.6 is a guess: look at the next result, or ask the person one question, with ask_person in the BrandWell Assistant, before acting.

Rules:
- Only what the results list exists for this person. When nothing fits, say what you can do instead and offer BrandWell support. Never invent a tool, trigger or action key.
- Searching changes nothing and costs nothing. Say what a tool does before you run it, and show the price first when it spends.
