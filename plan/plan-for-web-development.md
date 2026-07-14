# Plan for the Web Development Learning Path

## Purpose

Create one clear beginner-to-advanced path without turning a language course into a collection of unrelated web tools. Shared browser knowledge is taught once. Framework courses teach only their own model and responsibilities.

## Path architecture

1. Web Foundations teaches how pages work, semantic HTML, CSS, responsive design, forms, accessibility, and browser developer tools without requiring programming.
2. Learn TypeScript teaches programming and the JavaScript runtime model from the beginning.
3. Frontend Development with TypeScript applies TypeScript to the DOM, events, forms, HTTP, storage, security, testing, performance, and deployment without a UI framework.
4. Learners choose React or Vue. Neither framework is a prerequisite for the other.
5. Next.js follows React because it adds routing, server rendering, server execution, caching, data mutation, and deployment behavior to React applications.
6. Nuxt, Node.js web servers, and other specializations can be planned later. They are not placeholders in the required path.

## Required module structure

Every course module contains `README.md`, `exercise/exercise.md`, `quiz/quiz.md`, `answers/exercise/exercise-solutions.md`, and `answers/quiz/quiz-answers.md`.

## Course sizes derived from lesson boundaries

- [x] Web Foundations: 24 modules
- [x] Frontend Development with TypeScript: 26 modules
- [x] React: 24 modules
- [x] Next.js: 26 modules
- [x] Vue: 24 modules

The counts are not shared targets. Web Foundations needs separate HTML, CSS, responsive, form, and accessibility boundaries. Frontend Development with TypeScript needs separate DOM, event, network, storage, testing, security, and performance boundaries. React and Vue have different state and composition models. Next.js has additional server, cache, routing, and deployment boundaries.

## Global rules

1. No framework before HTML, CSS, JavaScript behavior, DOM events, HTTP, and accessibility.
2. No Next.js before React state, effects, composition, and testing.
3. No framework course reteaches basic HTML, CSS, or TypeScript as if those prerequisites do not exist.
4. Accessibility, security, runtime validation, responsive behavior, testing, and performance are normal development concerns, not late optional decorations.
5. Examples use current stable APIs and label experimental or platform-limited behavior.
6. Installed packages appear only after package manifests, lock files, scripts, and dependency trust are explained.
7. Every exercise has observable completion criteria and a complete solution.
8. There is no miscellaneous module and no final assessment.

## Verification

- [x] Create the shared `learning-paths/web-development.md` entry point
- [x] Create all five courses and required module files
- [x] Check official MDN, React, Next.js, and Vue prerequisites
- [x] Verify HTML, CSS, TypeScript, and framework examples with appropriate tools
- [x] Check prerequisite vocabulary across course boundaries
- [x] Check relative links, code fences, ASCII-only text, quiz counts, and unfinished markers
- [x] Update the repository course catalog
- [x] Mark completed plan items
