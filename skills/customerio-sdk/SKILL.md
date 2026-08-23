---
name: customerio-sdk
description: >
  Customer.io SDK and app integration. Use to install or troubleshoot
  JavaScript, Node, iOS, Android, React Native, Expo, or Flutter SDKs, sandbox
  testing, first sends, Live Activities, or going live.
---

# Customer.io SDK

1. Confirm the `customerio` MCP server is connected.
2. Call `cio_prime`.
3. Read `cio` with `cio_skills_read`, then the matching subfile such as `cio/sdk_setup.md`, `cio/integration.md`, `cio/integration_web.md`, `cio/integration_mobile.md`, `cio/integration_backend.md`, `cio/sdk_troubleshooting.md`, `cio/sandbox.md`, or `cio/go-live.md`.
4. For Pipelines source settings and write keys, also read `cdp-api/sources.md`.
5. Do not put service-account tokens in application code. Use source write keys for behavioral data and App API keys for backend transactional sends.
