---
description: Run the documentation orchestrator and generate project docs
argument-hint: "[optional context file path]"
allowed-tools: Bash, Read, Write, Edit
---

Run the docs-orchestrator agent for this project.

Instructions:

1. Use `$ARGUMENTS` as the project-context file path when provided; otherwise use `docs/project-context.md`.
2. Follow `agents/docs-orchestrator.md` exactly.
3. Delegate repository analysis to the configured subagents. Do not analyze the entire repository directly.
4. Preserve `docs/project-context.md`; never overwrite or regenerate it.
5. Verify flows before documenting them. Generate only documentation supported by the codebase.
6. Run validation. Repeat generation/validation until validation passes.
7. Run the Zensical deployment step only after validation passes. Stop and report build/deployment errors; do not silently pass them.

Begin by invoking `agents/docs-orchestrator.md` with the selected context path and the user's request as the task.
