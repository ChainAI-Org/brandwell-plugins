---
name: brandwell-workflow-sharing
description: "Share a workflow: with the whole team or the teammates picked (run or edit), with specific people by email (run or view), or as a public page on brandwell.ai anyone can save a copy of; read how it is shared and whether its share video and images are ready. Use for 'share this with Dana', 'let the team run it', 'send it to my client', 'publish this workflow', 'is the share video ready'."
allowed-tools: workflows_sharing workflows_share_team workflows_share_people workflows_publish_public workflows_share_media automations_list
metadata:
  title: "Share a workflow"
  service: automations
  page: "#/automations"
---

# Share a workflow

Confirm facts with this skill's tools before stating them; what the page shows is a starting point, not the answer. When no tool can confirm something, say so and offer BrandWell support. Never say BrandWell cannot do something unless a tool says so.

Read `workflows_sharing` first: who has it now, the teammates you can pick (by id), and whether it has a public page.

Three ways, and what each does:
- Team: `workflows_share_team` with scope team (everyone, new teammates included) or members (the teammates the person named, by their ids from `workflows_sharing`), who can run it or edit it. They get a notice in BrandWell. Nothing leaves the account. Scope off stops it.
- Specific people: `workflows_share_people` with the email addresses the person gave and run or view. Each gets an email inviting them into their own BrandWell account, so the person confirms first. Never guess an address.
- Public: `workflows_publish_public` publishes a page on brandwell.ai that anyone can read and save a copy of, or updates the page it already has. The person confirms first. The first time, the person accepts the workflow creator terms in the Share dialog; when the tool says so, give them the link and publish again after.

Writing the public page: every page has the same blocks, and each lands in the styled page as written, so write them in the house style (plain, second person, short sentences, no em dash, never a data supplier's name):
- title: what it does, in a few words. result: one line on what it gets the reader.
- page.hero: one or two sentences under the title.
- page.unlocks: 2 to 4 results for the reader, in their words.
- page.how: for any step worth explaining, by its number, what it does (text) and what it finds (finds).
- page.benefits: 3 or 4, each a short title and one line.
- page.make_it_yours: 4 or 5 ways to adapt it, each a short title and one line (change any step, plug in their own tools at partner cost, build apps and internal tools from the same nodes, assign tasks to each teammate's agent).
Any block left out is generated from the workflow, so a page is never missing one. Prices are never written here: the page shows its own From price.

What a share carries: the steps, never the customer's connections, keys, webhook addresses or contacts. Whoever receives it can save their own copy; the original never changes.

`workflows_share_media` says whether the page's video, GIF and link image are ready or still rendering, with their addresses. It renders nothing.

Rules:
- Share only what the person asked, with whom they named. Ask one question at a time; in the BrandWell app's chat, ask with ask_person.
- Report what the tools returned: who has access, and the page address once it is published.
