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

1. Verify the current connection and workspace grant with `cio_auth_status`. Expect a healthy connection limited to Skycouchanddinner without exposing credentials.
2. List active automations. Expect `cio_prime`, skill/schema discovery, and a read-only API call that does not change workspace data.
3. Show delivery metrics for the onboarding automation over the last seven days. Expect clearly labelled metrics and no workspace changes.
4. Preview creation of a draft segment for recent signups. Expect a validated dry-run and confirmation that no segment was created.
5. Preview deletion of draft segment `123`. Expect a dry-run naming the target and confirmation that nothing was deleted.

## Negative test cases

1. `What meetings do I have tomorrow?` Customer.io should not be invoked because calendar management is outside its workflows.
2. `Draft a reply to the newest email in my Gmail inbox.` Customer.io should not be invoked because personal inbox access is outside its workflows.
3. `Open a pull request for the latest changes in my SDK repository.` Customer.io should not be invoked because source-control management is outside its workflows.

## Remaining portal evidence

- Upload the five validated skill ZIPs from `skills/` to the portal's optional Skills section. Chrome file uploads require the ChatGPT browser extension's **Allow access to file URLs** setting; the in-app browser does not expose this portal's native file picker.
- Complete the final authenticated tool rescan. The portal reached the correct EU OAuth consent flow for the `Firecorn` workspace with only the required `read` scope, but the user must approve the OAuth grant before the rescan can finish and replace the stale pre-deploy descriptors.
- Customer.io currently advertises OAuth authorization, token, dynamic client registration, and PKCE endpoints for both regions. It does not currently expose OpenID configuration or a UserInfo endpoint. Add `openid`, `email`, and UserInfo only if workspace domain restrictions are required.
- Provide a dedicated reviewer account with sample data and no MFA; the portal's test-credentials field is currently blank.
- Review and complete the portal policy attestations; do not submit until an authorized Customer.io representative has verified every attestation. Country availability is currently set to allow all supported countries.

## Read-only preflight evidence

Verified on August 23 and 25, 2026:

- A private ChatGPT Developer Mode connector (`Customer.io Dev`) was created with the Universal MCP URL, OAuth DCR, and only the `read` scope.
- Customer.io OAuth authorized workspace `Skycouchanddinner` (`226500`), and ChatGPT successfully listed its four active campaigns without making changes.
- The final 2-minute-37-second Developer Mode recording is available at `https://drive.google.com/file/d/1-g24SArgsmUG0jmEJv4KMZc6SkvButPs/view?usp=sharing`; Google Drive metadata confirms the 9,155,117-byte MP4 is readable by anyone with the link and is not discoverable in search.
- Both US and EU MCP protected-resource documents are public and advertise the correct region-specific resource URL and Customer.io scopes.
- Both authorization servers advertise authorization, token, dynamic client registration, authorization-code, and PKCE support.
- The production services code contains bidirectional OAuth authorization handoff and authenticated request routing between `mcp.customer.io` and `mcp-eu.customer.io`; targeted auth middleware tests pass, and the broader services PR CI is green.
- `customerio/services#25232` merged as `b48a00bf7d8692b2f9f416220e9222c772379ced` on August 25, 2026. Its post-merge test and deploy workflows completed successfully.
- The PR's validator regression tests drive the production MCP server options with all eight real tool descriptors, accept every JSON value returned by the dynamic API envelope, reject a malformed success result, and confirm tool errors bypass success-schema validation.
- The directory, composer, website, support, privacy, terms, and MCP documentation URLs are reachable.
- The portal issued domain-verification token `D9XrEaD9zp4PJZePXOVkD2dBhDezTRbIAwh3BgYnvK4`; both `https://mcp.customer.io/.well-known/openai-apps-challenge` and `https://mcp-eu.customer.io/.well-known/openai-apps-challenge` return HTTP 200 with that exact plain-text value. The portal verified `mcp.customer.io` successfully on August 25, 2026.
- The initial authenticated portal scan discovered all eight tools. A post-deploy authenticated MCP call successfully returned the structured `cio_auth_status` envelope and a populated nested `cio_skills_list` envelope. The portal still needs a final rescan to record the updated descriptors.
- `chatgpt-app-submission.json` validates against OpenAI's currently published `chatgpt-app-submission.v1.json` JSON Schema and contains exactly eight tools, five positive tests, and three negative tests.

## Submission-skill review findings

- Sensitive data solicitation: no tool input explicitly asks for credentials, MFA codes, payment-card data, government identifiers, biometrics, or health data. The generic API tools can access Customer.io workspace data only within the OAuth account, workspace, route, and scope checks enforced by the service; `read:sensitive` remains a separate opt-in scope.
- Tool data use: `cio_read_api`, `cio_write_api`, and `cio_delete_api` proxy validated Customer.io API operations. Their descriptions identify the method constraints and dry-run workflow, and the submission tests exercise read-only and preview behavior.
- Tool naming and descriptions: the eight `cio_*` names match the inspected implementations; no misleading or unsupported capability was found.
- Widget CSP: the MCP server exposes no widget resources, so there is no widget CSP to narrow or expand.
- Output schemas: the services PR declares an object-root `outputSchema` for every tool and returns matching structured content on successful calls. The final portal rescan after deployment is still required as production evidence.
