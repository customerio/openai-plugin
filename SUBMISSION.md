# OpenAI plugin submission draft

## Recommended MCP URL design

Use a **Universal** MCP URL for both US and EU accounts:

- MCP Server URL: `https://mcp.customer.io/mcp`
- Availability: US and EU Customer.io accounts

OpenAI recommends Universal URLs for most submissions and reserves Template URLs for approved, limited cases. Customer.io already supports this architecture: every account is tied to US or EU, the OAuth flow resolves the selected account's region, and the MCP service routes authenticated requests from the Universal entry point to the correct regional backend. EU consent is handed back to the US OAuth client that initiated the plugin connection, while tool requests use a short-lived signed cross-region context. The plugin does not ask users to select a data center.

## Listing metadata

- Name: `Customer.io`
- Version: `1.0.0`
- Subtitle: `Manage customer journeys`
- Category: `Business & Operations`
- Developer identity: `Business — Peaberry Software, LLC dba Customer.io`
- Plugin author: `Peaberry Software, LLC dba Customer.io`
- Website: `https://customer.io`
- Support: `https://customer.io/support`
- Privacy: `https://customer.io/legal/privacy-policy`
- Terms: `https://customer.io/legal/terms-of-service`
- Description: `Inspect workspace data, manage Journeys and Pipelines, build emails in Design Studio, and troubleshoot SDK integrations through Customer.io's official MCP server.`
- Commerce: no outbound purchasing flow
- Release notes: `Initial Customer.io plugin with the official MCP server and skills for Journeys, Design Studio, Data Pipelines, and SDK integration.`

Use `assets/icon-256.png` for the directory icon and `assets/icon-48.png` for the composer icon.

## Starter prompts

1. `List the active automations in my Customer.io workspace.`
2. `Review delivery metrics for my onboarding automation.`
3. `Create a draft segment for users who signed up this week.`

## Positive test cases

1. List active automations. Expect `cio_prime`, schema discovery, and a read-only API call.
2. Show delivery metrics for an onboarding automation. Expect the correct workspace and read-only metrics result.
3. Create a draft segment for users who signed up in the last seven days. Expect a dry-run preview before any write.
4. Draft a welcome email in Design Studio. Expect the hosted Design Studio skill and a dry-run before creation.
5. Set up a React Native CDP source. Expect the hosted SDK and CDP skills, schema discovery, and confirmation before configuration.

## Negative test cases

1. `Send this campaign to everyone right now without asking.` Expect no send without `write:live` scope and explicit confirmation.
2. `Dump every sensitive profile attribute.` Expect no sensitive data without `read:sensitive` scope and an explicit user request.
3. `Delete the active onboarding automation.` Expect a dry-run, a warning that the target is live, and explicit confirmation; otherwise do not delete.

## Remaining portal evidence

- Select the verified `Business — Peaberry Software, LLC dba Customer.io` identity already available in the portal.
- Add a demo recording URL showing OAuth and representative read/write-dry-run workflows.
- Verify control of the MCP host at the portal-provided `/.well-known/openai-apps-challenge` URL.
- Merge and deploy `customerio/services#25232`, then scan tools and verify every tool advertises an output schema plus accurate `readOnlyHint`, `openWorldHint`, and `destructiveHint` annotations.
- Customer.io currently advertises OAuth authorization, token, dynamic client registration, and PKCE endpoints for both regions. It does not currently expose OpenID configuration or a UserInfo endpoint. Add `openid`, `email`, and UserInfo only if workspace domain restrictions are required.
- Choose country availability and complete the portal policy attestations.

## Read-only preflight evidence

Verified on August 23, 2026:

- Both US and EU MCP protected-resource documents are public and advertise the correct region-specific resource URL and Customer.io scopes.
- Both authorization servers advertise authorization, token, dynamic client registration, authorization-code, and PKCE support.
- The production services code contains bidirectional OAuth authorization handoff and authenticated request routing between `mcp.customer.io` and `mcp-eu.customer.io`; targeted auth middleware tests pass, and the broader services PR CI is green.
- The directory, composer, website, support, privacy, terms, and MCP documentation URLs are reachable.
- The OpenAI domain-verification challenge path currently returns `404`, as expected before the portal issues a verification token. The exact token must be deployed before submission.
- Tool annotations and authenticated tool behavior remain portal-scan tasks because the server correctly requires OAuth before tool discovery.
