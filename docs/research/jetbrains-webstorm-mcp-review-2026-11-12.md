# WebStorm MCP documentation review

Reviewed 2026-11-12 against the staged WebStorm Skills changes. This note records official-documentation mismatches and possible refinements; it does not claim that a tool absent from the published catalog is absent from every WebStorm session.

## Findings and recommended refinements

1. **Check the MCP router before concluding an operation is unavailable.** JetBrains documents that tools can be hidden from the direct tool list by router-only mode and invoked through the universal router. Keep live-schema validation, but distinguish unavailable in the current session from unavailable in WebStorm generally. [MCP Server: Supported tools and universal toolset](https://www.jetbrains.com/help/webstorm/mcp-server.html)

2. **Label debugger controls as session-specific, not published MCP guarantees.** The published MCP catalog documents run-configuration discovery/execution, but does not list the `ide_debug_*` controls in `skills/debugging-code/reference/debugger-tools.md`. These controls may exist in a connected tool environment; describe them as verified only for a live session whose schemas were checked. [MCP Server](https://www.jetbrains.com/help/webstorm/mcp-server.html)

3. **Make Node attach prerequisites explicit, and qualify browser debugging.** Attaching uses an Attach to Node.js/Chrome run/debug configuration, and the target Node process must run with `--inspect` or `--inspect-brk`. WebStorm browser debugging is documented for Chrome and Chromium-based browsers. [Running and debugging Node.js](https://www.jetbrains.com/help/webstorm/running-and-debugging-node-js.html), [Debug code](https://www.jetbrains.com/help/webstorm/debugging-code.html)

4. **Avoid promising automatic TypeScript alias updates during file moves.** WebStorm documents choosing “Search for references” to update references to moved files, but does not specifically promise changes to `compilerOptions.paths` or `baseUrl`. Keep the post-move alias audit; change any wording that implies those aliases are automatically updated. [Code refactoring: Move a file or a folder](https://www.jetbrains.com/help/webstorm/refactoring-source-code.html)

5. **Add MCP client setup to the README.** Enabling the server is only part of setup: JetBrains documents configuring or auto-configuring the external client and restarting it. Mention tool exposure settings, including that tools may be direct or router-only. [MCP Server: External client setup](https://www.jetbrains.com/help/webstorm/mcp-server.html)

6. **Frame reference schemas as live-session observations.** The current skill references include parameters not present in the published MCP contract, including `strong_warning` for `lint_files`, extra `rename_refactoring` arguments, and a narrow `read_file` parameter list. Do not present these as universal published contracts; instruct agents to inspect the current schema. [MCP Server](https://www.jetbrains.com/help/webstorm/mcp-server.html)

7. **Keep diagnostics conditional on configured integrations.** TypeScript and linter results depend on the project and enabled integrations; Biome support was not confirmed in the official WebStorm pages reviewed. Present Biome as conditional on availability and direct agents to use project scripts where needed. [TypeScript support](https://www.jetbrains.com/help/webstorm/typescript-support.html), [JavaScript linters](https://www.jetbrains.com/help/webstorm/linters.html)

## Potential skill coverage

The review found no mandatory specialist domain missing from the suite. A distinct **running/building JavaScript projects** workflow was added at [`skills/running-js-projects/SKILL.md`](../../skills/running-js-projects/SKILL.md) because JetBrains publishes run-configuration discovery/execution and project-build operations, which are broader than debugging or running tests. It deliberately avoids duplicating the test and runtime-diagnosis workflows. [MCP Server](https://www.jetbrains.com/help/webstorm/mcp-server.html)

The README now describes external client setup, restart, tool exposure, and router-only behavior. Skill references now distinguish the published tool catalog from a session's live direct/router schemas.

## Confirmed strengths

- WebStorm documents JavaScript/TypeScript symbol rename, top-level ES-module symbol moves, extraction, file moves, safe delete, and refactoring previews. [Refactoring JavaScript](https://www.jetbrains.com/help/webstorm/specific-javascript-refactorings.html), [Code refactoring](https://www.jetbrains.com/help/webstorm/refactoring-source-code.html)
- The published MCP catalog includes call hierarchy, code insight, file problems, batch linting, run configurations, and a universal tool router. Agents should continue resolving tools dynamically instead of assuming a fixed prefix or complete direct tool list. [MCP Server](https://www.jetbrains.com/help/webstorm/mcp-server.html)
