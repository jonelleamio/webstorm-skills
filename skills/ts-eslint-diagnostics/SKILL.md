---
name: ts-eslint-diagnostics
description: Use to inspect TypeScript/JavaScript type errors, unresolved imports, and configured ESLint, Biome, or Stylelint findings in WebStorm before invoking slow bundler or full type-check builds. Trigger after edits or when the user asks for IDE diagnostics.
---

# TypeScript and Lint Diagnostics

Use WebStorm's TypeScript service and configured inspections for fast, changed-file feedback before a full build.

1. Discover the current IDE file-problem/lint tools and inspect their live parameter schemas; do not assume the MCP prefix or a complete direct tool list. If an operation is absent, check for the universal router and use it only with its live schema.
2. Check the changed files with IDE diagnostics. Use batch linting for several files; confirm which project-configured inspection engines actually ran. Do not assume a Biome IDE integration is available; use the repository's configured script if not.
3. Fix actionable type errors, unresolved imports, and configured lint violations. Re-run diagnostics on the affected files.
4. Only then run a bundler or full `tsc` build if the user requested it or the change needs build-level validation; IDE inspections do not replace that validation.

**If WebStorm is not running or neither direct nor router access provides diagnostics:** inspect source/config with `rg` and standard file tools, and use only project-provided scripts if available. Clearly report that TypeScript service and IDE inspections were skipped; do not present static search as equivalent diagnostics.

See [verified diagnostics contracts and interpretation](reference/diagnostics-tools.md).
