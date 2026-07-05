# Question 01: strictNullChecks

What does `strictNullChecks` do and what problem does it solve?

```typescript
// With strictNullChecks: false (the dangerous default in old TypeScript)
let user: { name: string } = null; // No error! Very risky.
console.log(user.name);            // Runtime crash: Cannot read properties of null.

// With strictNullChecks: true
let user2: { name: string } = null; // ERROR at compile time.
```

1. What does enabling `strictNullChecks` force TypeScript to do?
2. How would you correctly type `user` if it should be allowed to be either a user object OR `null`?
3. What is the connection between `strictNullChecks` and the `?` optional chaining operator?

## ANSWER HERE

> **What strictNullChecks forces TypeScript to do:**

> **Correct type for a nullable user:**

> **Connection to optional chaining:**
