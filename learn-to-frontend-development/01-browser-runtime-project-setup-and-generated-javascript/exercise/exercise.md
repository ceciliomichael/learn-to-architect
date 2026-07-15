# Exercise: Create a Browser TypeScript Project

## Goal

Create the shared course project and prove you understand how its HTML, TypeScript, tools, and browser output connect.

## Steps

1. Verify Node.js and npm.
2. Create `browser-course` with the Vite `vanilla-ts` template.
3. Install dependencies and start the development server.
4. Replace `index.html` with a semantic page containing an `h1` and a paragraph with `id="status"`.
5. In `src/main.ts`, safely find that paragraph and change its text to `Ready to learn browser APIs.`
6. Inspect the result in the Elements, Console, Network, and Sources panels.
7. Temporarily remove `id="status"`, observe your intentional error, then restore the identifier.
8. Stop the server, type-check without emitting files, build, and preview the production output.
9. Explain why `node_modules` and `dist` can both be deleted and recreated, while `src` cannot.

## Success check

- The project uses plain TypeScript without a UI framework.
- HTML loads `/src/main.ts` as a module.
- The DOM lookup handles `null` explicitly.
- The development and preview servers both display the expected text.
- Type checking and the production build succeed.
- No generated directory was edited manually.
