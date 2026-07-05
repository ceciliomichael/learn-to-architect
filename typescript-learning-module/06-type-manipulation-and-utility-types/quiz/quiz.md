# Welcome to Conceptual Quiz: Type Manipulation and Utility Types

Welcome to the conceptual quiz for **Type Manipulation and Utility Types**! True engineering mastery requires understanding *why* code works under the hood, not just memorizing syntax.

These questions are designed to test your mental models, compiler mechanics, and readiness for real-world architectural reviews and technical interviews.

## Topics We Are Testing Today

1. **[Question 01: Object Shape Transformations and Memory Models](./question-01.md)**: Evaluate how `Partial`, `Required`, and `Readonly` alter interface rules at compile time vs runtime.
2. **[Question 02: Property Plucking and Record Dictionaries](./question-02.md)**: Analyze the architectural trade-offs between `Pick` and `Omit`, and evaluate exhaustiveness checking in `Record`.
3. **[Question 03: Union Transformations in ORM Queries](./question-03.md)**: Examine how `Exclude`, `Extract`, and `NonNullable` filter union types and sanitize database lookups.
4. **[Question 04: Function Inspection and the typeof Context](./question-04.md)**: Compare runtime vs compile-time `typeof`, and reverse-engineer function signatures using `ReturnType` and `Parameters`.
5. **[Question 05: Advanced Type Engines](./question-05.md)**: Explain Mapped Type assembly loops (`[P in keyof T]`), Conditional Types with `infer`, and Template Literal string patterns.

## How to Take This Quiz

1. Open each question file sequentially.
2. Think through the compiler mechanics before peeking at any notes.
3. Write your architectural reasoning clearly inside the **ANSWER HERE** block.
4. Avoid short 1-line answers: provide exhaustive, senior-level explanations.

## Check Your Answers

When you are done, verify your answers against our thorough architectural explanations inside **[../answers/quiz/](../answers/quiz/)**. Let us see how many you ace!
