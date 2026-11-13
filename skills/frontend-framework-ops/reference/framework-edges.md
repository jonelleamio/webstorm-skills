# Framework refactoring edge cases

Resolve JetBrains IDE tools dynamically and use only currently exposed schemas. Tools may be router-only and absent from the direct list; check the universal router before concluding an operation is unavailable. Semantic rename is appropriate for indexed symbols; literal strings and generated styling references need an explicit text-search pass.

## Component and template bindings

- **React:** check prop declarations and all JSX call sites, custom hooks and their callers, generic component types, tests, and Storybook stories. A prop name may also appear in object spreads or string-based APIs.
- **Vue:** inspect `<script>`/`<script setup>`, template bindings, emits, slots, and any Options API declarations. Confirm the template still resolves to the intended script binding.
- **Angular:** inspect component inputs/outputs, decorators, template bindings, host bindings, and test fixture setup. Keep selector strings distinct from class/type names.
- **Svelte:** inspect script declarations, markup references, event handlers, stores, and component props. Check both framework-specific declarations and TypeScript types when present.

These are review surfaces, not guarantees about a particular IDE refactoring. Let WebStorm show the resolved usage preview, then verify with diagnostics.

## CSS Modules and Tailwind

CSS Module keys are often accessed as `styles.foo`, while Tailwind utilities are string literals, class arrays, or conditional expressions. Search for the old literal/key in source, templates, stylesheets, tests, snapshots, and docs. Update only matching references; avoid broad regex that can change unrelated strings. Check generated class names only through the project's configured tooling.

## File moves and barrel exports

Use WebStorm's **Refactor > Move/Rename** UI for files when no matching direct or router MCP operation exists. For moves, enable **Search for references** and review the preview. Verify `tsconfig.json` aliases as well as relative paths; do not assume aliases are updated automatically. For `index.ts`, update direct and wildcard exports and confirm public import paths used by consumers remain valid.

## Verification

Run IDE diagnostics/lint for changed files. If the IDE is unavailable, use `rg` to inventory references and standard file tools to inspect them, but report that semantic resolution, template binding checks, and IDE diagnostics were skipped.
