# Module 08 Quiz

## Question 1

What are the property names and value types in this object?

```typescript
const item = {
  name: "Pen",
  price: 12,
  inStock: true,
};
```

## Question 2

Does declaring an object variable with `const` make all its properties readonly?

## Question 3

Predict the output:

```typescript
const first = { count: 1 };
const second = first;
second.count = 5;
console.log(first.count);
```

## Question 4

How does `const copy = { ...original };` differ from `const copy = original;` for an object with only primitive properties?

## Question 5

Correct both mistakes:

```typescript
const user = { name = "Kai", age: 20 };
console.log(user.Name);
```

Then read the [quiz answers](../answers/quiz/quiz-answers.md).
