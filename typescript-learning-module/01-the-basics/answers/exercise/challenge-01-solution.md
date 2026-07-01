# Challenge 01: Solution - Fix the Broken Code

```typescript
// ERROR 1: 'username' was declared with 'const', meaning it cannot be reassigned.
// Fix: Change 'const' to 'let' if the value needs to change.
let username: string = "code_ninja_99";
username = "senior_dev_2026"; // Now valid.

// ERROR 2: The value "25" is a string (wrapped in quotes), but the type is number.
// Fix: Remove the quotes to make it an actual number.
let age: number = 25;

// ERROR 3: The value 1 is a number, but the type is boolean.
// Fix: Use 'true' or 'false'.
let isLoggedIn: boolean = true;

// ERROR 4: skills is inferred as string[], but 404 is a number.
// TypeScript will not allow pushing a number into a string array.
// Fix: Push a string instead.
let skills = ["HTML", "CSS", "JS"];
skills.push("TypeScript"); // Valid. Strings only in a string array.
```
