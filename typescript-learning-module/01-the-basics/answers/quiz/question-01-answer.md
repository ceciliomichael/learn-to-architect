# Question 01 Answer

**Correct answer: B**

Type annotations like `: string`, `: number`, and `: number[]` are completely removed during compilation. They do not appear anywhere in the compiled JavaScript output.

TypeScript is purely a development-time tool. It exists to help you catch mistakes while writing code. Once the compiler finishes translating your `.ts` file into a `.js` file, all type information is stripped out. The resulting JavaScript is identical to what you would have written without TypeScript  -  there are no `typeof` checks inserted, no comments, and no runtime type enforcement.

This is called **type erasure**. It is why TypeScript adds zero overhead to your running application.
