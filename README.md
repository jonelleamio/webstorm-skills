# WebStorm Skills

A suite of [Agent Skills](https://agentskills.io/) for WebStorm and the JavaScript/TypeScript ecosystem. These skills guide coding agents through project execution, semantic navigation and refactoring, Node/browser debugging, frontend diagnostics, and JavaScript test discovery and authoring.

## What's included

| Skill | Purpose |
| --- | --- |
| [`running-js-projects`](skills/running-js-projects/SKILL.md) | Discover and run project scripts, WebStorm run configurations, and supported builds without assuming a package manager or command. |
| [`refactoring-code`](skills/refactoring-code/SKILL.md) | Refactor TypeScript/JavaScript symbols, modules, and framework code with WebStorm's semantic refactoring engine; use IDE actions for operations not exposed through MCP. |
| [`navigating-code`](skills/navigating-code/SKILL.md) | Find symbol usages and implementations, trace barrel exports, and inspect external `.d.ts` definitions. |
| [`debugging-code`](skills/debugging-code/SKILL.md) | Investigate runtime behavior in Node.js, Vitest/Jest, and JavaScript Debug configurations for Chrome/Chromium. |
| [`discovering-tests`](skills/discovering-tests/SKILL.md) | Locate unit, integration, and E2E tests using IDE search and JavaScript ecosystem conventions. |
| [`ts-eslint-diagnostics`](skills/ts-eslint-diagnostics/SKILL.md) | Use configured TypeScript and linter diagnostics for fast feedback before full builds. |
| [`frontend-framework-ops`](skills/frontend-framework-ops/SKILL.md) | Handle multi-file React, Vue, Angular, Svelte, CSS Modules, Tailwind, and barrel-export changes safely. |
| [`js-test-authoring`](skills/js-test-authoring/SKILL.md) | Author Vitest, Jest, or Playwright tests using the project's real types, fixtures, and mocks. |

## How it works

Each `SKILL.md` contains concise triggers, decision gates, workflows, and anti-patterns. Detailed tool contracts and framework-specific edge cases live in `reference/` files and are loaded as needed.

At runtime, skills resolve JetBrains IDE tools from the names and descriptions exposed in the current session, then inspect live parameter schemas. They do not assume a fixed MCP server prefix or that the direct tool list is complete: WebStorm can make tools router-only, available through its universal `execute_tool` router. If an operation is absent from the direct list, check whether a router is available and use it only with its live schema and verified operation details. If neither route provides the operation, use the appropriate WebStorm UI or fall back to `rg` and standard file tools; report which IDE-backed checks were skipped. Reference tables describe documented or previously observed interfaces, not guarantees about every WebStorm version or MCP session.

## Requirements and setup

- **JetBrains WebStorm** with the target JavaScript/TypeScript project open.
- **IDE as MCP Server** enabled in WebStorm. In its settings, review the project access prompt before enabling the server.
- An agent that supports Agent Skills and MCP.

Configure the agent as an external MCP client in the MCP Server settings. Use **Auto-Configure** when available, or copy the appropriate manual transport configuration into the client's settings, then restart the client. In **Exposed Tools**, confirm the needed tools are enabled; router-only tools require the client to expose the universal router. See the [official WebStorm MCP Server setup](https://www.jetbrains.com/help/webstorm/mcp-server.html).

Start the agent from the project directory opened in WebStorm so IDE indexing, language services, and run configurations refer to the same project.

## Install

### Claude Code

```text
/plugin marketplace add jonelleamio/webstorm-skills
/plugin install webstorm-skills@webstorm-skills
/reload-plugins
```

### Codex

```bash
codex plugin marketplace add jonelleamio/webstorm-skills
```

Then run `/plugins` in Codex and install **WebStorm Skills** from the marketplace browser.

### Manual

For agents without plugin support, copy or symlink individual folders from `skills/` into `~/.claude/skills/` or `<project>/.claude/skills/`.

## Repository layout

| Path | Contents |
| --- | --- |
| `skills/` | The eight Agent Skills, one folder each. |
| `skills/<skill>/SKILL.md` | Skill triggers, workflow, guardrails, and concise fallback behavior. |
| `skills/<skill>/reference/` | Detailed tool contracts and framework patterns, loaded on demand. |
| `skills/<skill>/metadata.json` | Skill version and content hash. |
| `.claude-plugin/` | Claude Code plugin and marketplace manifests. |
| `.codex-plugin/` | Codex plugin manifest. |

## Contributing

The `Validate` workflow checks skill frontmatter against the Agent Skills specification, validates plugin manifests and their shared name/version, checks local Markdown/reference links, and verifies each skill's `metadata.json`. After changing a skill, raise its version and update its hash with:

```bash
python3 .github/scripts/check_skill_metadata.py
```

## License

Licensed under the [Apache License 2.0](LICENSE).
