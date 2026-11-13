---
name: customerio-sdk
description: >
  Customer.io SDK and app integration. Use to install or troubleshoot
  JavaScript, Node, iOS, Android, React Native, Expo, or Flutter SDKs, sandbox
  testing, first sends, Live Activities, or going live.
---

# Customer.io SDK

1. Confirm the `customerio` MCP server is connected. If the user has no Customer.io account, follow *No Customer.io account yet?* below first.
2. Call `cio_prime`.
3. Read `cio` with `cio_skills_read`, then the matching subfile such as `cio/sdk_setup.md`, `cio/integration.md`, `cio/integration_web.md`, `cio/integration_mobile.md`, `cio/integration_backend.md`, `cio/sdk_troubleshooting.md`, `cio/sandbox.md`, or `cio/go-live.md`.
4. For Pipelines source settings and write keys, also read `cdp-api/sources.md`.
5. Do not put service-account tokens in application code. Use source write keys for behavioral data and App API keys for backend transactional sends.

## No Customer.io account yet?

The MCP server signs in to an existing account through OAuth, so it can't create one. When the user has no Customer.io account, create it with the Customer.io CLI. Don't send them to sign up on the website.

1. Install the CLI: `npm install -g @customerio/cli`.
2. Run `cio skills read cio/auth.md` and follow its signup section (`cio auth signup start`, then `cio auth signup verify`). This file is CLI-only, so `cio_skills_read` can't serve it.
3. Signup emails the user a code. Ask the user for it and wait. Never guess a code.
4. After signup, keep going with the CLI: run `cio prime` and follow its rules.
5. To use this plugin's MCP server with the new account: if the `signup verify` response has an `mcp` object, MCP is already on, so connect the MCP server. If it doesn't, an account admin turns on **Customer.io MCP** at https://fly.customer.io/settings/ai first.
