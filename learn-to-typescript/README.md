# Learn TypeScript Step by Step

Welcome. This course is for you even if you have never written code before.

You will begin by printing one line of text. You will then learn how programs store information, make decisions, repeat work, and organize data. Once those ideas feel familiar, you will learn how TypeScript checks your code and helps you describe data clearly.

The course eventually reaches advanced TypeScript, but it does not rush. Every module builds on earlier modules. You should not need a concept that has not already been taught.

## What TypeScript is

JavaScript is a programming language used in browsers, servers, desktop tools, and many other places. TypeScript adds a type checker to JavaScript.

A type checker studies your code before it runs. It can find mistakes such as passing a number to a function that expects text. TypeScript cannot prove that a whole program is correct, and it does not check information arriving from a user or a network while the program runs. You will learn both its strengths and its limits.

TypeScript code is turned into JavaScript before it runs. You will see this process in small steps instead of memorizing it all at once.

## How to use this course

Work through the modules in number order. For each module:

1. Read its `README.md` slowly.
2. Type every example yourself. Do not only copy and paste.
3. Pause when the lesson asks you to predict a result.
4. Complete `exercise/exercise.md` without opening the answers.
5. Run your work and compare the result with the requirements.
6. Complete `quiz/quiz.md` without looking ahead.
7. Read both answer files, including their explanations.
8. Change one exercise solution to see what happens.

It is normal to repeat a module. Learning to program takes practice, not speed.

## Two ways to run the examples

### Option 1: Use the TypeScript Playground

The TypeScript Playground runs in a web browser and requires no setup.

1. Open <https://www.typescriptlang.org/play>.
2. Replace the example code with the code from a lesson.
3. Select **Run** to see its output.

This is the simplest choice for the first few modules.

### Option 2: Work on your computer

Install a current Node.js LTS release from <https://nodejs.org>. Node.js lets your computer run JavaScript outside a browser. Its installer also includes `npm`, which installs development tools.

Open a terminal and check the installation:

```text
node --version
npm --version
```

Create a practice project:

```text
mkdir my-typescript-practice
cd my-typescript-practice
npm init -y
npm install --save-dev typescript tsx @types/node
```

Create a file named `index.ts`, then run it with:

```text
npx tsx index.ts
```

In Module 19, you will learn what each project file does and how to configure the TypeScript compiler. Until then, the command above is enough.

## What to do when code does not work

Use this routine:

1. Read the first error message.
2. Find the file and line it mentions.
3. Compare punctuation carefully.
4. Check the spelling and letter case of names.
5. Print the values you are unsure about.
6. Make one small change, then run the code again.

Do not change many unrelated lines at once. A small change makes its effect easier to understand.

## Course map

### Part 1: First steps in programming

1. [Your First TypeScript Program](./01-your-first-typescript-program/README.md)
2. [Values, Variables, and Basic Types](./02-values-variables-and-basic-types/README.md)
3. [Working with Text and Numbers](./03-working-with-text-and-numbers/README.md)
4. [Comparisons and Decisions](./04-comparisons-and-decisions/README.md)
5. [Repeating Work with Loops](./05-repeating-work-with-loops/README.md)
6. [Functions](./06-functions/README.md)
7. [Arrays](./07-arrays/README.md)
8. [Objects](./08-objects/README.md)
9. [Array Methods](./09-array-methods/README.md)
10. [Debugging Small Programs](./10-debugging-small-programs/README.md)

### Part 2: The TypeScript type system

11. [Type Inference and Annotations](./11-type-inference-and-annotations/README.md)
12. [Type Aliases, Unions, and Literal Types](./12-type-aliases-unions-and-literal-types/README.md)
13. [Narrowing](./13-narrowing/README.md)
14. [Object Types and Interfaces](./14-object-types-and-interfaces/README.md)
15. [Optional and Readonly Data](./15-optional-and-readonly-data/README.md)
16. [Tuples and Readonly Collections](./16-tuples-and-readonly-collections/README.md)
17. [Function Types and Callbacks](./17-function-types-and-callbacks/README.md)
18. [Modules and Code Organization](./18-modules-and-code-organization/README.md)
19. [TypeScript Projects and Compiler Settings](./19-typescript-projects-and-compiler-settings/README.md)

### Part 3: Safe and reusable programs

20. [Unknown Data and Runtime Validation](./20-unknown-data-and-runtime-validation/README.md)
21. [Errors and Recovery](./21-errors-and-recovery/README.md)
22. [Generics](./22-generics/README.md)
23. [Keys and Indexed Access Types](./23-keys-and-indexed-access-types/README.md)
24. [Utility and Mapped Types](./24-utility-and-mapped-types/README.md)
25. [Classes and Composition](./25-classes-and-composition/README.md)

### Part 4: Asynchronous and advanced TypeScript

26. [Promises and Asynchronous Work](./26-promises-and-asynchronous-work/README.md)
27. [Async, Await, and Request Boundaries](./27-async-await-and-request-boundaries/README.md)
28. [Discriminated Unions and State](./28-discriminated-unions-and-state/README.md)
29. [Advanced Function APIs](./29-advanced-function-apis/README.md)
30. [Conditional Types and Infer](./30-conditional-types-and-infer/README.md)
31. [Advanced Mapped and Template Literal Types](./31-advanced-mapped-and-template-literal-types/README.md)
32. [Third-Party Types and Declaration Files](./32-third-party-types-and-declaration-files/README.md)
33. [Precise Type Design](./33-precise-type-design/README.md)
34. [Testing and Maintaining TypeScript](./34-testing-and-maintaining-typescript/README.md)

## Suggested pace

For Modules 01 to 10, one module every two or three days is a comfortable pace. Later modules may need a week each. A useful study session is 30 to 60 minutes followed by a break.

You are ready to begin with [Module 01](./01-your-first-typescript-program/README.md).
