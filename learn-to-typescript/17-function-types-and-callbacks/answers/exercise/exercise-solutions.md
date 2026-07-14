# Module 17 Exercise Solutions

## Exercise 1

```typescript
type TextTransformer = (text: string) => string;

const toLowercase: TextTransformer = (text) => text.toLowerCase();
const toUppercase: TextTransformer = (text) => text.toUpperCase();

function transformText(text: string, transformer: TextTransformer): string {
  return transformer(text);
}

console.log(transformText("Hello", toLowercase));
console.log(transformText("Hello", toUppercase));
```

## Exercise 2

```typescript
type NumberTest = (value: number) => boolean;

function countNumbers(values: readonly number[], test: NumberTest): number {
  let count = 0;

  for (const value of values) {
    if (test(value)) {
      count = count + 1;
    }
  }

  return count;
}

const values = [4, 11, 12, 15];
console.log(countNumbers(values, (value) => value % 2 === 0));
console.log(countNumbers(values, (value) => value > 10));
```

## Exercise 3

```typescript
function greet(name: string, title?: string): string {
  if (title === undefined) {
    return `Hello, ${name}`;
  }

  return `Hello, ${title} ${name}`;
}

function multiply(value: number, factor = 2): number {
  return value * factor;
}
```

Inside `greet`, `title` may still be undefined. Inside `multiply`, an omitted or undefined factor has already been replaced by 2.

## Exercise 4

```typescript
run(announce);
```

`run` needs the function value. Calling `announce()` immediately supplies no message and produces `void`, which is not the required callback.

## Exercise 5

```typescript
const squareExpression = (value: number): number => value * value;

const squareBlock = (value: number): number => {
  return value * value;
};
```

The expression body returns automatically. The block body needs an explicit return.
