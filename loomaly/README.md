# Loomaly plugin

Fix your site's SEO from your coding assistant. Loomaly checks every page of your site, ranks what to fix first, gives your assistant a fix prompt for your framework, and re-checks the page once the fix is live.

- MCP server: `https://loomaly.com/mcp` (sign in with your Loomaly account the first time)
- Skills: `fix-seo`, `site-health`, `internal-links`, `weekly-loop`
- Docs: https://loomaly.com/docs/mcp

## Claude Code

```bash
claude mcp add --transport http loomaly https://loomaly.com/mcp
```

## Cursor

Add to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "loomaly": { "url": "https://loomaly.com/mcp" } } }
```
