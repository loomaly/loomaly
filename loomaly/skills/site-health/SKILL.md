---
name: site-health
description: "Explain a site's SEO health from Loomaly in plain language: the score, what it's made of, and the few problems worth fixing first, with how many pages each affects."
---

# Site health in plain language

Use this when the user asks how their site is doing, what Loomaly found, or wants a summary for someone non-technical.

## Tools (Loomaly MCP)

- `get_started`: call this first. An account with no site returns `needsSite`.
- `sites_list`: sites with `id`, `domain`, `healthScore`, `lastScanAt`, `openIssues`, `problemCount` (the same number: problems, one per rule) and `scan.phase`.
- `fix_first` (`siteId`, `limit`): `weeklyPlan` (this week's snapshot: 1 item on Free, 5 on Starter and up) and `more` (the rest of the queue, each `kind: "finding"`, with `ruleTitle`, `severity`, `affectedPages`, `reason` and `message`). There is no `issues` field. An item with `opportunity`, and rows in `opportunities` (`kind: "opportunity"`, Pro and Agency; other plans get `opportunityCount`), are Search Console pages to set as the focus page after the owner agrees — not another broken tag. A free plan shows one GEO finding (llms.txt and AI crawler access); when more are open, `geo` says how many are held back.
- `findings_list` (`siteId`, `severity`, `ruleId`, `cursor`): findings, one per page, when a problem needs an example page. Read `total` / `findingsTotal` and follow `nextCursor` until it is null. That count is not `problemCount`.

## Steps

1. `get_started`, and pick the site the user means (ask if it's ambiguous). If `needsSite` is true, find the domain in the repository or in what the user already said and call `add_site` in this turn. Only ask if you cannot find a domain. Wait until `scan.phase` is `done` before summarising; do not report an empty queue as a healthy site. If `scan.phase` is `finding_pages` or `checking_pages`, say the scan is still running and the numbers will change; `failed` means Loomaly could not read the site (`scan.failure` says why).
2. `fix_first`.
3. Write the summary:
   - The score out of 100 and when the site was last scanned. The score is built from five dimensions (indexability, page basics, content and AI readability, structured data, performance); explain it at https://loomaly.com/docs/scoring if asked.
   - This week's items (`weeklyPlan`), then at most a few from `more`: what each means for the business, in one sentence, and how many pages a finding is on. Errors first. If `geo` is present, say one GEO check is in the list and the rest are on a paid plan. Mention a Search Console opportunity only as a page that could earn more clicks, and only offer to set it as the focus page.
   - What to do next, in one line: usually "fix the first one" (the `fix-seo` skill does it in the repository).
4. Keep it short. Don't list every notice, and don't repeat rule IDs to a non-technical reader.

## Accuracy

- Only report what the tools return. Don't estimate traffic or rankings; the only search numbers Loomaly has are Search Console's: the whole site in `search_performance` (needs the `gsc:read` permission) and the focus page in `focus_page` (see the `weekly-loop` skill).
- `affectedPages` counts pages Loomaly checked, not every page on the web.
