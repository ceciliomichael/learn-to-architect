# Exercise Solution: Create and Inspect a Next.js Project

## Commands

```text
node --version
npm --version
npx create-next-app@latest nextjs-course --use-npm
cd nextjs-course
npm run dev
```

Choose TypeScript, ESLint, and App Router. Leave React Compiler, Tailwind CSS, the `src` directory, and custom aliases off for this course.

## app/page.tsx

```tsx
export default function HomePage() {
  return (
    <main>
      <h1>My Next.js Learning Project</h1>
      <p>I am learning how routes, server rendering, and typed data work together.</p>
    </main>
  );
}
```

## app/layout.tsx

Keep the generated imports and update the metadata values:

```tsx
import type { Metadata } from "next";
import "./globals.css";

export const metadata: Metadata = {
  title: "My Next.js Learning Project",
  description: "A practice project for the Next.js course",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Final checks

Stop the development server with `Ctrl+C`, then run:

```text
npm run lint
npm run build
```

The solution is complete when both commands succeed and the edited page appears after restarting `npm run dev`.

`package.json` declares packages and scripts. `package-lock.json` locks the installed dependency versions. `app/page.tsx` owns the `/` page. `app/layout.tsx` owns shared document structure and metadata. `public` stores directly served assets. `.next` is generated build output. `node_modules` stores installed packages.
