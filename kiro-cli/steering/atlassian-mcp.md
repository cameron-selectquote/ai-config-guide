# Atlassian MCP (Jira + Confluence)

Purpose: Standardize how to access Jira and Confluence via the hosted Atlassian MCP server.

## Default Approach
- Use the hosted Atlassian MCP server for Jira/Confluence requests.
- Do NOT use MCP keys or other MCP servers unless explicitly asked.
- Do NOT ask the user to add another MCP; the hosted server is sufficient.

## MCP Configuration Location (Kiro)
- User config: `~/.kiro/settings/mcp.json`
- Workspace config: `.kiro/settings/mcp.json`

## MCP JSON (Kiro)
```json
{
  "mcpServers": {
    "atlassian": {
      "url": "https://mcp.atlassian.com/v1/sse"
    }
  }
}
```

## Server Endpoint
- Hosted server URL: `https://mcp.atlassian.com/v1/sse`
- GitHub: https://github.com/atlassian/atlassian-mcp-server

## Capabilities
- Read and update both Jira and Confluence based on the user’s Atlassian permissions.

## Authentication
- The first request triggers an OAuth browser flow.
- If auth fails, re-authenticate via the hosted service (browser-based OAuth).
- If problems persist, force a fresh auth flow using the command below.

## Force Auth (manual re-auth)
```
npx -y mcp-remote https://mcp.atlassian.com/v1/sse
```

## Debug Checklist
- Confirm the MCP server URL is correct in the MCP config.
- Re-run the force auth command to refresh tokens.
- Ensure the Atlassian account has access to the target Jira/Confluence spaces/projects.
- Retry the request after auth completes.

## Notes
- No API keys are required.
- No additional MCP servers are required.
