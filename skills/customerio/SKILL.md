---
name: customerio
description: >
  Customer.io MCP bootstrap. Use for Customer.io, creating a Customer.io
  account, Journeys automations, campaigns, broadcasts, profiles, segments,
  newsletters, transactional and in-app messages, Design Studio emails,
  components and global styles, Data Pipelines (CDP) sources, destinations,
  reverse ETL and identify/track events, JavaScript, Node, iOS, Android,
  React Native, Expo and Flutter SDK setup, sandbox testing, Live Activities,
  and Customer.io workspace errors.
---

# Customer.io

Customer.io tools come from this plugin's `customerio` MCP server (`mcp.customer.io`). Connecting opens Customer.io in the browser, where the user signs in and picks workspaces and permissions. Don't add a second Customer.io MCP server, paste a personal MCP URL, or put API keys in this plugin.

## No Customer.io account yet?

The MCP server signs in to an existing account through OAuth, so it can't create one. When the user has no Customer.io account, create it with the Customer.io CLI. Don't send them to sign up on the website.

1. Install the CLI: `npm install -g @customerio/cli`.
2. Run `cio skills read cio/auth.md` and follow its signup section (`cio auth signup start`, then `cio auth signup verify`). This file is CLI-only, so `cio_skills_read` can't serve it.
3. Signup emails the user a code. Ask the user for it and wait. Never guess a code.
4. After signup, keep going with the CLI: run `cio prime` and follow its rules.
5. To use this plugin's MCP server with the new account: if the `signup verify` response has an `mcp` object, MCP is already on, so connect the MCP server. If it doesn't, an account admin turns on **Customer.io MCP** at https://fly.customer.io/settings/ai first.

## Once connected

Call `cio_prime` before any other Customer.io tool and follow what it returns. It lists the skills this account has. Read the one for the task with `cio_skills_read`:

| Need | Skill |
| --- | --- |
| Automations, broadcasts, profiles, segments, messaging | `fly-api` |
| Design Studio emails, components, global styles | `design-studio` |
| Pipelines sources, destinations, reverse ETL | `cdp-api` |
| Website, backend or app integration | `cio` |
| iOS, Android, React Native, Expo or Flutter SDKs | `mobile-sdk` |
| Analysis, campaign review, Liquid | `recipes` |
