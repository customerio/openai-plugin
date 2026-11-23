---
name: customerio
description: >
  Customer.io MCP bootstrap. Use for Customer.io, creating a Customer.io
  account, Journeys, CDP Pipelines,
  Design Studio, sandbox testing, app integration, SDK setup, transactional
  messaging, sources, destinations, identify/track events, and Customer.io
  workspace errors.
---

# Customer.io

Use the official Customer.io MCP server bundled with this plugin, then drive the workspace with its live tools and hosted skills.

## No Customer.io account yet?

The user can create an account while connecting. Don't send them to sign up on the website.

1. Connect this plugin's MCP server `customerio`. With no Customer.io session in the browser, Connect opens the "Create your Customer.io account" page.
2. The user enters their email on that page, then the code Customer.io emails them, and picks a data center (United States or Europe). The data center can't be changed later. No password is needed. The code goes into the browser page, so don't ask for it in chat.
3. The browser moves on to the consent page, where the user picks the workspace and permission scopes and allows access.
4. Call `cio_prime` and carry on.

A user who already has an account clicks **Log in** on that page.

The new account has no password. To use the Customer.io web app later, the user chooses **Forgot password?** on the sign-in page and sets a password from the emailed link.

### Already working in the `cio` CLI?

CLI signup works too, for a session that runs the Customer.io CLI.

1. Install the CLI: `npm install -g @customerio/cli`.
2. Run `cio skills read cio/auth.md` and follow its signup section (`cio auth signup start`, then `cio auth signup verify`). This file is CLI-only, so `cio_skills_read` can't serve it.
3. Signup emails the user a code. Ask the user for it and wait. Never guess a code.
4. After signup, keep going with the CLI: run `cio prime` and follow its rules.
5. To use this plugin's MCP server with the new account: if the `signup verify` response has an `mcp` object, MCP is already on, so connect the MCP server. If it doesn't, an account admin turns on **Customer.io MCP** at https://fly.customer.io/settings/ai first.

## Connect

1. Confirm the `customerio` MCP server is enabled and complete Customer.io OAuth.
2. Select the workspaces and minimum permission scopes needed for the task.
3. The plugin uses the Universal `mcp.customer.io` entry point for both US and EU accounts. OAuth identifies the selected account's data center, and Customer.io routes EU requests to `mcp-eu.customer.io`; do not ask the user to choose a region manually.
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
