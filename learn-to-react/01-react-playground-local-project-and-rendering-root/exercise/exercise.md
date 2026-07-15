# Exercise: Create and Trace a React Application

## Goal

Create the local React project and explain the complete path from `index.html` to the visible component.

## Steps

1. Verify Node.js and npm in a terminal.
2. Create `react-course` with the Vite `react-ts` template.
3. Install its dependencies and start the development server.
4. Replace `src/main.tsx` with the guarded rendering-root example from the lesson.
5. Replace `src/App.tsx` with a `main`, an `h1`, and two paragraphs about your learning goal.
6. Change the document title in `index.html`.
7. In your own words, trace `index.html` to `src/main.tsx`, then to `src/App.tsx`.
8. Stop the server and run the linter and production build.

## Deliberate failure

Temporarily change `id="root"` in `index.html` to `id="application"`. Reload the page and read the error from the null check. Restore `id="root"` and confirm the page recovers.

## Success check

- The project was created with the TypeScript template.
- The application has one rendering root.
- A missing root produces the intentional clear error.
- Your component uses semantic HTML.
- `npm run lint` and `npm run build` both succeed.
