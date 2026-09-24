---
description: Map Laravel request lifecycle and business flows
model: inherit
tools: Bash
---

Map lifecycle:

Route → Middleware → Controller → Service → Model → Job/Event

Identify:

- core business flows
- async jobs
- external integrations
- background processing

Prioritize:

1. authentication flow
2. main business flow
3. integrations
