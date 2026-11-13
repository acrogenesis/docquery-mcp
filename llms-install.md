# Installing the DocQuery MCP server (for AI agents)

DocQuery is a **remote** MCP server. Do not clone, build, or run anything. Only add a config entry.

1. Ask the user for a DocQuery API key (created in their workspace at https://docquery.io). If they just want to try it, use the public read-only demo key `dq_demo_readonly`.
2. Add this server to the MCP settings file:

```json
{
  "mcpServers": {
    "docquery": {
      "type": "streamableHttp",
      "url": "https://docquery.io/api/v1/mcp",
      "headers": { "Authorization": "Bearer <API_KEY>" }
    }
  }
}
```

3. Verify by calling the `list_tables` tool. With the demo key it returns sample tables such as `example_customers` and `example_invoices`.

All tools are read-only: `list_tables`, `list_relations`, `query_table`, `related_rows`.
