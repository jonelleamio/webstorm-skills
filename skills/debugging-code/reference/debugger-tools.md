# WebStorm run and debugger operations

Resolve JetBrains IDE tools from the current session's names and descriptions, then inspect their live schemas. Do not hardcode an MCP server prefix or assume the direct list is complete. WebStorm can make tools router-only; if an operation is absent from the direct list, check for the universal router and use it only with its live schema. The published MCP catalog documents run-configuration discovery and execution, but not the `ide_debug_*` controls listed below. Treat those controls as session-specific: use them only when their live schemas are present and verified. Do not infer that a debugger operation is universally unavailable from its absence in the direct list.

## Run configurations

| Operation | Common parameters | Use |
|---|---|---|
| `get_run_configurations` | Optional `filePath`, `projectPath` | Without `filePath`, list configurations; with it, find executable locations. |
| `execute_run_configuration` | Either `configurationName` or `filePath` + `line`; optional `programArguments`, `workingDirectory`, `envs`, `timeout`, `waitForExit`, `projectPath` | Run an existing project configuration or a discovered run point. |
| `ide_debug_run` | Required `configName` (if exposed) | Session-specific operation to start a named configuration under the debugger. |

For dynamic launch overrides, use them only when `supportsDynamicLaunchOverrides` is true in the configuration listing. Choose the project's existing Node.js, Vitest/Jest, or JavaScript Debug configuration; do not invent configuration names. Vitest/Jest support depends on project scripts and available run configurations, not on a dedicated MCP test-runner operation.

## Session-specific debugger controls

| Operation | Parameters observed in this session | Use only if this live schema is available |
|---|---|---|
| `ide_debug_set_breakpoint` | Required absolute `file` path and 1-based `line` | Set a standard breakpoint. |
| `ide_debug_session_state` | No arguments | Check whether a session is running or paused and where. |
| `ide_debug_stack_trace` | No arguments | Read the paused call stack. |
| `ide_debug_evaluate` | Required `expression` | Evaluate in the current frame; read values without mutating state. |
| `ide_debug_step` | Required `direction`: `over`, `into`, or `out` | Advance a paused session. |
| `ide_debug_resume`, `ide_debug_pause`, `ide_debug_stop` | No arguments | Control the active session. |
| `ide_debug_console_output` | Optional `maxChars` | Read recent captured output. |

These are not guarantees of the published WebStorm MCP catalog. Use only parameters present in the current direct or router schema. Do not send guessed fields or invoke unverified commands through a generic executor.

## WebStorm UI-only operations

- **Attach to a running Node.js process:** start the target with `--inspect` or `--inspect-brk`, then use an **Attach to Node.js/Chrome** run/debug configuration and select the target process. Do not restart a process the user expects to keep running.
- **Conditional breakpoint:** use **Run > View Breakpoints** or the gutter breakpoint settings and enter a JavaScript expression as the condition.
- **Logpoint:** configure a non-suspending breakpoint with a log expression in the breakpoint settings.
- **Browser debugging:** use Chrome or a Chromium-based browser with the project's JavaScript Debug configuration. Verify the browser target and source maps before interpreting a mapped source location.

Names and menus vary by version/keymap; use **Find Action** if needed. If the UI operation cannot be performed, record that as a limitation rather than claiming the MCP breakpoint has condition/logpoint behavior.

## Evidence discipline

At each pause, capture the file/line, stack, and at least one relevant value. Closure locals are visible only while their lexical frame is available. Reactive framework state may be proxied or lazily evaluated; inspect the actual runtime object and avoid changing it in the debugger. Async frames may be runtime-dependent: if absent, state that the async boundary was not observed.
