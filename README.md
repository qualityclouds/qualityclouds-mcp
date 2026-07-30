<!-- mcp-name: ai.qualityclouds/hub -->
# Norma MCP Server

AI code governance rules injected into Cursor, Claude Code and other MCP clients at generation time.

Norma connects your AI development tool to a governance rule library built around the error patterns AI-generated code typically contains. When the model generates code, the rules for your detected stack are already in its context, so the output follows them from the first line.

- Remote server (Streamable HTTP): `https://api.qualityclouds.ai/mcp`
- Auth: OAuth. Sign in via browser on first connection. Permanent free tier.
- Works with Cursor, Claude Code, Lovable, Replit and any MCP-compatible client
- Stacks covered: TypeScript, Python, Java, Node, React, Supabase and more

## What it does

Rulesets are stack-specific and activate automatically for the stack the server detects. A single repository scan activates rulesets across six functional areas: Security, Performance, Scalability, Manageability, Maintainability and Architecture. The Supabase ruleset alone covers 12 rules, including no service-role keys outside the server, no hardcoded keys or project URLs, mandatory error checks on every mutation, no client-side JWT decoding, and rate limiting on edge functions.

The server exposes five tools:

| Tool | What it does |
|------|--------------|
| `link_repository` | Links the current workspace to Norma. Called once, on first connection in a workspace, before any other tool |
| `get_tools` | Detects your project's stack and returns the applicable governance tooling |
| `get_rules_for_tool` | Returns the active ruleset, rule by rule, with IDs, for a given tool |
| `live_check` | Real-time scan of a code snippet: returns severity-rated issues and remediation advice as the model writes it |
| `register_applied_actions` | Records what was done: rules verified compliant, violations fixed (file and lines), violations prevented during generation, and which model did the work |

Every session produces a structured record of what was checked, fixed and prevented. Your repository's Production-Ready Score and full findings live in your workspace at [portal.qualityclouds.ai](https://portal.qualityclouds.ai).

## How it works

A coding agent connected to Norma follows this sequence:

1. `link_repository` — first connection in each workspace, before any other call.
2. `get_tools` — at the start of any coding task.
3. `get_rules_for_tool` — for each relevant tool ID; never skipped.
4. The agent writes or modifies code, with those rules in context.
5. `live_check` — after each file is created or modified, before moving on.
6. `register_applied_actions` — after the task, using the exact rule IDs from step 3.

## Try it in 5 minutes (Claude Code)

1. Add the server:

```bash
claude mcp add --scope user --transport http norma https://api.qualityclouds.ai/mcp
```

2. Check it connected:

```bash
claude mcp list
```

3. On first use, your browser opens to sign in. Free to start, no credit card.
4. Open a session in any repo and ask Claude Code to review a file against your coding standards. It will link the repository, fetch the rules for your stack, and register the results back to your workspace.

## Cursor

Add to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "norma": {
      "url": "https://api.qualityclouds.ai/mcp"
    }
  }
}
```

Cursor will prompt you to sign in via browser on first connection.

## Links

- Sign up: [portal.qualityclouds.ai](https://portal.qualityclouds.ai)
- Product: [qualityclouds.ai/hub](https://qualityclouds.ai/hub)
- Community, docs and support: [github.com/qualityclouds/community](https://github.com/qualityclouds/community/discussions)

Built by [Quality Clouds](https://qualityclouds.ai), the AI Code Governance platform, governing 950+ enterprise platform instances since 2017.
