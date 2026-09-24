# Documentation Generator Agent

Claude Code plugin for generating verified, domain-oriented documentation for Laravel projects.

The plugin combines project analysis, flow detection, test-coverage mapping, Mermaid diagram generation, documentation validation, and optional Zensical/Docker deployment.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- A Laravel project to document
- Git (recommended; used for diff-aware regeneration)
- Docker and Docker Compose (only for the deployment step)

## Install

### Local development

Clone this repository, then load it for a Claude Code session:

```bash
git clone <repository-url> docs-generator-agent
cd <your-laravel-project>
claude --plugin-dir /absolute/path/to/docs-generator-agent
```

`--plugin-dir` loads the plugin for that session. Restart Claude Code with the same flag when testing changes to the plugin.

### Installed marketplace plugin

Install it from the Claude Code interactive prompt:

```text
/plugin marketplace add backend-timedoor/docs-generator-agent 
/plugin install docs-generator-agent@docs-generator-agent
```

Enable it in a project with `.claude/settings.json` when required:

```json
{
  "enabledPlugins": {
    "docs-generator-agent@docs-generator-agent": true
  }
}
```

The repository currently contains the plugin manifest, agents, and commands. 

## Permissions

The plugin does not grant permissions. Its agents use the effective permissions of the project where Claude Code runs.

For shared project settings, add only the commands your team accepts to `.claude/settings.json`. Use `.claude/settings.local.json` for personal settings.

Example:

```json
{
  "permissions": {
    "allow": [
      "Task",
      "Bash(ls *)",
      "Bash(grep *)",
      "Bash(cat *)",
      "Bash(git *)"
    ],
    "ask": [
      "Bash(php *)",
      "Bash(docker *)"
    ]
  }
}
```

Merge these arrays with existing settings. Do not copy an unrelated project's complete settings file. Keep Docker and deployment commands prompting unless your team explicitly approves them.

## Use

Start Claude Code in the Laravel project, then run:

```text
/docs-generator-agent:setup
```

This creates `docs/project-context.md` if it does not exist. Optional notes can seed the context file:

```text
/docs-generator-agent:setup The application serves schools and has separate admin and student portals.
```

Generate documentation:

```text
/docs-generator-agent:generate-docs
```

Use a different context file:

```text
/docs-generator-agent:generate-docs path/to/project-context.md
```

Add a task-specific request after the command, for example:

```text
/docs-generator-agent:generate-docs Focus on payment and assessment flows.
```

The command starts the `docs-orchestrator` agent. The agent delegates repository analysis to specialized agents rather than analyzing the entire repository alone.

## Pipeline

1. Read optional project context.
2. Analyze Laravel structure, authentication, data, flows, domains, diffs, and test coverage.
3. Verify applicable detailed flow agents before running them.
4. Generate flow documentation in `docs/flows/`.
5. Generate Mermaid diagrams and project documentation.
6. Validate generated documentation.
7. Repeat generation and validation until validation passes.
8. Run the Zensical/Docker deployment step only after validation succeeds.

`docs/project-context.md` is manual input. The plugin never overwrites or regenerates it.

## Generated output

Typical output includes:

```text
docs/
├── project-context.md       # Manual context; preserved
├── flows/                   # Verified detailed flow documentation
├── architecture.md
├── database.md
├── api.md
├── development.md
├── code-standards.md
└── troubleshooting.md
```

Exact files depend on the project and verified features. The agents document only behavior supported by the codebase.

## Deployment

The final deployment agent expects:

- `docs/`
- `zensical.yaml`
- `Dockerfile`
- `docker-compose.yml`

It builds and starts the site, then checks:

```text
http://localhost:8090
```

Build or deployment errors stop the pipeline and are reported. Run generation without Docker by asking Claude to stop after documentation validation.

## Repository layout

```text
.claude-plugin/plugin.json   Plugin metadata
agents/                      Orchestrator and specialized subagents
commands/setup.md            Context-file setup command
commands/generate-docs.md    Documentation generation command
```

Detailed flow agents are listed in [`agents/flow/README.md`](agents/flow/README.md).

## Development

Load the local plugin while editing it:

```bash
claude --plugin-dir /absolute/path/to/docs-generator-agent
```

Then test both commands in a disposable Laravel project. Validate plugin metadata and inspect the generated command names if Claude Code reports that a command is unavailable.

## Troubleshooting

### Command not found

Confirm the plugin is loaded:

```bash
claude --plugin-dir /absolute/path/to/docs-generator-agent
```

Use the namespaced command form:

```text
/docs-generator-agent:generate-docs
```

### Permission prompt or denial

Add the minimum required rule to the consuming project's `.claude/settings.json` or `.claude/settings.local.json`. Plugin agent frontmatter declares tools; it does not bypass permission checks.

### No deployment

Check that Docker Compose is installed and that `zensical.yaml`, `Dockerfile`, and `docker-compose.yml` exist or can be generated. Deployment happens only after documentation validation passes.

### Missing context file

This is not fatal. The generation command continues without context. Run `/docs-generator-agent:setup` when project-specific background information is useful.

## License

See [`LICENSE`](LICENSE).
