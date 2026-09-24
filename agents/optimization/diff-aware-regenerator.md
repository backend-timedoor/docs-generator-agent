---
description: Update documentation only for changed Laravel components
model: inherit
tools: Bash
---

Read:

git diff
git status

Detect changes in:

- routes → update api.md
- models → update database.md
- services → update architecture.md
- jobs/events → update flow docs
- config → update development.md

Output:

- which docs must regenerate
- which remain unchanged

Now docs scale for large repos.
