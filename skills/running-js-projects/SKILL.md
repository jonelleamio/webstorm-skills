---
name: running-js-projects
description: Discover, build, and run JavaScript/TypeScript project scripts and WebStorm run configurations. Use when asked to start an app or dev server, execute a package script, or run a project build; use debugging-code for runtime diagnosis and test-specific skills for test workflows.
---

# Running JavaScript Projects

Use the repository's existing package scripts or WebStorm configurations; never assume a package manager, script name, or run configuration.

1. Inspect the nearest `package.json`, lockfile, workspace configuration, and relevant build/tool config. Identify the package manager, intended script, and required working directory; read unfamiliar scripts before running them.
2. Discover WebStorm run configurations or executable run points from the current tool catalog. Inspect live schemas; when a tool is absent from the direct list, check for the universal router before falling back to project scripts. Use only a verified operation and its current schema.
3. Prefer an existing matching run configuration or project script. Pass one-time overrides only when the configuration explicitly supports them. Do not invent a configuration or replace a missing script with a guessed command.
4. For requested IDE builds, use the available WebStorm build operation when supported; otherwise run the repository's documented build script. Do not run broad or expensive builds unless the task needs them.
5. Capture the actual command/configuration, working directory, output, exit status, and timeout. If a dev server is meant to stay alive, confirm startup using available output or a health check, and do not stop a process the user expects to keep running.

**If WebStorm or the required operation is unavailable:** use the project-defined script with the repository's package manager and available terminal tools. Report which IDE-backed run/build checks were unavailable; never claim success without observed output.

Use [execution-tool guidance](reference/execution-tools.md) for MCP tool discovery and result reporting.
