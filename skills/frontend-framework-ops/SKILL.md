---
name: frontend-framework-ops
description: Use for multi-file frontend changes where text replacement can break resolved bindings, props, hooks, templates, CSS Modules, Tailwind class references, or barrel exports. Applies to React, Vue, Angular, and Svelte projects in WebStorm.
---

# Frontend Framework Operations

Treat framework bindings as code relationships, not interchangeable text.

1. Identify the framework, component/module boundary, and relevant TypeScript/JavaScript declaration. Resolve current JetBrains IDE tools dynamically and inspect their schemas. If a needed operation is absent from the direct list, check for the universal router and use it only with its live schema.
2. Use semantic rename for resolved props, hooks, components, and types when supported. For file moves, framework template changes, safe delete, and extraction, use WebStorm's matching refactoring UI if no direct or router MCP operation is exposed.
3. For CSS Modules and Tailwind, search every literal class/reference and update declarations, templates, tests, and snapshots together. Do not assume symbol rename understands arbitrary CSS strings or generated class names.
4. Check Vue/Angular/Svelte template bindings, React JSX/TSX usage, barrel re-exports, relative imports, and `tsconfig` path aliases. Run IDE diagnostics on the changed files.

**If WebStorm is not running or neither direct nor router access provides the needed operation:** use `rg` and standard file tools to enumerate references, make targeted edits, and inspect each affected file. State that semantic bindings and IDE diagnostics were not verified.

Never use a blind regex replacement for a symbol rename or framework binding. See [framework-specific edge cases](reference/framework-edges.md).
