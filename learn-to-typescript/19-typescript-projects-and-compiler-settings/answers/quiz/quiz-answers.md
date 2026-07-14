# Module 19 Quiz Answers

## Answer 1

`package.json` describes the JavaScript package, scripts, dependencies, and runtime package mode. `tsconfig.json` defines the TypeScript project files and compiler checking, resolution, and output behavior.

## Answer 2

`npm run check`, which runs `tsc --noEmit`.

## Answer 3

It adds the possibility of `undefined`, revealing that the requested index or key may not exist.

## Answer 4

It distinguishes an absent optional property from a present property containing undefined unless undefined is explicitly part of the value type.

## Answer 5

The emitted JavaScript must use paths and module syntax the actual loader understands. Type checking is most accurate when it models that same environment.
