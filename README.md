# Customer.io plugin for ChatGPT and Codex

This draft packages Customer.io's official MCP server with focused workflows for Journeys, Design Studio, Data Pipelines, and SDK integration.

## Local test

The bundled MCP configuration and public plugin both use the Universal entry point, `https://mcp.customer.io/mcp`. Enable the `customerio` server, complete Customer.io OAuth, select the workspaces and minimum scopes needed, then start with `cio_prime`.

Every Customer.io account belongs to either the US or EU region. The OAuth flow resolves the selected account's region. If it is an EU account, Customer.io completes OAuth against the original US OAuth client and routes subsequent MCP requests to `https://mcp-eu.customer.io/mcp` with a short-lived signed cross-region context. Users of this plugin therefore do not choose or configure a data center manually. Customer.io's general MCP documentation still lists both regional URLs for clients configured directly.

## Safety defaults

- Read-only access is sufficient for inspection and reporting.
- Writes and deletes must be dry-run first.
- Live-data and sensitive-data scopes are opt-in Customer.io account controls.
- API keys and service-account tokens do not belong in this package.

## Source documentation

- [Customer.io MCP setup](https://docs.customer.io/ai/mcp/get-started/)
- [ChatGPT setup](https://docs.customer.io/ai/mcp/chatgpt/)
- [OpenAI plugin packaging](https://developers.openai.com/plugins/build/plugins)
- [OpenAI submission requirements](https://developers.openai.com/plugins/deploy/submission)
