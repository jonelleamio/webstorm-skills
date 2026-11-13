---
name: js-test-authoring
description: Use when authoring or changing Vitest, Jest, or Playwright tests for JavaScript/TypeScript code. Resolve real source types and project mocks/fixtures first, then validate imports, types, and lint with WebStorm diagnostics before running the relevant test suite.
---

# JavaScript Test Authoring

Write tests in the framework and conventions already used by the target package.

1. Use `discovering-tests` first when existing coverage or conventions are not already known. Inspect the package scripts and runner configuration; do not add a framework by default.
2. Resolve the production symbol and inspect its actual declaration, types, and call sites through WebStorm's live symbol tools. If a tool is absent from the direct list, check for the universal router and use it only with its live schema. Read neighboring tests, fixtures, mocks, and setup files.
3. Add focused tests for the requested behavior and meaningful boundary cases. Reuse project factories and mocks; do not invent API signatures or mock shapes.
4. Run IDE diagnostics/lint on changed tests and sources. Fix unresolved imports, type mismatches, and configured lint findings before launching the relevant test configuration/script.
5. Report which diagnostics and test command/configuration actually ran.

**If WebStorm is not running or neither direct nor router access provides the needed operation:** use `rg` and standard file tools to inspect declarations and test conventions. State that semantic type resolution and IDE diagnostics were skipped; use only the repository's existing test scripts for execution.

See [framework patterns and verified IDE contracts](reference/test-authoring.md).
