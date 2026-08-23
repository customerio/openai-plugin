# Customer.io plugin for ChatGPT and Codex

This draft packages Customer.io's official MCP server with focused workflows for Journeys, Design Studio, Data Pipelines, and SDK integration.

## Local test

The bundled MCP configuration targets the US endpoint, `https://mcp.customer.io/mcp`. Enable the `customerio` server, complete Customer.io OAuth, select the workspaces and minimum scopes needed, then start with `cio_prime`.

For an EU account, change the endpoint to `https://mcp-eu.customer.io/mcp` before connecting. The initial public submission should use the Universal US endpoint. A later global version can keep one Universal URL, determine the account's US or EU region during OAuth, and bind the session to the correct regional backend. OAuth discovery alone cannot change the MCP URL a client already connected to, so the Universal endpoint must perform that routing.

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
