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

The user can create one while connecting. Don't send them to sign up on the website.

1. Ask the user to connect this plugin's `customerio` MCP server. If the browser isn't signed in to Customer.io, the page that opens starts on creating an account. Someone who already has an account chooses Log in on that page.
2. They enter their email, then the code Customer.io emails them, and choose a data center, United States or Europe. The data center can't be changed later. No password is needed. The code goes into the browser page, so don't ask for it in chat.
3. If no code comes and Customer.io's email says they already have an account, they choose Sign in on that page. An account made from an AI client has no password yet, so they use **Forgot password?** to set one, then connect again.
4. If the browser is already signed in to Customer.io, the page goes straight to the access screen, and the connection uses that login. For a new account, they sign out of Customer.io in that browser and connect again.
5. Once they allow access, call `cio_prime` and carry on. If they end up in the Customer.io app or don't come back connected, ask them to connect again.

To use the Customer.io web app later, a new account sets a password with **Forgot password?** on the sign-in page.

### Already working in the `cio` CLI, or in a shell with no browser?

CLI signup works too.

1. Install the CLI: `npm install -g @customerio/cli`.
2. Run `cio skills read cio/auth.md` and follow its signup section (`cio auth signup start`, then `cio auth signup verify`).
3. Signup emails the user a code. Ask the user for it and wait. Never guess a code.
4. After signup, keep going with the CLI: run `cio prime` and follow its rules.
5. To use this plugin's MCP server with the new account, connect it. If an older account can't connect, an account admin turns on **Customer.io MCP** at https://fly.customer.io/settings/ai.

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
