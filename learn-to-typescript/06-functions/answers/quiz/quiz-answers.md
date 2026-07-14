# Module 06 Quiz Answers

## Answer 1

A parameter is a local name in the function declaration. An argument is a particular value supplied when the function is called.

## Answer 2

```text
12
```

The call gives `6` to `value`, and the function returns `6 * 2`.

## Answer 3

`console.log` displays information. `return` ends the current function call and sends a value back to the caller. A caller can store or calculate with a returned value.

## Answer 4

No. `message` is local to `createMessage`. Code outside the function can use the returned value by calling the function and storing its result.

## Answer 5

```typescript
function add(a: number, b: number) {
  return a + b;
}

const total = add(2, 3);
```

The returned number becomes the value of `total`.
