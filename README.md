# Loomaly for Claude, ChatGPT, Cursor and Codex

[Loomaly](https://loomaly.com) is one MCP for all of your SEO: rankings, AI search, fixes and reports. Fixed in your code, proven in your numbers. Your assistant gets the problem Loomaly ranks first with evidence and steps for your framework. A coding agent (Claude Code, Codex or Cursor) makes the change in your repo for you to review, or the assistant sends it to a developer, and Loomaly re-checks the live page once it ships. Loomaly never changes your site itself.

This repository is the plugin: Loomaly's MCP server (`https://loomaly.com/mcp`, version **2.1.1**, twelve tools) plus three skills.

| Skill | Who | What it does |
| --- | --- | --- |
| `seo` | solo / developers | Takes the problem Loomaly ranks first, fixes it in this repository on a branch, marks it fixed with the PR link, and re-checks it once deployed. |
| `seo-ops` | ops | Weekly report, hands work to developers, tracks fix progress, and reads charts from tool text (tables and sparklines). |
| `weekly-loop` | product | One focus page that should make money: judges the last change by search and conversions, and proposes one next change with evidence. |

Tools: `status`, `add_site`, `todo`, `problem`, `triage`, `send_to_dev`, `check`, `visibility`, `focus`, `set_goals`, `google`, `report`. Every reply carries `say` (what to tell you), `next` (the next call) and, for steps only you can do in the browser, a `handoff` to `https://loomaly.com/account/...`.

The first time a tool runs, your assistant opens a browser window so you can sign in or create a free account; the free plan covers one site. If the account has no site yet, the assistant finds this repository's domain and adds it with `add_site`, which starts the first scan.

## Install

### Claude Code

```
/plugin marketplace add loomaly/loomaly
/plugin install loomaly@loomaly
```

Or just the MCP server:

```bash
claude mcp add --transport http loomaly https://loomaly.com/mcp
```

### Cursor

Install **Loomaly** from the Cursor Marketplace, or [add the server in one click](https://cursor.com/en/install-mcp?name=loomaly&config=eyJ1cmwiOiJodHRwczovL2xvb21hbHkuY29tL21jcCJ9), or add it to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "loomaly": { "url": "https://loomaly.com/mcp" } } }
```

### Codex

Open **Plugins** in the sidebar, then **More → Add more**, and enter `loomaly/loomaly` as the marketplace source.

Or just the MCP server (the Codex CLI, app and IDE extension share it):

```bash
codex mcp add loomaly --url https://loomaly.com/mcp
```

Codex opens your browser to sign in straight away; if you close it, run `codex mcp login loomaly`.

### Claude on the web, desktop or phone

Open [Loomaly in the Claude connector directory](https://claude.ai/directory/loomaly) and click **Connect**. No terminal needed. Claude there reads your site's numbers and problems and explains how to fix them; it can't change your code, so use one of the coding agents above to have fixes made for you.

### ChatGPT

On ChatGPT Business, Enterprise or Edu, add a custom MCP connector with the URL `https://loomaly.com/mcp` and sign in to Loomaly when ChatGPT opens the browser.

## Try it

From your site's repository, ask your assistant:

- "Use Loomaly to check example.com. Fix the problem it ranks first in this repo, and open a PR for me to review."
- "How did my site do this week?"
- "Send the top problem to my developer."

## Pricing

A new account starts on the **Free** plan ($0, no card): 1 site and 50 in-depth pages a month. Paid plans are Starter **$29/month** (3 sites, $3/month data budget), Pro **$79/month** (10 sites, $12/month data budget) and Agency **$199/month** (20 sites, $35/month data budget, white-label reports). The data budget pays for rankings, AI visibility, competitors and backlinks; when it runs out, paid checks pause until next month, with no overage. Details: https://loomaly.com/docs/plans

## Links

- Docs: https://loomaly.com/docs/mcp
- Account and billing: https://loomaly.com/account
- Claude connector directory: https://claude.ai/directory/loomaly
- Free check of any site, no sign-up: https://loomaly.com
- Privacy: https://loomaly.com/privacy

MIT licensed.
