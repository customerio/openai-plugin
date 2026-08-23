---
name: customerio-design-studio
description: >
  Customer.io Design Studio. Use to create, edit, review, or publish emails,
  components, global styles, connected emails, or email accessibility and QA.
---

# Customer.io Design Studio

1. Confirm the `customerio` MCP server is connected.
2. Call `cio_prime`.
3. Read `design-studio` with `cio_skills_read`, then the relevant subfile such as `design-studio/nodes.md`, `design-studio/email_review.md`, or `design-studio/journeys.md`.
4. Discover endpoints with `cio_schema`.
5. Read with `cio_read_api`. Mutate with `cio_write_api` and `dry_run: true` first.

Wiring a finished email into an automation, broadcast, or transactional message uses Journeys. Audience and send logic belongs in `customerio-journeys`.
