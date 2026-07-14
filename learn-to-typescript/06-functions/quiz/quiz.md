# Module 06 Quiz

## Question 1

Explain the difference between a parameter and an argument.

## Question 2

What is the output?

```typescript
function double(value: number) {
  return value * 2;
}

const result = double(6);
console.log(result);
```

## Question 3

Why is `return` different from `console.log`?

## Question 4

Can the final line use `message`? Explain.

```typescript
function createMessage(name: string) {
  const message = `Hello, ${name}`;
  return message;
}

console.log(message);
```

## Question 5

Correct this function so the caller receives the sum:

```typescript
function add(a: number, b: number) {
  console.log(a + b);
}

const total = add(2, 3);
```

Then read the [quiz answers](../answers/quiz/quiz-answers.md).
