# Exercise Solution: Build the TypeScript Node.js Course Project

Use the `package.json` and `tsconfig.json` from the lesson.

## .gitignore

```text
node_modules/
dist/
.env
.env.*
!.env.example
```

## src/main.ts

```ts
type RuntimeObservation = {
  label: string;
  sequence: number;
  recordedAt: Date;
};

function record(label: string, sequence: number): void {
  const observation: RuntimeObservation = {
    label,
    sequence,
    recordedAt: new Date(),
  };

  console.log(observation);
}

record("synchronous", 1);

setTimeout(() => {
  record("timer", 3);
}, 0);

Promise.resolve().then(() => {
  record("promise", 2);
});
```

## Verification

```text
npm run typecheck
npx tsx src/main.ts
npm run build
npm start
```

The synchronous record appears first because it runs on the current stack. The promise record appears next because promise callbacks are microtasks. The timer runs afterward in a timer phase. Both the development and compiled executions should preserve that order.

To prove the checker is active, assigning a string to `sequence` must fail because `RuntimeObservation.sequence` is a number.
