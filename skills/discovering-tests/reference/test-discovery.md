# Test discovery patterns

Use WebStorm's current file/symbol/text search operations when available; resolve tool names and schemas dynamically. If unavailable, use `rg --files` and `rg` with the patterns below and report that IDE search was skipped.

## Paths and names

Search the nearest package first, then the workspace:

- `**/*.{test,spec}.{js,jsx,ts,tsx,mjs,cjs,mts,cts}`
- `**/__tests__/**`
- `**/{test,tests,integration,e2e}/**`
- Framework-specific Playwright directories such as `playwright/` or `e2e/`

These are conventions, not an exhaustive inventory. Inspect `package.json` workspaces and test configuration files such as `vitest.config.*`, `jest.config.*`, and `playwright.config.*` for custom locations and aliases.

## Follow the package scripts

Read each relevant `package.json`'s `scripts` and workspace metadata. Note which script is unit, integration, watch, browser, or E2E; check whether it forwards filters or expects a package-specific working directory. Do not assume `npm test` exists or that the repository uses npm.

## Verify relevance

Match test imports and assertions to the target symbol/component rather than relying only on a filename. Read candidate tests and their fixtures/mocks. Report searched roots, runner/config clues, and likely coverage; avoid claiming exhaustive coverage when the index is incomplete or some packages were not searched.
