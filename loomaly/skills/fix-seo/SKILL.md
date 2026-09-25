---
name: fix-seo
description: "Fix the SEO problem Loomaly ranks first on a site, in this repository: get the fix-first queue, read the evidence and fix prompt, change the code on a branch, mark it fixed with the PR link, and re-check it once it's deployed."
---

# Fix what Loomaly ranks first

Use this when the user wants to fix their site's SEO, work through Loomaly issues, or asks "what should I fix first". Run it from inside the site's repository.

## Tools (Loomaly MCP)

- `sites_list`: the sites this account can see, with `id`, `domain` and `healthScore`. Every other tool needs a site `id`.
- `fix_first` (`siteId`, `limit`): open problems in the order Loomaly recommends. One entry per rule by default, with `affectedPages`, `templates`, `sampleUrl` and `reason`. A rule on many pages is usually one change in a shared layout or template.
- `findings_list` (`siteId`, `severity`, `state`): individual issues with IDs, for `fix_prompt` and `verify`.
- `fix_prompt` (`findingId`): the rule, the evidence and `devPrompt`, an instruction written for the site's framework.
- `mark_fixed` (`siteId`, `ruleId` + `pathTemplate` or `allPages: true`, or `findingId`; `ref`, `note`): moves the problem to pending verification.
- `verify` (`findingId`), then `verify_status` (`auditRunId`, `findingId`): re-checks the live page. Only after the fix is deployed. Each `verify` uses one of the plan's monthly pages.

If the tools aren't available, tell the user to connect Loomaly (`claude mcp add --transport http loomaly https://loomaly.com/mcp`) and stop.

## Steps

1. `sites_list`. If more than one site matches the repository, ask which one; don't guess.
2. `fix_first` with `limit: 5`. Tell the user the top problem in one sentence: what it is, how many pages, and `reason`. Say what you'll change before you change it.
3. `findings_list` for the site, pick a finding of that rule on the sample page, and `fix_prompt` for it. Read `evidence` before the prompt: fix what the evidence shows, not what the rule's name suggests.
4. Find where the problem comes from in this repository. Prefer the shared layout, template or component over editing pages one by one: `affectedPages` tells you whether it's a template-wide fix.
5. Make the change on a new branch, run the project's own checks and tests, and open a PR. Don't push to the main branch.
6. `mark_fixed` with `ruleId` and the `pathTemplate` you fixed (or `allPages: true` for a layout-wide change), `ref` set to the PR URL and a one-sentence `note`.
7. Tell the user the problem stays pending until a re-check. Once they say it's deployed, `verify` one finding and poll `verify_status` every 20–30 seconds until `finished`. Report the verdict: `fixed`, `still-open` (look again at the evidence), or `check-failed` (the page couldn't be loaded; not a verdict on the fix).

## Don't

- Don't mark something fixed before the change is merged.
- Don't call `verify` on a branch that isn't deployed: it reads the live page.
- Don't fix a problem the evidence doesn't support. If the evidence contradicts the rule (the page already has the tag it says is missing), say so instead of editing.
