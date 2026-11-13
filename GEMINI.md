# DocQuery

The `docquery` MCP server is read-only. It exposes a workspace's spreadsheet tables and PDF-extracted tables as one relational dataset.

- Start with `list_tables` to see table slugs and typed columns, then `list_relations` to see foreign keys between tables.
- Use `query_table` to filter rows and `related_rows` to follow a relation (for example, a customer's invoices).
- Rows extracted from PDFs record the source file and page; cite them when answering.
- Sign-in is OAuth (scope `mcp:read`). To try example data without an account, use the header `Authorization: Bearer dq_demo_readonly`.
