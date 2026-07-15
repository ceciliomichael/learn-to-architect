# Module 01: Node.js Runtime, Event Loop, and TypeScript Project Setup

## Before you start

Complete Backend Foundations, Learn TypeScript, and Learn SQL first. This course does not reteach variables, functions, promises, modules, or TypeScript narrowing.

Install Node.js 24 LTS and open a new terminal:

```text
node --version
npm --version
```

The Node.js result should start with `v24.`.

## What you will learn

By the end of this module, you will be able to:

- create a strict TypeScript project for Node.js
- explain which code runs in Node.js and which work is performed outside JavaScript
- distinguish development execution from compiled production output
- observe the order of synchronous work, promise callbacks, and timers
- run type checking, tests, builds, and compiled code through package scripts

## 1. Create the project

Create a disposable project outside this course repository:

```text
mkdir node-api-course
cd node-api-course
npm init -y
npm install --save-dev typescript @types/node tsx
mkdir src
```

`typescript` provides the compiler. `@types/node` describes Node.js APIs to TypeScript. `tsx` runs TypeScript during development without pretending that type checking is optional.

Installed packages belong to this project. They are recorded in `package.json`, resolved in `package-lock.json`, and downloaded into `node_modules`.

## 2. Configure package scripts

Keep the dependency versions written by `npm install`. Add the project settings and scripts with npm:

```text
npm pkg set private=true --json
npm pkg set type=module
npm pkg set scripts.dev="tsx watch src/main.ts"
npm pkg set scripts.typecheck="tsc --noEmit"
npm pkg set scripts.build="tsc"
npm pkg set scripts.start="node dist/main.js"
npm pkg set scripts.test="node --import tsx --test"
```

Open `package.json` afterward. Confirm that `private` is the Boolean value `true`, not the string `"true"`, and that the installed development dependency versions are still present.

`private` prevents accidental publication. `type: module` selects ECMAScript modules. Scripts give the team one stable vocabulary even if their internal tools change later.

## 3. Configure strict TypeScript

Create `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2023",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "verbatimModuleSyntax": true,
    "sourceMap": true,
    "types": ["node"]
  },
  "include": ["src/**/*.ts"]
}
```

`NodeNext` makes TypeScript follow Node.js module rules. `rootDir` identifies authored source. `outDir` keeps generated JavaScript in `dist`. The strict options make missing values and optional properties visible rather than silently widening them.

Do not edit `dist` or `node_modules`. Both can be recreated.

## 4. Run a typed Node.js program

Create `src/main.ts`:

```ts
type CourseStatus = {
  course: string;
  ready: boolean;
};

const status: CourseStatus = {
  course: "Node.js Backend",
  ready: true,
};

console.log("1. synchronous start", status);

setTimeout(() => {
  console.log("3. timer callback");
}, 0);

Promise.resolve().then(() => {
  console.log("2. promise callback");
});

console.log("1. synchronous end");
```

Run it once:

```text
npx tsx src/main.ts
```

Expected ordering:

```text
1. synchronous start { course: 'Node.js Backend', ready: true }
1. synchronous end
2. promise callback
3. timer callback
```

Exact object punctuation can vary, but the order should not.

The current stack finishes first. Promise callbacks run from the microtask queue before timer callbacks are taken in a later event-loop phase. A zero-millisecond timer means "eligible after at least this delay," not "run immediately."

## 5. Development execution is not type checking

`tsx` transforms and executes TypeScript quickly. Run the compiler separately:

```text
npm run typecheck
```

Temporarily change `ready: true` to `ready: "yes"`. Type checking should reject the string. Restore the boolean.

Now build and execute the generated JavaScript:

```text
npm run build
npm start
```

Inspect `dist/main.js`. Type annotations are gone because Node.js executes JavaScript. The TypeScript source remains the code you maintain.

## 6. Understand Node.js work ownership

JavaScript callbacks execute on the main event-loop thread unless worker threads are introduced deliberately. Node.js and the operating system can perform network, timer, filesystem, and other work outside that JavaScript stack, then queue callbacks when results are ready.

This does not make CPU-heavy JavaScript harmless. A long calculation on the main thread delays requests, timers, shutdown handlers, and other callbacks. Later modules measure this instead of relying on slogans about "non-blocking" code.

## Common mistakes

### Treating `tsx` as the type checker

Fast development execution and complete static checking are different responsibilities. Keep `npm run typecheck` in the normal workflow.

### Installing course tools globally

Local development dependencies make the project reproducible. Scripts automatically find binaries in the local `node_modules` folder.

### Assuming every task runs in parallel

The event loop schedules callbacks. Ordinary JavaScript still runs one callback at a time on its thread.

### Committing generated or installed files

Commit source, configuration, `package.json`, and `package-lock.json`. Ignore `node_modules` and `dist`.

## Check your understanding

1. Why are `typescript`, `@types/node`, and `tsx` separate packages?
2. Why does the project run type checking separately from development execution?
3. What is generated in `dist`?
4. Why does the promise callback run before the timer callback?
5. Why can CPU-heavy JavaScript delay unrelated requests?

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before reading the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../02-es-modules-package-boundaries-and-dependency-scripts/README.md).
