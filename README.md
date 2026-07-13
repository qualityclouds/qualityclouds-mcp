<!-- mcp-name: ai.qualityclouds/hub -->
# Quality Clouds Hub MCP Server
AI code governance rules injected into Cursor, Claude Code and other MCP clients at generation time.
Quality Clouds Hub connects your AI development tool to a governance rule library built around the error patterns AI-generated code typically contains. When the model generates code, the rules for your detected stack are already in its context, so the output follows them from the first line.
- Remote server (Streamable HTTP): `https://api.qualityclouds.ai/mcp`
- Auth: API key, generated in one click at [portal.qualityclouds.ai](https://portal.qualityclouds.ai). Permanent free tier.
- Works with Cursor, Claude Code, Lovable, Replit and any MCP-compatible client
- Stacks covered: TypeScript, Python, Java, Node, React, Supabase and more
## What it does
Rulesets are stack-specific and activate automatically for the stack the server detects. A single repository scan activates rulesets across six functional areas: Security, Performance, Scalability, Manageability, Maintainability and Architecture. The Supabase ruleset alone covers 12 rules, including no service-role keys outside the server, no hardcoded keys or project URLs, mandatory error checks on every mutation, no client-side JWT decoding, and rate limiting on edge functions.
The server exposes three tools:
| Tool | What it does |
|------|--------------|
| `get_tools` | Detects your project's stack and returns the applicable governance tooling |
| `get_rules_for_tool` | Returns the active ruleset, rule by rule, with IDs |
| `register_applied_actions` | Records what was done: rules verified compliant, violations fixed (file and lines), violations prevented during generation, and which model did the work |
Every session produces a structured record of what was checked, fixed and prevented. Your repository's Production-Ready Score and full findings live in your workspace at [portal.qualityclouds.ai](https://portal.qualityclouds.ai).
## Try it in 5 minutes (Claude Code)
1. Sign up and generate an API key at [portal.qualityclouds.ai](https://portal.qualityclouds.ai) (MCP Connections page).
2. Add the server:
```bash
claude mcp add --scope user --transport http qualityclouds-hub https://api.qualityclouds.ai/mcp \
  --header "Authorization: Bearer <your-api-key>"
```
3. Check it connected:
```bash
claude mcp list
```
4. Open a session in any repo and ask Claude Code to review a file against your coding standards. It will detect the Hub server, fetch the rules for your stack, and register the results back to your workspace.
## Cursor
Add to `.cursor/mcp.json`:
```json
{
  "mcpServers": {
    "qualityclouds-hub": {
      "url": "https://api.qualityclouds.ai/mcp",
      "headers": { "Authorization": "Bearer <your-api-key>" }
    }
  }
}
```
## Links
- Sign up: [portal.qualityclouds.ai](https://portal.qualityclouds.ai)
- Product: [qualityclouds.ai/hub](https://www.qualityclouds.ai/hub)
- Community, docs and support: [github.com/qualityclouds/Community](https://github.com/qualityclouds/Community)
Built by [Quality Clouds](https://www.qualityclouds.ai), the AI Code Governance platform, governing 950+ enterprise platform instances since 2015.
