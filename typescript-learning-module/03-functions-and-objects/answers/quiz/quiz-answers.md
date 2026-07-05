# Module 03 Quiz Answers: Master Reference

Welcome to the production-grade answer guide for **Module 03: Functions and Signatures**. This document provides an exhaustive architectural breakdown, complete compiler mechanics, and deep technical trade-offs for all five conceptual quiz questions.

---

## 1. Summary of Quiz Answers

1. **[Question 01: Callbacks and Contextual Typing](./question-01-answer.md)**: Explains what a callback function is, how TypeScript performs Contextual Typing on `(num) => num * 2` inside `.map()`, and why calling `num.toUpperCase()` is instantly blocked by the type checker before execution.
2. **[Question 02: void Callbacks](./question-02-answer.md)**: Details why passing `() => true` into a parameter typed as `() => void` does not cause a compiler error. Explains the intentional design of TypeScript to maintain compatibility with real-world JavaScript patterns like `array.push()` inside `.forEach()`.
3. **[Question 03: Rest Parameter Type](./question-03-answer.md)**: Confirms that **Option B (`...words: string[]`)** is the only valid syntax. Analyzes why rest parameters must be typed as arrays and how the JavaScript runtime gathers variadic arguments into an Array instance.
4. **[Question 04: for vs for...of](./question-04-answer.md)**: Compares classic index loops against modern `for...of` loops. Explains when numeric index access (`i`) is mandatory versus when value-only iteration (`for...of`) provides superior safety, readability, and async/await control as taught in Section 7 of the README.
5. **[Question 05: Function Overloading and Hidden Signatures](./question-05-answer.md)**: Explains why TypeScript hides the implementation signature from external callers, what architectural problems hiding it solves, and why attempting to pass unsupported types like booleans is blocked at compile time.

---

## 2. Deep Dive Architectural Guides

For symbol-by-symbol breakdowns, complete code demonstrations, and enterprise engineering best practices for each conceptual topic, please consult the individual answer documents in this directory:
* [Question 01 Answer: Callbacks and Contextual Typing](./question-01-answer.md)
* [Question 02 Answer: void Callbacks](./question-02-answer.md)
* [Question 03 Answer: Rest Parameter Type](./question-03-answer.md)
* [Question 04 Answer: for vs for...of](./question-04-answer.md)
* [Question 05 Answer: Function Overloading and Hidden Signatures](./question-05-answer.md)
