# IDE diagnostics contracts

Resolve live JetBrains tool names by operation/description and use the exact schema in the session. Do not rely on a fixed server prefix. If a tool is absent from the direct list, check for WebStorm's universal router and invoke it only with its live schema. The published `lint_files` contract lists `warning` and `error`; other severities are session/version-specific if present in the live schema.

| Operation | Common parameters; inspect the full live schema | Use |
|---|---|---|
| `get_file_problems` | Required `filePath`; optional `projectPath`, `errorsOnly` (boolean), `timeout` | Inspect one file; set `errorsOnly` false to include warnings. |
| `lint_files` | Required `files` (string array); optional `projectPath`, `min_severity` (`warning`, `error`), `timeout` | Inspect multiple changed files in one request. The live schema may vary. |

A tool error, timeout, `notAnalyzedReason`, or incomplete batch is not a clean result. Report it and retry only after correcting a concrete input issue or timeout.

## Inspection coverage

WebStorm diagnostics reflect installed/enabled language and lint integrations plus project configuration. Confirm the project has the relevant `tsconfig.json`, ESLint, Biome, and/or Stylelint configuration and that an integration for each requested engine is actually enabled. Do not imply that WebStorm provides a Biome integration unless it is available in the current installation; use the project's Biome script otherwise. Do not assume all engines ran simply because the tool returned no problems. Avoid a full bundler or type-check build for immediate feedback unless it is required by the task.

When WebStorm is unavailable, inspect config and source with `rg` and standard file tools. Static search cannot establish TypeScript types or replace ESLint/Biome/Stylelint inspections; name the skipped checks in the result.
