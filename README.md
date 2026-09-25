# Loomaly for Claude Code, Cursor and Codex

[Loomaly](https://loomaly.com) checks every page of your site, ranks what to fix first, and hands each problem to your coding assistant as a fix prompt for your framework. Once the fix is live, it re-checks the page.

This repository is the plugin: Loomaly's MCP server (`https://loomaly.com/mcp`) plus three skills.

| Skill | What it does |
| --- | --- |
| `fix-seo` | Takes the problem Loomaly ranks first, fixes it in this repository on a branch, marks it fixed with the PR link, and re-checks it once deployed. |
| `site-health` | Explains a site's health score in plain language: what it's made of, and the few problems worth fixing first, with how many pages each affects. |
| `internal-links` | Goes through the internal links Loomaly suggests with you, adds the approved ones to the source content, and records each decision. |

You need a Loomaly account; the free plan covers one site. The first time a tool runs, your assistant opens a browser window so you can sign in.

## Install

### Claude Code

```
/plugin marketplace add dengzhaofun/loomaly
/plugin install loomaly@loomaly
```

Or just the MCP server:

```bash
claude mcp add --transport http loomaly https://loomaly.com/mcp
```

### Cursor

Install **Loomaly** from the Cursor Marketplace, or add the server to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "loomaly": { "url": "https://loomaly.com/mcp" } } }
```

### Codex

Open **Plugins** in the sidebar, then **More → Add more**, and enter `dengzhaofun/loomaly` as the marketplace source.

## Try it

From your site's repository, ask your assistant:

- "What should I fix first on my site's SEO?"
- "Fix the top Loomaly issue and open a PR."
- "Explain my site's SEO health score."

## Links

- Docs: https://loomaly.com/docs/mcp
- Free check of any site, no sign-up: https://loomaly.com
- Privacy: https://loomaly.com/privacy

MIT licensed.
