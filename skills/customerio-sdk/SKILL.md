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
