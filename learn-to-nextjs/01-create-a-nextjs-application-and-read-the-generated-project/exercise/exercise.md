# Exercise: Create and Inspect a Next.js Project

## Goal

Create the local project yourself, prove that it runs, and explain the files you will use throughout the course.

## Steps

1. Check `node --version` and `npm --version` in a new terminal.
2. Create `nextjs-course` with `create-next-app` and the exact choices from the lesson.
3. Start the development server and open `http://localhost:3000`.
4. Replace `app/page.tsx` with a page containing one `main`, one `h1`, and a paragraph describing what you want to learn.
5. Change the page title and description in the metadata exported from `app/layout.tsx`.
6. In your own words, describe `package.json`, `package-lock.json`, `app/page.tsx`, `app/layout.tsx`, `public`, `.next`, and `node_modules`.
7. Stop the server, run the linter, and create a production build.
8. Start the development server once more and confirm your edited page still works.

## Success check

- The project uses TypeScript and the App Router.
- `npm run dev`, `npm run lint`, and `npm run build` finish successfully.
- The browser shows your content at `/`.
- The document tab shows your title.
- You can identify which folders are authored source and which are generated.
- You did not edit or commit `node_modules` or `.next`.
