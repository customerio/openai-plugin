# Customer.io plugin for ChatGPT and Codex

Official Customer.io plugin for **ChatGPT** and **Codex**: the hosted **MCP
connector** (`mcp.customer.io`) plus **skills** for Journeys, Data Pipelines,
Design Studio, and SDK setup.

## Install

Install **Customer.io** from the ChatGPT plugin directory once the listing is
live. The listing is currently awaiting OpenAI review. Until then, follow the
[setup documentation](https://docs.customer.io/ai/plugins/chatgpt-codex/).

## Connect

The first use triggers Customer.io OAuth. Pick the workspaces and permission
scopes you need; read, write, and delete access are granted independently.

The plugin uses the Universal entry point `https://mcp.customer.io/mcp` for
both US and EU accounts. The account's home region is resolved after login, so
users never pick a data center.

Do not paste a personal MCP URL. Do not add a second Customer.io MCP server.
No API keys or service-account tokens belong in this package.

## Skills

| Skill | Use for | Then read from MCP |
| --- | --- | --- |
| `customerio` | Bootstrap, region, dry-run, routing | `cio_prime` |
| `customerio-journeys` | Automations, profiles, segments, broadcasts, transactional, in-app | `fly-api` |
| `customerio-design-studio` | Design Studio emails and components | `design-studio` |
| `customerio-pipelines` | Sources, destinations, reverse ETL, data in/out | `cdp-api` |
| `customerio-sdk` | JS / mobile SDK install, sandbox, go-live | `cio` |

The source of truth for skill content, for the OpenAI portal; playbooks live on the MCP server (`cio_skills_read`) so they update without a plugin release.

## Docs

- Setup: https://docs.customer.io/ai/plugins/chatgpt-codex/
- Submission notes: [SUBMISSION.md](SUBMISSION.md)

## License

MIT — see [LICENSE](LICENSE).
