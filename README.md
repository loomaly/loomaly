# Loomaly for Claude Code, Cursor and Codex

[Loomaly](https://loomaly.com) checks every page of your site and ranks its SEO problems by what to fix first. Your coding agent (Claude Code, Codex or Cursor) gets each problem with a fix prompt for your framework, makes the change in your repo for you to review, and asks Loomaly to re-check the page once the fix is live. Loomaly never changes your site itself.

This repository is the plugin: Loomaly's MCP server (`https://loomaly.com/mcp`) plus four skills.

| Skill | What it does |
| --- | --- |
| `fix-seo` | Takes the problem Loomaly ranks first, fixes it in this repository on a branch, marks it fixed with the PR link, and re-checks it once deployed. |
| `site-health` | Explains a site's health score in plain language: what it's made of, and the few problems worth fixing first, with how many pages each affects. |
| `internal-links` | Goes through the internal links Loomaly suggests with you, adds the approved ones to the source content, and records each decision. |
| `weekly-loop` | Runs the weekly loop on one page that should make money: judges the last change by search and conversions, and proposes one next change with evidence. |

The first time a tool runs, your assistant opens a browser window so you can sign in or create a free account; the free plan covers one site.

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

## Try it

From your site's repository, ask your assistant:

- "Use Loomaly to check example.com. Fix the 3 problems it ranks first in this repo, and open a PR for me to review."
- "What should I fix first on my site's SEO?"
- "Explain my site's SEO health score."

## Links

- Docs: https://loomaly.com/docs/mcp
- Free check of any site, no sign-up: https://loomaly.com
- Privacy: https://loomaly.com/privacy

MIT licensed.
