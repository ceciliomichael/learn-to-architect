# Module 32: Third-Party Types and Declaration Files

## Before you start

Complete Modules 01 to 31. You should understand modules, generics, classes, and advanced type expressions.

## What you will learn

- find where a library's types come from
- read a declaration file as an API description
- understand what `.d.ts` files do and do not do
- install a matching `@types` package when needed
- write a small module declaration for existing JavaScript
- understand module augmentation and its runtime limit

## Why this matters

Most projects use libraries. TypeScript needs an accurate description of each library's JavaScript API. A declaration file supplies that description but does not supply the implementation.

## 1. Three common sources of library types

### Built into TypeScript

TypeScript includes declarations for standard JavaScript APIs and selected environments through library files such as DOM and ECMAScript declarations.

### Bundled with a package

Many npm packages publish their own `.d.ts` files and point to them from `package.json`. Install the package and TypeScript resolves its bundled types.

### DefinitelyTyped packages

Some JavaScript packages have community-maintained declarations published under `@types`:

```text
npm install some-library
npm install --save-dev @types/some-library
```

Do not install an `@types` package automatically. First check whether the main package already bundles types. Duplicate or mismatched declarations can cause confusion.

## 2. What a declaration file is

A `.d.ts` file contains type declarations without an implementation:

```typescript
export function formatTitle(title: string): string;

export interface FormatOptions {
  uppercase?: boolean;
}
```

It tells TypeScript what JavaScript exists elsewhere. It emits no JavaScript.

The declaration must match runtime truth. If it claims a function returns string but the JavaScript returns a number, consumers may type-check and still fail.

## 3. Read declarations as contracts

When an import is confusing, use editor navigation to open its declaration. Look for:

- parameter and return types
- overloads
- optional properties
- generic defaults and constraints
- exported names
- comments describing runtime behavior

Do not try to understand an entire large declaration file. Start at the imported name and follow only the types it uses.

## 4. Declare an untyped module honestly

Suppose runtime JavaScript package `legacy-format` exports one function. Create `src/legacy-format.d.ts`:

```typescript
declare module "legacy-format" {
  export function format(value: string): string;
}
```

Now TypeScript can check:

```typescript
import { format } from "legacy-format";

console.log(format("hello"));
```

The declaration does not install the package. The runtime JavaScript must still exist in `node_modules`.

## 5. Avoid an empty escape declaration

This silences the missing-types error by making the module effectively `any`:

```typescript
declare module "legacy-format";
```

It may unblock a short migration, but it removes useful checking. Prefer describing the small API surface your project actually uses.

## 6. Global declarations

Some older scripts create a global value instead of a module import:

```typescript
declare const legacyVersion: string;
```

This declaration says the value exists at runtime. It does not create it. Use global declarations only when the runtime really provides the global.

Modern code usually prefers modules because dependencies are explicit.

## 7. Module augmentation

Sometimes a library supports a runtime plugin that adds behavior. TypeScript can merge matching type declarations:

```typescript
import "some-library";

declare module "some-library" {
  interface Options {
    customMode?: boolean;
  }
}
```

Augmentation changes TypeScript's understanding of an existing module. It does not install the plugin or add runtime behavior. The runtime extension must happen separately.

Module augmentation is different from declaring a missing module. Placement and whether the file is itself a module affect the meaning. Follow the target library's documented extension pattern.

## 8. Generate declarations for your own library

For a library package, TypeScript can emit public declarations:

```json
{
  "compilerOptions": {
    "declaration": true,
    "outDir": "./dist"
  }
}
```

The generated `.d.ts` files describe exported APIs. Consumers do not see unexported implementation details.

Publishing a library also requires correct package entry points, runtime module formats, and a `types` or export mapping that points to declarations. Declaration output alone does not make a package correctly publishable.

## 9. `skipLibCheck` is a tradeoff

`skipLibCheck` skips full checking of declaration file contents, which can speed builds and avoid duplicate-library conflicts. Your use of those declarations is still checked.

It can hide declaration inconsistencies. Do not use it to pretend your own public types are correct. Investigate dependency version mismatches first.

## Common mistakes

### Installing `@types` when the package bundles types

Inspect the package and TypeScript resolution first.

### Believing `.d.ts` creates runtime code

It only describes code that must already exist.

### Declaring more of a library than you have verified

Keep the declaration honest and test it against runtime behavior.

### Augmenting types without loading runtime behavior

The compiler can accept methods that do not actually exist.

## Check your understanding

1. What are the three common sources of library types?
2. Does a `.d.ts` file emit JavaScript?
3. What risk does an empty module declaration add?
4. Does module augmentation add runtime behavior?
5. Why start reading a declaration from the imported name?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 33](../33-precise-type-design/README.md) uses precision tools while keeping public APIs readable.
