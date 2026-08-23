# Customer.io plugin for ChatGPT and Codex

This draft packages Customer.io's official MCP server with focused workflows for Journeys, Design Studio, Data Pipelines, and SDK integration.

## Local test

The bundled MCP configuration targets the US endpoint, `https://mcp.customer.io/mcp`. Enable the `customerio` server, complete Customer.io OAuth, select the workspaces and minimum scopes needed, then start with `cio_prime`.

For an EU account, change the endpoint to `https://mcp-eu.customer.io/mcp` before connecting. The preferred public submission uses an OpenAI-approved templated MCP configuration so users select their data center during installation. If template approval is unavailable, Customer.io should provide one universal routing endpoint rather than publish separate regional plugins.

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
