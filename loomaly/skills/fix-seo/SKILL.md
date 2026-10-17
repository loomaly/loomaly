---
name: fix-seo
description: "Fix the SEO problem Loomaly ranks first on a site, in this repository: get the fix-first queue, read the evidence and fix prompt, change the code on a branch, mark it fixed with the PR link, and re-check it once it's deployed."
---

# Fix what Loomaly ranks first

Use this when the user wants to fix their site's SEO, work through Loomaly issues, or asks "what should I fix first". Run it from inside the site's repository.

## Tools (Loomaly MCP)

- `get_started` (optional `domain`): call this first. If the account has no site and you pass `domain`, it adds the site and starts the first scan. If `needsSite` is true and there is no domain yet, find one and call `add_site`.
- `sites_list`: the sites this account can see, with `id`, `domain`, `healthScore` and `scan.phase`. Every other tool needs a site `id`. An empty account returns `needsSite`.
- `add_site` (`domain`, optional `path`, `language`): adds a site and starts its first scan. Returns `poll` so you can watch `sites_list` until `scan.phase` is `done` or `failed`.
- `fix_first` (`siteId`, `limit`): open problems in the order Loomaly recommends. One entry per rule by default, with `affectedPages`, `templates`, `sampleUrl`, `sampleFindingId`, `lastSeenAt` and `reason`. A rule on many pages is usually one change in a shared layout or template.
- `findings_list` (`siteId`, `severity`, `state`, `ruleId`, `pathTemplate`, `url`): individual issues with IDs, for `fix_prompt` and `verify`.
- `fix_prompt` (`findingId`): the rule, the evidence and `devPrompt`, an instruction written for the site's framework. `template` says how many pages of the same template have the problem.
- `mark_fixed` (`siteId`, `ruleId` + `pathTemplate` or `allPages: true`, or `findingId`; `ref`, `note`): moves the problem to pending verification.
- `verify` (`findingId`, or `siteId` + `ruleId` + `pathTemplate` with a `limit`), then `verify_status` (`auditRunId` + `findingId`, or `runs`): re-checks live pages. Only after the fix is deployed. Each page re-checked uses one of the plan's monthly pages.
- `ignore_finding` (`siteId`, a target as for `mark_fixed`, `reason`): for a finding the user says is not a problem for their site.

If the tools aren't available, tell the user to connect Loomaly (`claude mcp add --transport http loomaly https://loomaly.com/mcp`) and stop.

## Steps

1. `get_started`. If `needsSite` is true, find the domain in this repository before asking the user: `package.json` `homepage`, the README, a canonical URL, the production URL in config, or a URL the user already gave you. If `suggestedDomain` is set, use that. Call `add_site` (or `get_started` again with `domain`) in this turn. Only ask when you cannot find a domain. The call starts the first scan. Poll `sites_list` until `scan.phase` is `done` or `failed` (5–20 minutes). While it is `finding_pages` or `checking_pages`, say the scan is running, not that the site is clean. If more than one site matches the repository, ask which one; don't guess.
2. `fix_first` with `limit: 5`. Tell the user the top problem in one sentence: what it is, how many pages, and `reason`. Say what you'll change before you change it.
3. `fix_prompt` with the entry's `sampleFindingId`. If `lastSeenAt` is older than the last deploy, check the live page first: it may already be fixed. Read `evidence` before the prompt: fix what the evidence shows, not what the rule's name suggests.
4. Find where the problem comes from in this repository. Prefer the shared layout, template or component over editing pages one by one: `affectedPages` tells you whether it's a template-wide fix.
5. Make the change on a new branch, run the project's own checks and tests, and open a PR. Don't push to the main branch.
6. `mark_fixed` with `ruleId` and the `pathTemplate` you fixed (or `allPages: true` for a layout-wide change), `ref` set to the PR URL and a one-sentence `note`.
7. Tell the user the problem stays pending until a re-check. Once they say it's deployed, `verify` one finding (or the group, `ruleId` + `pathTemplate` with `limit: 3`, for a template fix) and poll `verify_status` every 20–30 seconds until `finished`. Report the verdict: `fixed`, `still-open` (look again at the evidence), or `check-failed` (the page couldn't be loaded; not a verdict on the fix).

## Don't

- Don't mark something fixed before the change is merged.
- Don't call `verify` on a branch that isn't deployed: it reads the live page.
- Don't fix a problem the evidence doesn't support. If the evidence contradicts the rule (the page already has the tag it says is missing), say so instead of editing, and offer to `ignore_finding` it with that reason.
- Don't ignore a finding without the user's say-so.
