---
name: navigating-code
description: Use to find TypeScript/JavaScript symbol usages, implementations, callers, re-exports, or external declaration files in a WebStorm project. Trigger when text search could confuse same-name symbols or miss resolved imports. Do not use for ordinary file-name lookup or plain strings.
---

# Navigating Code

Prefer WebStorm's symbol index for code relationships; use text search to trace string-based exports and configuration references.

1. Resolve the current JetBrains IDE tools dynamically from the available tool names and descriptions. Read the live parameter schema before calling; do not assume a server prefix or a complete direct tool list. If a needed operation is absent, check for the universal router and use it only with its live schema.
2. Find the declaration with semantic symbol search. Use Find Usages for all references, Go to Implementations for interface/abstract-class implementations, and call hierarchy for callers/callees.
3. Trace `index.ts` barrel exports from the importing symbol back through each `export`, including `export *` and aliased exports. Confirm the final declaration rather than stopping at the first barrel.
4. For library types, search external symbols and open the resolved `.d.ts` definition in `node_modules`; distinguish declarations from implementation code.

**If WebStorm is not running or neither direct nor router access provides a semantic operation:** use `rg` and standard file tools to search declarations, imports, and exports. Treat matches as textual evidence, not proof of resolved usages or implementations, and report which IDE-backed searches were skipped.

Never conclude that an identifier has no usages from one text search. See [verified navigation contracts and UI paths](reference/navigation-tools.md).
