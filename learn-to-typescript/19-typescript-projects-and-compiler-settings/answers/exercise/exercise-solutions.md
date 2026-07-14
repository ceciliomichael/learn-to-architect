# Module 19 Exercise Solutions

## Exercise 1

- `npm run check` checks all included TypeScript files and emits nothing.
- `npm run dev` runs `src/index.ts` through `tsx` without creating the course build in `dist`.
- `npm run build` type-checks and emits JavaScript and source maps into `dist` when there are no errors.
- `npm start` asks Node to run the already emitted `dist/index.js`.

The expected program output is `5`.

## Exercise 2

```typescript
const names = ["Ana", "Bo"];
const first = names[0];

if (first !== undefined) {
  console.log(first.toUpperCase());
}
```

The type describes arrays of any length, including an empty array. The compiler does not prove from the general array type that index 0 exists.

## Exercise 3

Omit the property:

```typescript
interface Profile {
  nickname?: string;
}

const profile: Profile = {};
```

Or explicitly include undefined as a possible present value:

```typescript
interface Profile {
  nickname?: string | undefined;
}

const profile: Profile = { nickname: undefined };
```

The first model says the key is absent or contains a string. The second additionally permits a present key whose value is undefined.

## Exercise 4

With `noEmitOnError`, a type error makes the compiler exit unsuccessfully without writing new output. Old files already in `dist` may still remain, so do not mistake existing output for a successful new build. After the fix, a successful build updates the output.

## Exercise 5

A browser bundler performs module loading and transformation differently from Node. Its recommended `module`, `moduleResolution`, available global APIs, and run commands can differ. Configuration should describe the actual runtime and build tool rather than being copied only because it is strict.
