---
description: Correlate Laravel layers into real system architecture
model: inherit
---

Input sources:

- laravel-analyzer
- auth-analyzer
- data-analyzer
- flow-analyzer
- domain-mapper

Correlate:

Route → Middleware → Controller → Service → Model → DB
                        ↓
                       Job → Event → Queue → Worker

Output:

- true architecture topology
- cross-module relationships
- domain boundaries
- system hotspots
- critical dependencies

Avoid:

- generic layering
- assumed architecture
- repeating folder structure

This produces:

architecture that explains behavior, not folders.
