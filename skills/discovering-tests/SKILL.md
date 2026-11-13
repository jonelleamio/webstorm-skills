---
name: discovering-tests
description: Use before adding tests or when asked to locate tests for a JavaScript/TypeScript module, function, or component. Find existing unit, integration, and end-to-end coverage using WebStorm search plus repository test conventions. Do not assume tests are absent from naming alone.
---

# Discovering Tests

Locate existing coverage before creating a new test or choosing a framework.

1. Inspect the target module/component and its `package.json` scripts. Discover WebStorm file, symbol, and text search tools from the current session and use their live schemas. If a tool is absent from the direct list, check for the universal router; use it only with its live schema.
2. Search nearby tests and ecosystem conventions: `*.test.*`, `*.spec.*`, `__tests__/`, `test/`, `tests/`, `integration/`, and `e2e/`. Include colocated and workspace/package-level tests.
3. Identify the actual runner and scope from scripts/config (`vitest`, Jest, Playwright, or project-specific); read an adjacent test to learn local fixtures, mocks, and naming style.
4. Report the relevant test paths and what each covers. If none are found, distinguish “no matches in searched paths” from “no tests exist.”

**If WebStorm is not running or neither direct nor router access provides the needed search:** use `rg`, standard file tools, and `package.json`/runner configuration. State that IDE-backed symbol/file search was skipped.

Do not write a new test until the existing coverage and project test conventions have been checked. See [search patterns and runner clues](reference/test-discovery.md).
