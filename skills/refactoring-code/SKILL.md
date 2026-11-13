---
name: refactoring-code
description: Use for semantic refactoring in WebStorm projects, including renaming TypeScript/JavaScript symbols across source and framework templates, moving or renaming files, safe deletion, and extracting functions, types, or components. Trigger before changing a symbol's name or structure across files. Do not use for plain text, comments, configuration values, or behavior-only edits.
---

# Refactoring Code

Use WebStorm's indexed refactoring engine when a change affects resolved symbols or imports. Never rename a symbol with `rg` plus text replacement.

1. Discover the available JetBrains IDE MCP tools dynamically. Match the needed operation by its live name and description, inspect its current schema, and call only parameters in that schema; never assume a server prefix or a complete direct tool list. If an operation is absent, check for the universal router and use it only with its live schema.
2. Locate the declaration and inspect its type and usages. Use the semantic rename operation for supported symbol renames; use WebStorm's **Refactor** UI for file moves/renames, safe delete, and extraction when no matching direct or router MCP operation is exposed.
3. For file moves, ask WebStorm to search for and update references. Review the refactoring preview, then audit relative imports and `tsconfig.json` path aliases manually; do not assume aliases were updated automatically.
4. Run IDE diagnostics on changed files and inspect unresolved imports, template bindings, barrel exports, and affected tests.

**If WebStorm is not running or neither direct nor router access provides the needed operation:** use `rg` and standard file tools to find and update references, then check every affected file and import manually. State which semantic refactorings and IDE diagnostics were skipped; never imply that text search verified semantic references.

Do not manually edit references before applying an available semantic refactoring. See [verified tool contracts and UI paths](reference/ide-refactorings.md).
