---
name: customerio
description: >
  Customer.io MCP bootstrap. Use for Customer.io, Journeys, CDP Pipelines,
  Design Studio, sandbox testing, app integration, SDK setup, transactional
  messaging, sources, destinations, identify/track events, and Customer.io
  workspace errors.
---

# Customer.io

Use the official Customer.io MCP server bundled with this plugin, then drive the workspace with its live tools and hosted skills.

## Connect

1. Confirm the `customerio` MCP server is enabled and complete Customer.io OAuth.
2. Select the workspaces and minimum permission scopes needed for the task.
3. This local draft targets the US data center at `mcp.customer.io`. EU accounts use `mcp-eu.customer.io`; select the EU endpoint in the published plugin or update the local MCP URL before connecting.
4. Do not paste personal MCP URLs, API keys, or service-account tokens into plugin files.

## First calls

Call `cio_prime` before other Customer.io tools. It returns the current rules for schema lookup, pagination, dry-run writes, and hosted skill discovery.

Then use:

- `cio_auth_status` when authentication or workspace access is unclear.
- `cio_schema` to discover endpoints. Never guess paths or field names.
- `cio_skills_list` and `cio_skills_read` for task-specific workflows.
- `cio_read_api` for GET requests.
- `cio_write_api` and `cio_delete_api` with `dry_run: true` before execution.

## Route to live skills

| Need | Read with `cio_skills_read` |
| --- | --- |
| Builder, SDK, sandbox, first send, go-live | `cio` |
| Automations, campaigns, broadcasts, profiles, segments, messaging | `fly-api` |
| Design Studio emails, components, global styles, publishing | `design-studio` |
| CDP sources, destinations, reverse ETL, identify/track | `cdp-api` |
| Analysis, campaign review, goals, Liquid | `recipes` |

Prefer the hosted skills over copied playbooks so instructions stay current with Customer.io.

## Terminology and safety

- Automations are the `campaigns` API resource.
- Profiles are the `customers` API resource.
- Dry-run every write and delete before executing it.
- Do not embed service-account tokens (`sa_live_...`) in application code.
- Use CDP source write keys for SDK identify/track/page/screen calls.
- Use workspace-scoped App API keys for backend transactional sends.
- Do not return raw customer PII unless the user explicitly requests it.
