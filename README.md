# Warm Agent Plugin & Skills

Connect your AI agent to [Warm](https://warm.io) through Warm's hosted Streamable HTTP MCP server (`https://app.warm.io/mcp`), paired with workflow skills for financial check-ins, approved record updates, and confirmed credit card benefits.

Compatible with **Hermes Agent**, **Cursor**, **Claude Code**, **Codex**, **OpenCode**, **Gemini CLI**, and any agent supporting [Agent Plugins v1.0.0](https://agent-plugins.org) or `npx skills`.

## Install

### Skills (`skills.sh` / Agent Skills)

```bash
npx skills add jasonstockman/warm-agent-plugin
```

### Hermes Agent

```bash
hermes plugins install warm
hermes plugins enable warm
hermes mcp login warm
```

### Direct MCP URL (any MCP client)

```text
https://app.warm.io/mcp
```

## Included components

- **Remote MCP server (`warm`)**: Connects to Warm's hosted Streamable HTTP endpoint at `https://app.warm.io/mcp`.
- **`financial-checkin` skill**: Checks `get_financial_context`, `get_findings`, `get_transactions`, and `read_operation` while following Warm's per-tool amount sign conventions and personal-info filter.
- **`organize-finances` skill**: Looks up exact record IDs via `find_transactions` and `read_operation`, previews edits with `describe_operation`, respects Warm's approval gate (`invoke_operation`), and creates human handoffs (`request_handoff`) for bank or account actions.
- **`card-benefits` skill**: Presents confirmed credit card statement credits, protections, reset dates, conditions, and as-of dates from `get_card_benefits` without guessing enrollment or usage.

## Authentication and permissions

Warm authenticates MCP clients via OAuth 2.1 (PKCE + Client ID Metadata Document). No API key or client secret is stored in this repository.

- **Read-only grant** (`financial_context:read`, `transactions:read`, available on all plans including Free): `get_financial_context`, `get_transactions`, `request_handoff`, and `get_handoff_status`.
- **Read-and-write grant** (`financial_records:write`, available on Warm Plus and Warm Pro): adds `find_transactions`, `get_findings`, `get_card_benefits`, `read_operation`, `describe_operation`, `invoke_operation`, and `get_operation_status`.

Every write operation is previewed through `describe_operation` and waits for your explicit approval in Warm by default. You can disconnect any agent at any time in Warm under **Settings > Export & API > Connected apps**.

## Disclosure

- **Hosted-only connector with no local executable code:** This package contains only JSON manifests, Markdown skills, and an icon—no local scripts, binaries, background daemons, or embedded credentials.
- **Network calls:** When enabled and authenticated, MCP tool calls go only to `https://app.warm.io/mcp` over HTTPS.
- **Read-only bank connections:** Warm connects to financial institutions read-only through Plaid. Neither Warm nor your AI agent can move money, transfer funds, or initiate payments.
- **Personal info filter:** When enabled (default for hosted read-only access), merchant names, descriptions, notes, and tags are omitted from `get_transactions`.
- **No financial advice:** Warm reports financial facts and catalog data from your accounts; it does not provide investment, tax, legal, or insurance advice.

## Links

- [Warm](https://warm.io/)
- [Warm Hosted MCP Overview](https://warm.io/financial-mcp-server/)
- [Connect Your AI Assistant](https://warm.io/connect-ai-assistant/)
- [Warm Developer Documentation](https://warm.io/developers/)
- [Privacy Policy](https://warm.io/privacy/)
- [Terms of Service](https://warm.io/terms/)
- Support: [hello@warm.io](mailto:hello@warm.io) ([warm.io/contact](https://warm.io/contact/))
