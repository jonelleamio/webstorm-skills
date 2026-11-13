# JavaScript test authoring reference

## Pick the repository's framework

Read the relevant `package.json` scripts and runner configuration, then match the nearest tests. Do not add a dependency or assume package-manager commands.

- **Vitest:** follow existing `describe`/`it`/`test` and `expect` patterns, setup files, fake-timer conventions, and module-mocking style.
- **Jest:** follow the project's environment, setup, mock lifecycle, and TypeScript transform conventions.
- **Playwright:** prefer existing page objects, fixtures, and locator conventions; assert user-visible behavior and use the configured browser/project.

Use the installed version's actual types and source declarations for mocks and test utilities. Keep tests isolated and avoid asserting implementation details unless the existing suite requires them.

## Resolve the real API

Discover current IDE tools and read their live schemas. If a tool is absent from the direct list, check whether the universal router is exposed; do not guess router commands. Search operations include `search_symbol`; position-based symbol inspection uses `get_symbol_info`, and source reading uses `read_file`. Treat parameter lists in this reference as examples, not exhaustive contracts. Use symbol search to find the declaration, read it, then use position-based symbol info only with the actual location. Do not infer parameter or return types from an example call.

## Validate and run

Use `get_file_problems` for one changed file or `lint_files` for several, with the live schemas. Run the existing test run configuration via `execute_run_configuration` when available; its verified modes are a named `configurationName` or a `filePath` plus `line`. Otherwise follow the package's existing script and package manager. Do not invent a run configuration or claim tests passed without output.

When WebStorm is unavailable, inspect source and tests with `rg` and standard file tools, and explicitly report skipped symbol/type resolution and IDE diagnostics.
