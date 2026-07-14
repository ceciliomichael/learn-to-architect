# Module 18: Modules and Code Organization

## Before you start

Complete Modules 01 to 17. You should understand functions, object types, and type-only names.

## What you will learn

- understand file scope in an ECMAScript module
- export and import named values
- export and import types
- use type-only imports
- choose small file boundaries based on responsibility
- recognize that module paths must work for the runtime

## Why this matters

A small program can fit in one file. As a program grows, separate modules make it easier to find code, reuse it, and understand which parts depend on each other.

## 1. What makes a file a module

A TypeScript file with a top-level `import` or `export` is a module.

Variables and functions in a module belong to that file unless they are exported:

```typescript
const privateMessage = "Only this module can use me";

export const publicMessage = "Other modules can import me";
```

Module scope prevents unrelated files from accidentally sharing ordinary top-level names.

A file with no top-level import or export may be treated as a script whose declarations can enter a shared global scope. In a modern module project, keep files as modules. An empty `export {};` can mark a file as a module when it otherwise exports nothing.

## 2. Named exports

Create `math.ts`:

```typescript
export function add(left: number, right: number): number {
  return left + right;
}

export function subtract(left: number, right: number): number {
  return left - right;
}

const internalLabel = "math helpers";
```

`add` and `subtract` are available to import. `internalLabel` stays inside the module.

You can also export after declarations:

```typescript
function multiply(left: number, right: number): number {
  return left * right;
}

export { multiply };
```

## 3. Named imports

Create `main.ts`:

```typescript
import { add, subtract } from "./math.js";

console.log(add(5, 3));
console.log(subtract(5, 3));
```

The names inside braces must match exported names. An alias can provide a local name:

```typescript
import { subtract as minus } from "./math.js";

console.log(minus(5, 3));
```

The `.js` path may look surprising inside TypeScript. In a Node.js ECMAScript module project, the emitted file is `math.js`, so the runtime import needs that path. TypeScript's Node module resolution maps it back to `math.ts` while checking source.

Other runtimes and bundlers can use different path rules. Module settings should match the tool that will actually load the JavaScript.

## 4. Export types

Create `task.ts`:

```typescript
export interface Task {
  id: string;
  title: string;
  isComplete: boolean;
}

export function completeTask(task: Task): Task {
  return {
    ...task,
    isComplete: true,
  };
}
```

Both the interface and function are exported, but only the function becomes a runtime JavaScript value.

## 5. Use `import type` for type-only imports

```typescript
import { completeTask } from "./task.js";
import type { Task } from "./task.js";

const task: Task = {
  id: "task-1",
  title: "Study modules",
  isComplete: false,
};

console.log(completeTask(task));
```

`import type` states that `Task` is used only by the type checker. It is removed from emitted JavaScript.

This distinction is enforced clearly when `verbatimModuleSyntax` is enabled in Module 19.

TypeScript also supports a combined form:

```typescript
import { completeTask, type Task } from "./task.js";
```

Use whichever form remains easiest to scan in the file.

## 6. Named and default exports

A module may have one default export:

```typescript
export default function greet(name: string): string {
  return `Hello, ${name}`;
}
```

The importer chooses its local name:

```typescript
import createGreeting from "./greet.js";
```

Named exports make names consistent across files and allow several clear exports from one module. This course prefers named exports for its examples. Default exports are still valid and common in some frameworks.

## 7. Avoid circular dependencies

A circular dependency occurs when module A imports B while B also imports A, directly or through other modules.

Some cycles work, while others produce partially initialized values or confusing design. If two files depend on each other, look for:

- a shared type that can move to a third module
- a function that belongs with the data it uses
- two responsibilities that should be one module
- a dependency direction that can be simplified

Do not create extra files only to satisfy a rule. Split code when the boundary makes the program easier to understand.

## 8. Organize by responsibility

A small task program might use:

```text
src/
  index.ts
  task.ts
  task-list.ts
```

- `task.ts` defines the task shape and operations on one task.
- `task-list.ts` works with collections of tasks.
- `index.ts` creates data and coordinates the program.

This is one possible layout, not a required pattern for every project.

## 9. Avoid large re-export files by default

An `index.ts` that re-exports many modules is sometimes called a barrel file. It can create a convenient public entry point for a package. It can also hide dependency paths and make cycles easier to create.

Use re-exports deliberately at a real boundary. Do not add a barrel to every folder automatically.

## Common mistakes

### Importing a name that was not exported

Check the spelling and whether the source declaration has `export`.

### Using a type as a runtime value

Interfaces and type aliases disappear. Import them with `import type` when they are used only in type positions.

### Choosing path syntax without considering the runtime

The emitted JavaScript loader must be able to resolve the same module.

### Splitting every small function into its own file

File boundaries should improve understanding, not maximize file count.

## Check your understanding

1. What makes a TypeScript file a module?
2. What remains private when a declaration is not exported?
3. Why use `import type`?
4. Why does a Node ESM TypeScript source import use a `.js` path in this course?
5. When is a re-export file useful, and what risk can it add?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 19](../19-typescript-projects-and-compiler-settings/README.md) creates the project configuration that checks and builds these modules consistently.
