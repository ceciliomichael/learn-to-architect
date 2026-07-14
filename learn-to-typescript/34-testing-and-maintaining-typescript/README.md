# Module 34: Testing and Maintaining TypeScript

## Before you start

Complete Modules 01 to 33. Use the strict project created in Module 19.

## What you will learn

- separate runtime behavior tests from compile-time type checks
- write focused tests with Node's built-in test tools
- test asynchronous success and failure
- assert intentional type errors with `@ts-expect-error`
- refactor with compiler and test feedback
- upgrade dependencies in controlled steps

## Why this matters

Types catch many invalid uses, but they do not prove calculations or runtime integrations are correct. Runtime tests and type checks protect different promises. A maintained project needs both.

## 1. Test runtime behavior

Create `src/math.ts`:

```typescript
export function add(left: number, right: number): number {
  return left + right;
}
```

Create `src/math.test.ts`:

```typescript
import assert from "node:assert/strict";
import test from "node:test";
import { add } from "./math.js";

test("add returns the sum", () => {
  assert.equal(add(2, 3), 5);
});
```

Build the project, then run the emitted test explicitly:

```text
npm run build
node --test dist/math.test.js
```

The type checker confirms that arguments and imports fit. The test confirms the actual calculation result.

## 2. Arrange, act, assert

A readable test often has three parts:

```typescript
test("completed tasks are counted", () => {
  const tasks = [
    { title: "Read", isComplete: true },
    { title: "Practice", isComplete: false },
  ];

  const result = countCompleted(tasks);

  assert.equal(result, 1);
});
```

- Arrange input.
- Act by calling the behavior.
- Assert the observable result.

Do not test private implementation steps unless they are the public behavior.

## 3. Test boundaries

For a numeric range, test:

- a normal value
- the exact lower and upper boundaries
- one value outside each boundary
- invalid or missing input when the function accepts it

Tests should target meaningful behavior, not achieve a large count without purpose.

## 4. Test thrown errors

```typescript
test("divide rejects zero divisor", () => {
  assert.throws(
    () => divide(10, 0),
    /Cannot divide by zero/,
  );
});
```

Check the behavior callers rely on. Exact full messages can make tests fragile when wording is not part of the contract.

## 5. Test asynchronous behavior

```typescript
test("loads a delayed value", async () => {
  const value = await delayValue("ready", 1);
  assert.equal(value, "ready");
});
```

Return or await the Promise so the test runner knows when the test finishes.

For rejection:

```typescript
await assert.rejects(
  () => failingOperation(),
  /expected message/,
);
```

Avoid real network calls in small unit tests. Pass a dependency or test a validator with fixed unknown values.

## 6. Type tests

Normal `tsc --noEmit` checks valid uses. Sometimes a public API also needs proof that invalid uses stay invalid:

```typescript
declare function setTheme(theme: "light" | "dark"): void;

setTheme("light");

// @ts-expect-error invalid themes must be rejected
setTheme("blue");
```

`@ts-expect-error` requires the next line to produce an error. If a future change makes the line valid, TypeScript reports that the directive is unused.

Use it for intentional negative type tests, not to silence unexplained errors in application code.

## 7. Test inferred types with assignments

```typescript
const result = getProperty({ name: "Ana", age: 24 }, "age");
const expectedNumber: number = result;

// @ts-expect-error age result must not become string
const wrongString: string = result;
```

Keep type tests near public type helpers. Deeply testing compiler implementation details can make upgrades unnecessarily painful.

## 8. Refactor in small steps

Use this sequence:

1. Start with a clean `npm run check` and passing runtime tests.
2. Make one structural change.
3. Run the type checker.
4. Run the smallest relevant tests.
5. Continue until the refactor is complete.
6. Run the full check and test set.

Compiler errors can show every call site affected by a contract change. Tests reveal behavior the static types cannot express.

## 9. Upgrade deliberately

For TypeScript or dependency upgrades:

1. Read the package's official release and migration notes.
2. Update one related group at a time.
3. Install with the project's package manager.
4. Run the type check and tests.
5. Review new errors instead of immediately weakening settings.
6. Inspect changed emitted output or declarations for library projects.

New TypeScript versions can improve checking and reveal code that was always risky. They can also change library declarations. Keep the change focused enough to understand.

## 10. Maintain comments and types

Delete obsolete `@ts-expect-error` directives, assertions, and workarounds. A suppression should include a short reason and, when appropriate, a link to the issue that requires it.

Types are part of the maintained code. Simplify types that no longer match how the program is used.

## Common mistakes

### Believing type checking replaces runtime tests

It cannot verify formulas, network behavior, or many state changes.

### Writing tests that do not await async work

They may finish before the assertion runs.

### Using `@ts-ignore` for negative type tests

Prefer `@ts-expect-error`, which fails when the expected error disappears.

### Changing compiler settings to silence upgrade errors

Investigate what changed before weakening a useful check.

## Check your understanding

1. What different promises do runtime tests and type checks protect?
2. Why must an async test await or return its Promise?
3. What makes `@ts-expect-error` useful for a negative type test?
4. Which boundary cases should a range test include?
5. Why upgrade dependencies in focused steps?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Where to go from here

There is intentionally no final assessment yet. Revisit any weak module, build small programs from the exercises, and use the compiler plus tests as feedback. The next curriculum revision should be based on learner feedback and observed difficulties rather than adding an assessment too early.
