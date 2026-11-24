# Installing Warm MCP Server (`https://app.warm.io/mcp`)

Warm is a hosted remote Streamable HTTP MCP server (`https://app.warm.io/mcp`). There is **no local package to install, build, or run** and **no API key to configure**—clients connect directly over HTTPS and authenticate via OAuth 2.1 (PKCE + Client ID Metadata Document).

## Endpoint

- **URL:** `https://app.warm.io/mcp`
- **Transport:** Streamable HTTP (`http` / `streamableHttp`)
- **Authentication:** OAuth 2.1 (opens Warm sign-in and scope consent in your browser on first use)

## Client Configurations

### Cline (`cline_mcp_settings.json`)

Add `warm` under `mcpServers` in your Cline MCP settings:

```json
{
  "mcpServers": {
    "warm": {
      "type": "streamableHttp",
      "url": "https://app.warm.io/mcp",
      "disabled": false
    }
  }
}
```

### Claude Code / Cursor / OpenCode / Agent Plugins

```json
{
  "mcpServers": {
    "warm": {
      "type": "http",
      "url": "https://app.warm.io/mcp"
    }
  }
}
```

### Gemini CLI

Install directly as a Gemini CLI extension:

```bash
gemini extensions install https://github.com/jasonstockman/warm-agent-plugin
```

Or add to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "warm": {
      "httpUrl": "https://app.warm.io/mcp"
    }
  }
}
```

## OAuth Scopes

- **Read-only (`financial_context:read`, `transactions:read`, all plans including Free):** `get_financial_context`, `get_transactions`, `request_handoff`, `get_handoff_status`.
- **Read-and-write (`financial_records:write`, Warm Plus & Pro):** adds `find_transactions`, `get_findings`, `get_card_benefits`, `read_operation`, `describe_operation`, `invoke_operation`, `get_operation_status`. Every write operation previews via `describe_operation` and waits for explicit approval in Warm unless automatic approval is enabled in Warm Settings.
