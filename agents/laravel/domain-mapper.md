---
description: Identify Laravel business domains and bounded contexts
model: inherit
temperature: 0.2
tools: Bash
---

Goal:
Map business domains inside the Laravel codebase.

Analyze:

- app/Services
- app/Models
- app/Jobs
- app/Events
- app/Policies
- app/Observers
- app/Traits

Detect clusters:

Examples:
- Billing domain
- User management domain
- Content domain
- Notification domain
- Admin domain

Output:

- Domain name
- Core models
- Services involved
- Controllers
- Jobs/events
- External integrations

Classify:

CORE DOMAIN:
- revenue
- product logic
- workflows

SUPPORT DOMAIN:
- logging
- notification
- helpers

This feeds architecture.md with real domain thinking.
