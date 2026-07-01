# Module 08 Quiz Answers

Detailed explanations for Module 08 quiz.

---

### Answer 1:
TypeScript throws a compiler error (`Type 'null' is not assignable to type 'string'`).  
This prevents common runtime crashes (`Cannot read properties of null/undefined`) by forcing developers to explicitly handle missing values or type variables as nullable (`string | null`).

---

### Answer 2:
Raw JavaScript libraries lack type definitions. TypeScript displays an error indicating it cannot find declaration files for `'lodash'`.  
Installing `@types/lodash` downloads community-maintained declaration (`.d.ts`) files from DefinitelyTyped, supplying full IntelliSense and type checking for the library.

---

### Answer 3:
No! Declaration files (`.d.ts`) contain **only** type signatures and interfaces. Attempting to include executable statements or implementation bodies results in compile errors because declaration files are never emitted to JavaScript.

---

### Answer 4:
Any file lacking top-level `import` or `export` statements is treated by TypeScript as a global script, merging all top-level variables into the shared global scope. Presence of any top-level `import` or `export` statement isolates the file into its own module scope.
