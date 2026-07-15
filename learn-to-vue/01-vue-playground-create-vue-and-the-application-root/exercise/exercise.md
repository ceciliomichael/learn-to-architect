# Exercise: Create and Trace a Vue Application

## Goal

Create a minimal TypeScript Vue project and explain how the browser reaches the root component.

## Steps

1. Verify Node.js and npm.
2. Run `npm create vue@latest` and use the choices from the lesson.
3. Install packages and start the development server.
4. Add the guarded mount code to `src/main.ts`.
5. Replace `src/App.vue` with a TypeScript script and a semantic template containing your own project name.
6. Change the document title in `index.html`.
7. Explain the path from `index.html` to `src/main.ts` to `src/App.vue`.
8. Stop the server and run linting, type checking, and the production build.

## Deliberate failure

Temporarily change `id="app"` in `index.html`. Reload and read the intentional error. Restore the identifier and confirm the application mounts again.

## Success check

- TypeScript and ESLint are enabled.
- Router, Pinia, and testing were not added before their lessons.
- The missing-root failure is clear.
- The first component uses `<script setup lang="ts">`.
- Linting, type checking, and the production build succeed.
