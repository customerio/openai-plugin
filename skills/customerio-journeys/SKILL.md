---
name: customerio-journeys
description: >
  Customer.io Journeys. Use to create, list, edit, or review automations,
  campaigns, broadcasts, profiles, people, segments, newsletters,
  transactional messages, and in-app messages.
---

# Customer.io Journeys

1. Confirm the `customerio` MCP server is connected.
2. Call `cio_prime`.
3. Read `fly-api` with `cio_skills_read`, then the relevant subfile. Common routes include `fly-api/automations.md`, `fly-api/customers.md`, `fly-api/segments.md`, `fly-api/messaging.md`, `fly-api/transactional_send.md`, and `fly-api/in_app.md`.
4. Discover the endpoint with `cio_schema`.
5. Read with `cio_read_api`. Mutate with `cio_write_api` or `cio_delete_api`, always using `dry_run: true` first.

Use `customerio-design-studio` for email content and `customerio-pipelines` for sources and destinations.
