# Project execution tools

Resolve tools from the current session by their live names and descriptions. WebStorm may hide enabled tools from the direct list in router-only mode; check whether its universal `execute_tool` router is available and use it only with its live schema. Never assume a fixed MCP prefix, a complete direct list, or undocumented parameters.

## Run configurations

Use `get_run_configurations` to list existing configurations or discover executable code locations. Use `execute_run_configuration` only with a listed configuration name or a discovered file/line run point. The published tool supports one-time `programArguments`, `workingDirectory`, and `envs` overrides only when the configuration reports `supportsDynamicLaunchOverrides: true`; inspect the active schema and configuration details before passing any override.

Prefer repository-defined scripts when no relevant configuration is available. Inspect `package.json` scripts, the lockfile, workspace metadata, and the script's expected package directory. Choose the matching package manager from repository evidence, not from assumptions or global defaults.

## Builds and long-running processes

Use `build_project` for an IDE project build when the operation is exposed, the project supports it, and an IDE build is appropriate. Otherwise use the existing build script. A successful tool invocation is not necessarily a successful build: inspect the reported status, diagnostics, and output.

For dev servers, use the project's configured run action or script. Determine whether the process remains active, verify readiness only through observable output or a project health check, and report when startup or readiness could not be confirmed. Do not terminate an existing/user-owned process.

## Reporting

State the exact configuration or script and working directory used, the observed result and exit status, and any timeout or missing IDE operation. Distinguish “started” from “ready” and “build completed” from “build passed.” Do not infer success from an empty or truncated output.
