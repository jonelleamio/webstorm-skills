# WebStorm navigation operations

Find tools dynamically using live names/descriptions and inspect the active schemas before calling. The MCP namespace may vary by IDE and version; never hardcode it. WebStorm tools may be hidden from the direct list when router-only mode is enabled. Check the universal router when an operation is absent, and invoke it only with its live schema. The published catalog includes symbol/file/text search, call hierarchy, file reading, and external-symbol search; it does not list dedicated Find Usages or Find Implementations operations.

## Verified operations

| Operation | Common parameters; inspect the full live schema | Use |
|---|---|---|
| `search_symbol` | Required `q`; optional `paths` (string array), `include_external` (boolean), `limit` (integer) | Locate a project symbol; set `include_external` only when searching SDK/library symbols. |
| `search_file` | Required `q` glob; optional `paths`, `includeExcluded`, `limit` | Find files by name or glob. |
| `search_text` / `search_regex` | Required `q`; optional `paths`, `limit` | Find literal text or patterns such as `export * from`. |
| `analyze_calls` | Required `symbolFqn`, `analysisKind` (`INCOMING_CALLS` or `OUTGOING_CALLS`); optional `depth`, `maxChildren`, `maxNodes`, `treePath`, `childOffset`, `timeout` | Trace calls when the IDE has a hierarchy provider. |
| `read_file` | Required `file_path`; range options vary by schema | Read project or dependency sources, including `.d.ts` files. |
| `get_symbol_info` | Required `filePath`, `line`, `column` | Confirm a symbol's resolved declaration and type at a known position. |

Use only a direct or router tool actually exposed by the session. Do not assume a `find_usages` or `find_implementations` operation exists just because another JetBrains IDE exposes one; if neither direct nor router access is available, use WebStorm UI.

## UI relationships

- **Usages:** place the caret on the symbol and use **Find Usages** (`Alt+F7` on the default keymap); review scope and results.
- **Implementations:** use **Go to Implementations** (`Ctrl+Alt+B` on the default keymap) on the interface, abstract type, or member. Inspect indirect implementations too.
- **Declaration/type:** use **Go to Declaration** and the TypeScript quick documentation/type information for the exact resolved target.

Use **Find Action** when shortcuts differ. For files in `node_modules`, enable library/external search if available, then open the exact `.d.ts` path. Do not infer a runtime implementation from declaration-only types.

## Barrels and text-only references

Start from the consuming import, follow its resolved target to `index.ts`, then follow each re-export until reaching the defining module. For an `export *`, search that barrel's target for the named export; for aliases, record both exported and local names. Use text search for dynamic imports, registry strings, comments, and configuration references because those may not be symbol usages.
