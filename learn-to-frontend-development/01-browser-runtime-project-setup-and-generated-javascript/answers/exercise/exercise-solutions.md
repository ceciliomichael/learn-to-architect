# Exercise Solution: Create a Browser TypeScript Project

## Commands

```text
npm create vite@latest browser-course -- --template vanilla-ts
cd browser-course
npm install
npm run dev
```

## index.html

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browser Course</title>
  </head>
  <body>
    <main>
      <h1>Browser Course</h1>
      <p id="status">Waiting...</p>
    </main>
    <script type="module" src="/src/main.ts"></script>
  </body>
</html>
```

## src/main.ts

```ts
const status = document.querySelector<HTMLParagraphElement>("#status");

if (status === null) {
  throw new Error("Expected a paragraph with id status");
}

status.textContent = "Ready to learn browser APIs.";
```

## Final commands

```text
npx tsc --noEmit
npm run build
npm run preview
```

`src` contains authored source and cannot be recreated from build output. `node_modules` can be restored from `package.json` and `package-lock.json` with `npm install`. `dist` can be recreated from the source with `npm run build`.
