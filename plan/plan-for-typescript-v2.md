# Plan for the TypeScript Learning Program V2

## Purpose

This document is the source of truth for building the second version of the TypeScript learning program. It records the course goals, the teaching rules, the module order, the file structure, and the completion checks.

The program is for a person who has never programmed before. It must also grow far enough to teach advanced TypeScript in a careful and useful way.

## Current course findings

The existing TypeScript course contains useful information, but its structure makes learning harder than it needs to be.

The main problems found during the review are:

1. The modules are too broad. The first module alone teaches compiler behavior, variables, primitive types, arrays, `any`, `unknown`, template strings, and logging.
2. Basic programming ideas arrive late. Loops appear in the functions module even though earlier exercises already require array operations and runtime checks.
3. Some quizzes reach beyond their lessons. Early quiz answers discuss classes, declaration merging, conditional types, branding, modules, browser APIs, and package augmentation.
4. The writing often assumes professional software knowledge. Terms such as architecture, infrastructure, webhooks, observability, domain models, and state machines appear before the learner has enough context.
5. Some recommendations are presented as universal rules when they are choices. Examples include always writing return type annotations, never using `any`, always preferring one object type syntax, and treating a fixed file length as an architectural rule.
6. Very long explanations hide the main idea. Large analogies and symbol-by-symbol breakdowns are repeated even when a short direct explanation would be clearer.
7. Practice sometimes measures unfamiliar vocabulary instead of the idea taught in the lesson.
8. The course moves from absolute beginner language to senior-level language too quickly.

V2 will keep the useful goal of strong type safety while replacing the sequence and teaching method.

## Course promise

A learner who follows the modules in order should be able to:

- understand what each line of a small program does
- write and run TypeScript without copying unexplained commands
- solve problems with values, decisions, loops, functions, arrays, and objects
- read TypeScript errors and use them as useful feedback
- model data with unions, object types, interfaces, and generics
- handle missing, uncertain, failed, and asynchronous data safely
- organize code into modules and configure a strict TypeScript project
- understand and use advanced type tools when they genuinely improve code
- read unfamiliar TypeScript code and decide whether its types are helpful
- design clear typed APIs without trying to make the type system do unnecessary work

## Non-negotiable writing rules

Every course file must follow these rules:

1. Use no emoji.
2. Use no em dash character.
3. Prefer short, direct sentences.
4. Introduce one main idea at a time.
5. Define a new word when it first appears.
6. Do not use an analogy unless it makes the idea easier to understand.
7. Do not describe ordinary code with inflated words such as enterprise, production-grade, or architectural.
8. Do not promise that TypeScript prevents every bug. Explain what it checks and what it cannot check.
9. Do not present style preferences as language rules.
10. Explain the runtime result separately from the type-checking result when the difference matters.
11. Use examples with familiar subjects such as names, prices, tasks, books, temperatures, and simple messages.
12. Keep code examples small enough to understand without scrolling through unrelated details.
13. Never use syntax that has not been taught, unless the line is clearly marked as a preview and is not required for practice.
14. Do not use `any` in course implementations. Explain its real purpose and tradeoffs without pretending it never has a valid use.
15. Prefer inference for obvious local values. Add annotations where they teach, document, or protect a boundary.
16. Use current ECMAScript module syntax for new code.
17. Use `strict` TypeScript settings for the course project.
18. Use inclusive, calm language. Errors are information, not failure.

## Learning pattern for every module

Each module will keep a familiar folder layout with five learning files:

- `README.md`: the lesson
- `exercise/exercise.md`: guided and independent work
- `quiz/quiz.md`: a lesson-aligned understanding check
- `answers/exercise/exercise-solutions.md`: complete exercise answers with reasoning
- `answers/quiz/quiz-answers.md`: complete quiz answers with reasoning

Every lesson will follow this order:

1. `Before you start`: lists only the required earlier ideas.
2. `What you will learn`: two to five concrete outcomes.
3. `Why this matters`: a short, ordinary reason to learn the topic.
4. Lesson sections: explain, show a small example, and let the learner predict a result.
5. `Common mistakes`: likely errors and how to read them.
6. `Check your understanding`: short questions answerable from the lesson.
7. `Practice`: link to the module practice.
8. `Next step`: one short description of what follows.

Every exercise file will contain:

1. a warm-up that changes a working example
2. a guided exercise with numbered steps
3. an independent exercise with observable requirements
4. a debugging task when it suits the topic
5. a completion checklist
6. a link to the exercise solutions

Every quiz file will contain:

1. questions that only use the current and earlier lessons
2. a mix of prediction, explanation, comparison, and small code-reading questions
3. no interview trivia
4. no concepts from later modules
5. a link to the quiz answers

Every answer file will contain:

1. a complete solution for every task
2. a plain explanation of the important choices
3. expected output when code prints a result
4. one valid alternative when it teaches a useful distinction
5. no unrelated advanced syntax

## Course structure

The course will live in `typescript-learning-module-v2/`. The current `typescript-learning-module/` will remain unchanged for comparison and safe migration.

The V2 root will contain:

- `README.md`: course introduction, setup, study routine, and module map
- numbered module folders such as `01-programming-and-typescript`
- no miscellaneous folder
- no final assessment folder

## Curriculum roadmap

### Part 1: First steps in programming

- [x] **Module 01: Your First TypeScript Program**
  - Prerequisites: none
  - Teaches: what code is, source files, terminal basics, installing course tools, running a file, `console.log`, comments, and reading output
  - Outcome: the learner can create and run a small `.ts` file

- [x] **Module 02: Values, Variables, and Basic Types**
  - Prerequisites: Module 01
  - Teaches: values, `const`, `let`, assignment, names, `string`, `number`, `boolean`, and `typeof`
  - Outcome: the learner can store and update simple information

- [x] **Module 03: Working with Text and Numbers**
  - Prerequisites: Modules 01 to 02
  - Teaches: string methods, template strings, arithmetic, order of operations, rounding, and `NaN`
  - Outcome: the learner can calculate values and build readable messages

- [x] **Module 04: Comparisons and Decisions**
  - Prerequisites: Modules 01 to 03
  - Teaches: comparison operators, strict equality, `if`, `else if`, `else`, logical operators, and truth tables
  - Outcome: the learner can make a program choose between actions

- [x] **Module 05: Repeating Work with Loops**
  - Prerequisites: Modules 01 to 04
  - Teaches: repeated steps, `for`, `while`, counters, `break`, and avoiding infinite loops
  - Outcome: the learner can repeat a known action safely

- [x] **Module 06: Functions**
  - Prerequisites: Modules 01 to 05
  - Teaches: function declarations, parameters, arguments, return values, local scope, and small single-purpose functions
  - Outcome: the learner can name and reuse a group of steps

- [x] **Module 07: Arrays**
  - Prerequisites: Modules 01 to 06
  - Teaches: ordered collections, indexes, length, reading and changing items, `push`, `pop`, and `for...of`
  - Outcome: the learner can store and process a list

- [x] **Module 08: Objects**
  - Prerequisites: Modules 01 to 07
  - Teaches: properties, object literals, dot access, bracket access for known strings, updating data, and objects passed to functions
  - Outcome: the learner can group related values

- [x] **Module 09: Array Methods**
  - Prerequisites: Modules 01 to 08
  - Teaches: callbacks through practical use, `forEach`, `map`, `filter`, `find`, `some`, and `every`
  - Outcome: the learner can transform and search a list without manual bookkeeping

- [x] **Module 10: Debugging Small Programs**
  - Prerequisites: Modules 01 to 09
  - Teaches: syntax, type, and runtime errors, reading messages, tracing values, small-program decomposition, and a repeatable debugging routine
  - Outcome: the learner can investigate a broken beginner program methodically

### Part 2: The TypeScript type system

- [x] **Module 11: Type Inference and Annotations**
  - Prerequisites: Modules 01 to 10
  - Teaches: inferred types, annotations, assignment checking, function parameter annotations, return inference, and type erasure
  - Outcome: the learner understands what TypeScript checks and when an annotation helps

- [x] **Module 12: Type Aliases, Unions, and Literal Types**
  - Prerequisites: Modules 01 to 11
  - Teaches: naming a type, `|`, literal choices, `null`, `undefined`, and modeling a small set of valid values
  - Outcome: the learner can describe values with more precision than a primitive type

- [x] **Module 13: Narrowing**
  - Prerequisites: Modules 01 to 12
  - Teaches: why union members need checks, `typeof`, equality checks, truthiness with care, `Array.isArray`, and control-flow narrowing
  - Outcome: the learner can safely use a value that has more than one possible type

- [x] **Module 14: Object Types and Interfaces**
  - Prerequisites: Modules 01 to 13
  - Teaches: inline object types, reusable object aliases, interfaces, structural typing, and choosing clear property types
  - Outcome: the learner can describe and use structured data

- [x] **Module 15: Optional and Readonly Data**
  - Prerequisites: Modules 01 to 14
  - Teaches: optional properties, checking `undefined`, optional chaining, nullish coalescing, `readonly`, excess property checks, and index signatures
  - Outcome: the learner can model missing and protected data without unsafe assumptions

- [x] **Module 16: Tuples and Readonly Collections**
  - Prerequisites: Modules 01 to 15
  - Teaches: fixed positions, labeled tuples, destructuring, readonly arrays, and when an object is clearer than a tuple
  - Outcome: the learner can choose an appropriate collection shape

- [x] **Module 17: Function Types and Callbacks**
  - Prerequisites: Modules 01 to 16
  - Teaches: function type expressions, callback parameters, optional and default parameters, arrow functions, and contextual typing
  - Outcome: the learner can describe a function passed into another function

- [x] **Module 18: Modules and Code Organization**
  - Prerequisites: Modules 01 to 17
  - Teaches: file scope, named exports, named imports, `import type`, avoiding accidental globals, and small module boundaries
  - Outcome: the learner can split a program across files and follow its data flow

- [x] **Module 19: TypeScript Projects and Compiler Settings**
  - Prerequisites: Modules 01 to 18
  - Teaches: `package.json`, local dependencies, `tsconfig.json`, `tsc`, `noEmit`, output, `strict`, target, module settings, and selected strictness options
  - Outcome: the learner can create, check, and build a small TypeScript project

### Part 3: Safe and reusable programs

- [x] **Module 20: Unknown Data and Runtime Validation**
  - Prerequisites: Modules 01 to 19
  - Teaches: static types versus runtime data, `unknown`, safe checks, object guards, validation functions, JSON parsing boundaries, and the limited role of assertions
  - Outcome: the learner does not trust external data merely because a type was written

- [x] **Module 21: Errors and Recovery**
  - Prerequisites: Modules 01 to 20
  - Teaches: throwing built-in errors, `try`, `catch`, `finally`, caught values as `unknown`, and a simple result union. Custom error classes are deferred until class syntax has been taught.
  - Outcome: the learner can represent expected failure and recover from unexpected failure

- [x] **Module 22: Generics**
  - Prerequisites: Modules 01 to 21
  - Teaches: preserving a relationship between input and output types, generic functions, inference, generic aliases and interfaces, and useful constraints
  - Outcome: the learner can write reusable code without losing type information

- [x] **Module 23: Keys and Indexed Access Types**
  - Prerequisites: Modules 01 to 22
  - Teaches: `keyof`, indexed access types, `typeof` in a type position, generic property access, and safe lookup helpers
  - Outcome: the learner can derive a type from an existing object shape

- [x] **Module 24: Utility and Mapped Types**
  - Prerequisites: Modules 01 to 23
  - Teaches: `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`, mapped type syntax, and when explicit types are easier to read
  - Outcome: the learner can transform object types without duplicating their properties

- [x] **Module 25: Classes and Composition**
  - Prerequisites: Modules 01 to 24
  - Teaches: class instances, constructors, fields, methods, access modifiers, `implements`, inheritance, and choosing composition over inheritance when it is simpler
  - Outcome: the learner understands class-based code and can decide when a class is useful

### Part 4: Asynchronous and advanced TypeScript

- [x] **Module 26: Promises and Asynchronous Work**
  - Prerequisites: Modules 01 to 25
  - Teaches: delayed results, Promise states, `Promise<T>`, `.then`, `.catch`, timers, and why asynchronous work does not return an immediate value
  - Outcome: the learner can read and type a Promise-based function

- [x] **Module 27: Async, Await, and Request Boundaries**
  - Prerequisites: Modules 01 to 26
  - Teaches: `async`, `await`, rejected Promises, response checks, validating fetched data, sequential versus parallel work, `Promise.all`, and `Promise.allSettled`
  - Outcome: the learner can write a safe asynchronous workflow

- [x] **Module 28: Discriminated Unions and State**
  - Prerequisites: Modules 01 to 27
  - Teaches: common discriminant properties, impossible state prevention, exhaustive `switch`, `never`, and state transitions
  - Outcome: the learner can make invalid combinations difficult to represent

- [x] **Module 29: Advanced Function APIs**
  - Prerequisites: Modules 01 to 28
  - Teaches: rest parameters, spread arguments, overload signatures, `this` parameters, generic callbacks, and when a union is simpler than an overload
  - Outcome: the learner can understand and design flexible function signatures

- [x] **Module 30: Conditional Types and Infer**
  - Prerequisites: Modules 01 to 29
  - Teaches: conditional type syntax, distribution over unions, disabling distribution, `infer`, and small type helpers
  - Outcome: the learner can read and write focused conditional types without hiding ordinary code behind type tricks

- [x] **Module 31: Advanced Mapped and Template Literal Types**
  - Prerequisites: Modules 01 to 30
  - Teaches: mapping modifiers, key remapping with `as`, template literal types, string manipulation types, and generating event names from object keys
  - Outcome: the learner can derive repetitive API names from a trusted source type

- [x] **Module 32: Third-Party Types and Declaration Files**
  - Prerequisites: Modules 01 to 31
  - Teaches: bundled types, `@types`, reading library declarations, `.d.ts` files, ambient declarations, module augmentation, and why declarations must match runtime behavior
  - Outcome: the learner can diagnose missing library types and write a small honest declaration

- [x] **Module 33: Precise Type Design**
  - Prerequisites: Modules 01 to 32
  - Teaches: `as const`, `satisfies`, safe assertions, branded values at boundaries, variance as a practical compatibility issue, and balancing precision with readability
  - Outcome: the learner can make a public type precise without making it difficult to use

- [x] **Module 34: Testing and Maintaining TypeScript**
  - Prerequisites: Modules 01 to 33
  - Teaches: runtime tests, compile-time checks, expected errors with `@ts-expect-error`, refactoring with compiler feedback, dependency upgrades, and keeping type tests readable
  - Outcome: the learner can maintain confidence while changing a typed program

## Dependency rules

The following rules protect the learning sequence:

- Conditions must be taught before narrowing.
- Loops and basic functions must be taught before array callbacks.
- Objects must be taught before object types and interfaces.
- Union types must be taught before narrowing and result types.
- Functions and arrays must be taught before generics.
- Modules must be taught before project configuration and declaration files.
- `unknown` must be taught before catch handling and external request validation.
- Generics must be taught before `keyof`, mapped types, conditional types, and `infer`.
- Promises must be taught before `async` and `await`.
- Discriminated unions must be taught before exhaustive checks with `never`.
- Mapped types must be taught before key remapping.
- No exercise may require a later module's syntax.

## Accuracy rules

Technical statements will be checked against current TypeScript behavior and the official TypeScript documentation.

Important distinctions that must remain accurate:

- TypeScript checks code before runtime, but it does not validate network, file, or user data by itself.
- Type annotations are removed from emitted JavaScript, but TypeScript syntax can still affect emitted code depending on the feature and compiler settings.
- `readonly` prevents writes through a particular type view. It does not deeply freeze a runtime object.
- `private` in TypeScript and JavaScript `#private` fields do not have identical runtime behavior.
- An optional property and a required property whose value can be `undefined` are different shapes.
- `any` disables useful checking for operations that flow through it. It is not automatically a runtime error.
- `unknown` requires narrowing before most operations.
- Type assertions do not convert or validate values at runtime.
- Arrays can return `undefined` for a missing index. Compiler options can make that risk visible in the type.
- A Promise represents a future completion or failure. `async` does not make CPU-heavy work run on another thread.
- Interfaces and type aliases overlap heavily. The course will teach their actual differences without declaring a universal winner.
- Advanced type transformations are tools, not a measure of programming skill.

## Estimated learning time

The course is designed for steady practice rather than fast reading.

- Modules 01 to 10: about 2 to 4 hours each
- Modules 11 to 19: about 3 to 5 hours each
- Modules 20 to 25: about 4 to 6 hours each
- Modules 26 to 34: about 5 to 8 hours each

The full path is expected to take roughly 140 to 200 focused hours. A learner may need more time, and that is normal.

## Implementation checklist

- [x] Review the current course structure and representative content
- [x] Identify sequencing, tone, and accuracy problems
- [x] Define the V2 teaching standard
- [x] Define the complete beginner-to-advanced roadmap
- [x] Create the V2 root guide
- [x] Create Modules 01 to 10
- [x] Audit Modules 01 to 10 for prerequisites
- [x] Create Modules 11 to 19
- [x] Audit Modules 11 to 19 for prerequisites
- [x] Create Modules 20 to 25
- [x] Audit Modules 20 to 25 for prerequisites
- [x] Create Modules 26 to 34
- [x] Audit Modules 26 to 34 for prerequisites
- [x] Scan every V2 file for emoji and em dash characters
- [x] Check every internal Markdown link
- [x] Check representative TypeScript examples intended to compile with the current strict compiler
- [x] Review language for unexplained technical terms
- [x] Mark the curriculum checklist complete

## Definition of done

V2 is complete when:

1. Every planned module has a lesson, exercise file, quiz file, exercise solution file, and quiz answer file.
2. Every module states its prerequisites and only uses those ideas.
3. Every practice task has a complete explained solution.
4. The course contains no miscellaneous or final assessment section.
5. The V2 files contain no emoji and no em dash character.
6. Internal links resolve to existing files.
7. Compilable examples pass a strict TypeScript check or are clearly labeled as intentional errors.
8. The root guide gives a beginner a clear first action.
9. The language remains friendly, direct, and honest from Module 01 through Module 34.
10. The existing course remains intact.
