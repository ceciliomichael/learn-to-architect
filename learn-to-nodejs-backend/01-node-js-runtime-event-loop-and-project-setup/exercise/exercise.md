# Exercise: Build the TypeScript Node.js Course Project

## Goal

Create the continuing backend project, prove strict type checking works, and collect evidence of event-loop ordering.

## Steps

1. Create `node-api-course` with `npm init`.
2. Install TypeScript, Node.js types, and `tsx` as local development dependencies.
3. Add the package manifest, scripts, and strict `tsconfig.json` from the lesson.
4. Create a typed `RuntimeObservation` object with `label`, `sequence`, and `recordedAt` properties.
5. Log one synchronous observation, one promise observation, and one timer observation.
6. Predict the order before running the program, then record the actual order.
7. Introduce one deliberate type error and confirm `npm run typecheck` rejects it. Repair it.
8. Build the project, inspect `dist`, and run the compiled program.
9. Add `.gitignore` entries for `node_modules`, `dist`, and local environment files.

## Success check

- Dependencies are local and recorded in the lock file.
- Strict type checking passes after the deliberate error is repaired.
- The observed callback order is explained correctly.
- `dist/main.js` contains JavaScript without TypeScript annotations.
- Development execution and compiled execution produce the same ordering.
- No generated files or secrets are prepared for source control.
