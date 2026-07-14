# Module 19 Exercises

## Exercise 1: Create the course project

Create a new project using the commands and complete `package.json` and `tsconfig.json` from the lesson. Add `src/index.ts` and `src/math.ts`.

Run all four scripts:

```text
npm run check
npm run dev
npm run build
npm start
```

Record what each command does and which ones create files.

## Exercise 2: Reveal an unchecked index

Add:

```typescript
const names = ["Ana", "Bo"];
const first = names[0];
console.log(first.toUpperCase());
```

With `noUncheckedIndexedAccess`, fix the error by checking for `undefined`. Explain why index 0 is still considered possibly absent.

## Exercise 3: Test exact optional properties

Add:

```typescript
interface Profile {
  nickname?: string;
}

const profile: Profile = { nickname: undefined };
```

Read the error under `exactOptionalPropertyTypes`. Fix it in two different ways:

1. Omit the property.
2. Change the property type to explicitly permit undefined.

## Exercise 4: Catch build output on error

Introduce a type error and run `npm run build`. Confirm that `noEmitOnError` prevents updated output. Fix the error and build again.

## Exercise 5: Explain environment matching

In your own words, explain why a browser bundler project might not copy this Node ESM configuration unchanged.

## Completion checklist

- [ ] My project has local TypeScript tools.
- [ ] I can check, run, build, and start with separate commands.
- [ ] I handled an unchecked index.
- [ ] I observed exact optional property behavior.
- [ ] My module settings match Node ESM.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
