---
name: debugging-code
description: Use for runtime root-cause analysis in JavaScript/TypeScript applications when values, async control flow, Node.js behavior, browser execution, or reactive state cannot be established confidently from source and logs alone. Trigger on explicit debugger requests, intermittent/runtime failures, and unclear test behavior; do not use for obvious syntax or type errors.
---

# Debugging Code

Use a narrow reproducible Node.js, Vitest/Jest, or JavaScript Debug configuration and gather runtime evidence before changing behavior. WebStorm browser debugging is supported for Chrome and Chromium-based browsers.

1. Triage the error, expected versus actual behavior, and the narrowest runnable scenario. Discover current JetBrains debugger/run tools dynamically and inspect their live schemas; do not assume a server prefix or a complete direct tool list. If an operation is absent, check for the universal router and use it only with its live schema.
2. Find an existing matching run configuration for Node.js, Vitest/Jest, or JavaScript Debug. Reuse an active relevant debug session when possible; otherwise launch the selected configuration through the verified debugger workflow.
3. Set a breakpoint at the earliest uncertain state transition. The verified MCP breakpoint operation accepts a file and line only; use WebStorm's UI for conditional breakpoints and logpoints. Use the UI to attach to an already-running process because no attach operation is exposed in the current schema.
4. At a pause, inspect the stack and evaluate relevant expressions in the selected frame. Check closure locals and framework state through the debugger's variables/expressions; inspect async frames when the runtime exposes them. Record concrete values and the exact paused location.
5. Fix only after the failing transition is demonstrated. Remove agent-created breakpoints or stop sessions started solely for the investigation.

**If WebStorm is not running or neither direct nor router access provides the required debugger operation:** use `rg`, standard file tools, existing logs, and test output to trace the likely path. Do not claim runtime state was observed; report which IDE-backed checks and runtime values remain unverified.

See [verified run/debugger contracts and UI steps](reference/debugger-tools.md).
