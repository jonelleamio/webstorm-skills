# WebStorm refactoring tools and UI paths

Resolve tools at runtime by their operation name or description. MCP namespaces can differ across JetBrains IDEs and versions; use the full tool name and JSON schema currently exposed, not a remembered prefix or guessed parameters. WebStorm tools may be router-only and omitted from the direct list; check the universal router when an operation is absent, and use it only with its live schema. The published MCP catalog documents symbol search, semantic rename, file diagnostics, and linting, but does not list dedicated file-move, safe-delete, or extract operations.

## Published MCP operations

| Operation | Selected parameters documented in the published MCP catalog; inspect the live schema | Use |
|---|---|---|
| `search_symbol` | Required `q`; optional `paths` (string array), `include_external` (boolean), `limit` (integer) | Find a declaration before refactoring. |
| `rename_refactoring` | Required `pathInProject`, `symbolName`, `newName`; `projectPath` when known | Rename a resolved symbol. Check the live schema for additional parameters or disambiguation support. |
| `get_file_problems` | Required `filePath`; optional `projectPath`, `errorsOnly`, `timeout` | Inspect diagnostics for one changed file. |
| `lint_files` | Required `files` (string array); optional `projectPath`, `min_severity`, `timeout` | Inspect several changed files together. |

`rename_refactoring` is for symbols, not an assumed file-move API. Do not serialize command-line flags into a generic tool or infer unlisted parameters. A preview is analysis only; apply only when the returned result confirms it was applied. Documentation describes the published contract; the live schema for this session remains authoritative.

## WebStorm UI operations

- **Rename symbol:** place the caret on its declaration or reference and use **Refactor > Rename** (default shortcut: `Shift+F6`). Review the usage list, including JSX/TSX, Vue, Angular, and Svelte templates, before applying.
- **Move or rename file:** use **Refactor > Move** or **Refactor > Rename** from the Project view. For moves, enable **Search for references** and review the preview. Then verify relative imports and aliases configured by `compilerOptions.paths` and `baseUrl` in `tsconfig.json`; automatic alias updates are not guaranteed.
- **Safe delete:** use **Refactor > Safe Delete** and review the reported references; do not replace it with an unconditional file deletion.
- **Extract:** use the relevant **Refactor > Extract/Introduce** action for functions, types, or components. Check inferred parameters, return values, imports, and JSX/framework-specific boundaries before accepting.

Menus and shortcuts can vary by keymap and WebStorm version. If an action is absent, use **Find Action** to locate it and do not claim it ran through MCP.

## After the refactor

Use IDE file problems or linting for changed files. Search for plain-text uses (comments, documentation, string-based registries, CSS class strings) separately: semantic refactorings may intentionally leave these unchanged. For framework-specific bindings and style references, apply the same cross-file audit used by the frontend framework workflow.
