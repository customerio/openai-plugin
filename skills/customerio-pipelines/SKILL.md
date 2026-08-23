---
name: customerio-pipelines
description: >
  Customer.io Data Pipelines. Use to add or inspect sources, destinations,
  reverse ETL, database syncs, identify/track/page/screen calls, and data-in or
  data-out integrations.
---

# Customer.io Pipelines

1. Confirm the `customerio` MCP server is connected.
2. Call `cio_prime`.
3. Read `cdp-api` with `cio_skills_read`, then the relevant subfile such as `cdp-api/sources.md`, `cdp-api/destinations.md`, `cdp-api/reverse_etl.md`, or `cdp-api/journeys_integrations.md`.
4. Prefer a native Pipelines source for ongoing data ingestion.
5. Discover endpoints with `cio_schema`. Mutate with `dry_run: true` first.

Use `customerio-journeys` for automations, profiles, and segments. Use `customerio-sdk` for application SDK installation.
