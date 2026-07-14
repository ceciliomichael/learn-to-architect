# Module 14 Quiz

## Question 1

When is a short inline object type a reasonable choice?

## Question 2

Can both an interface and a type alias describe `{ name: string; age: number }`?

## Question 3

Why does this call work?

```typescript
interface Named {
  name: string;
}

const user = { name: "Ana", age: 24 };
printName(user);
```

Assume `printName` accepts `Named`.

## Question 4

Which form can directly name `"open" | "closed"`, an interface or a type alias?

## Question 5

Does assigning a value to an interface type validate unknown network data at runtime?

Then read the [quiz answers](../answers/quiz/quiz-answers.md).
