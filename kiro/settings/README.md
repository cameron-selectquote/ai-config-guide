# Kiro MCP Settings

This folder contains MCP server configurations for Kiro on Windows.

## MCP Config Locations

- User config: `~/.kiro/settings/mcp.json`
- Workspace config: `.kiro/settings/mcp.json`

Copy the `mcp.json` from this folder to either location.

---

# Playwright MCP

Browser automation for testing, scraping, and web interactions.

## Prerequisites

### Install Node.js

```powershell
# Using Winget
winget install OpenJS.NodeJS.LTS

# Or download from https://nodejs.org/
```

Verify installation:

```powershell
node --version
npm --version
```

### Install Playwright Browsers

```powershell
npx playwright install
```

This downloads Chromium, Firefox, and WebKit browsers.

To install only Chromium (smaller download):

```powershell
npx playwright install chromium
```

## Configuration

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest"
      ],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Browser not found" | Run `npx playwright install` |
| Permission errors | Run PowerShell as Administrator |
| Slow first run | Normal - downloads package from npm |

## Resources

- [Playwright Documentation](https://playwright.dev/)
- [Playwright MCP Server](https://github.com/microsoft/playwright-mcp)

---

# Atlassian MCP (Jira + Confluence)

Hosted MCP server for accessing Jira and Confluence.

## Overview

- Uses the hosted Atlassian MCP server (no local install required)
- No API keys needed
- OAuth authentication via browser

## Configuration

```json
{
  "mcpServers": {
    "atlassian": {
      "url": "https://mcp.atlassian.com/v1/sse"
    }
  }
}
```

## Authentication

The first request triggers an OAuth browser flow. Sign in with your Atlassian account.

### Force Re-authentication

If auth fails or tokens expire, run:

```powershell
npx -y mcp-remote https://mcp.atlassian.com/v1/sse
```

## Capabilities

- Read and update Jira issues
- Read and update Confluence pages
- Access based on your Atlassian account permissions

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Auth fails | Run the force auth command above |
| No access to project/space | Check Atlassian account permissions |
| Connection errors | Verify URL is `https://mcp.atlassian.com/v1/sse` |

## Resources

- [Atlassian MCP Server](https://github.com/atlassian/atlassian-mcp-server)
