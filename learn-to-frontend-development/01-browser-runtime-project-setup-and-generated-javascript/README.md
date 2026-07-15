# Module 01: Browser Runtime, Project Setup, and Generated JavaScript

## Before you start

Complete Web Foundations and Learn TypeScript first. You should be able to create an HTML document, use a terminal, write TypeScript functions, and read compiler errors.

This course uses Node.js 24 LTS and npm to run development tools. Check your installation in a new terminal:

```text
node --version
npm --version
```

The Node.js result should start with `v24.`. Node.js runs the development tools. The browser still runs the application itself.

## What you will learn

By the end of this module, you will be able to:

- create a strict browser TypeScript project
- explain why a browser cannot execute TypeScript syntax directly
- connect `index.html` to a TypeScript entry file
- distinguish source files, installed packages, and generated output
- start the development server and create a production build

## 1. Create the browser project

Move to a folder used for disposable practice. Run:

```text
npm create vite@latest browser-course -- --template vanilla-ts
cd browser-course
npm install
npm run dev
```

Vite is the development and build tool. `vanilla-ts` means plain browser TypeScript without React, Vue, or another UI framework. The extra `--` passes the template option through npm.

Open the local address printed in the terminal, commonly `http://localhost:5173`. Press `Ctrl+C` when you want to stop the server.

## 2. Read the project structure

The generated project contains files similar to:

```text
browser-course/
  public/
  src/
    counter.ts
    main.ts
    style.css
    typescript.svg
  index.html
  package-lock.json
  package.json
  tsconfig.json
```

- `index.html` is the browser entry document.
- `src/main.ts` is the TypeScript entry module.
- `src/style.css` contains the starting styles.
- `public` stores files copied and served without importing them.
- `package.json` records development dependencies and scripts.
- `package-lock.json` records the exact installed dependency tree.
- `tsconfig.json` controls TypeScript checking.
- `node_modules` contains installed packages. Do not edit or commit it.
- `dist` appears after a production build. It is generated and should not be edited.

Delete the generated demo-specific files and replace their content only after you can explain their roles.

## 3. Connect HTML and TypeScript

Replace `index.html` with:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browser TypeScript Course</title>
  </head>
  <body>
    <main>
      <h1>Browser TypeScript Course</h1>
      <p id="output">Waiting for TypeScript...</p>
    </main>
    <script type="module" src="/src/main.ts"></script>
  </body>
</html>
```

The script is a module, so imports work and names do not automatically become globals. During development, Vite receives the request for `/src/main.ts`, removes TypeScript-only syntax, and sends JavaScript the browser can execute.

## 4. Write and inspect the entry module

Replace `src/main.ts` with:

```ts
const message: string = "Browser TypeScript is running.";
const output = document.querySelector<HTMLParagraphElement>("#output");

if (output === null) {
  throw new Error("Expected a paragraph with id output");
}

output.textContent = message;
```

`querySelector` reads runtime HTML, so it can return `null`. The generic type tells TypeScript which kind of element is expected, but it does not create that element. The null check supplies the missing runtime evidence.

Open browser developer tools:

1. Use Elements to find the paragraph and inspect its changed text.
2. Use Console to confirm there are no unexplained errors.
3. Use Network to find `main.ts` during development.
4. Use Sources to compare the authored TypeScript with what the browser executes.

## 5. Type checking and building are different jobs

Stop the server and run:

```text
npx tsc --noEmit
npm run build
```

`tsc --noEmit` checks types without writing JavaScript. `npm run build` creates deployment files in `dist`. Vite performs transformation and bundling, while TypeScript reports type errors.

Preview the production result:

```text
npm run preview
```

Open the address printed by the preview server. This serves `dist`; it is not the same as the development server.

## 6. Understand package installation

`package.json` declares the tools the project needs. `npm install` resolves those declarations and creates `node_modules`. The lock file lets another learner install the same dependency graph.

Do not copy `node_modules` between machines and do not import packages before installing and recording them. Later modules add packages only when their responsibility is taught.

## Common mistakes

### Opening `index.html` with `file://`

Use the development server. Module paths and production behavior are better represented over HTTP.

### Assuming a generic type validates HTML

`querySelector<HTMLParagraphElement>` helps TypeScript after the lookup. It does not prove that the element exists or has the expected runtime origin.

### Editing `dist`

Change source files and rebuild. Generated files will be replaced on the next build.

### Confusing Node.js with the browser

Node.js runs Vite and TypeScript tools. Browser APIs such as `document` run in the browser page.

## Check your understanding

1. Why does this course use the `vanilla-ts` template?
2. What does the module script in `index.html` load?
3. Why is a null check still required after giving `querySelector` a generic type?
4. What is the difference between `node_modules` and `dist`?
5. What different evidence comes from `tsc --noEmit`, `npm run build`, and browser developer tools?

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../02-the-dom-tree-and-safe-element-queries/README.md).
