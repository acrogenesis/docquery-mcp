# DocQuery MCP server

Remote [MCP](https://modelcontextprotocol.io) server for [DocQuery](https://docquery.io). Point Claude, Cursor, Cline or any MCP client at a spreadsheet (Excel, CSV, Google Sheets, Airtable) **and** the PDFs that belong to it (invoices, contracts), and query them together as linked relational tables. Every extracted row keeps its source file (and page where known) so the agent can cite the PDF.

This repository holds the public connection details and client configs. The server itself is hosted; there is nothing to install or run locally.

- **Endpoint:** `https://docquery.io/api/v1/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1, or an API key as `Authorization: Bearer <key>`
- **Try it now:** public read-only demo key `dq_demo_readonly` (sample customers + invoices workspace)
- **Official MCP Registry:** `io.docquery/docquery`
- **Docs:** https://docquery.io/docs · https://docquery.io/mcp-server

## Tools (read-only)

| Tool | What it does |
| --- | --- |
| `list_tables` | Tables in the workspace with their columns |
| `list_relations` | Foreign-key links between tables (e.g. invoices -> customers) |
| `query_table` | Rows from one table, with `filter`, `search`, `columns` projection, `limit`/`offset` |
| `related_rows` | Follow a relation from one row to its linked rows |

MCP access is read-only on purpose; edits happen in the DocQuery app or the REST API.

## Connect

### Claude Desktop / Cursor / Cline (JSON config)

```json
{
  "mcpServers": {
    "docquery": {
      "type": "streamableHttp",
      "url": "https://docquery.io/api/v1/mcp",
      "headers": { "Authorization": "Bearer dq_demo_readonly" }
    }
  }
}
```

Some clients use `"type": "http"` instead of `"streamableHttp"`. Replace `dq_demo_readonly` with your own key from your workspace in https://docquery.io to query your own data. Clients that support OAuth can omit the header and sign in.

### Claude Code

```bash
claude mcp add --transport http docquery https://docquery.io/api/v1/mcp \
  --header "Authorization: Bearer dq_demo_readonly"
```

### Quick check with curl

```bash
curl -s https://docquery.io/api/v1/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -H 'Authorization: Bearer dq_demo_readonly' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Pricing

Free: 5 documents, 10,000 rows, REST + GraphQL + MCP. Starter $29/mo, Pro $79/mo. See https://docquery.io.

## Support

hello@docquery.io · security reports: security@docquery.io

Built by Adrian Rangel ([@acrogenesis](https://github.com/acrogenesis)).
