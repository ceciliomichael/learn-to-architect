# Module 27 Exercises

## Exercise 1: Convert a chain

Rewrite a two-step `then` chain with an async function and `await`. Keep the return type explicit as `Promise<string>`.

## Exercise 2: Safe request helper

Write `fetchJson(url: string): Promise<unknown>`. Check `response.ok`, include the status in an Error, and keep parsed JSON unknown.

## Exercise 3: Validate a response

Create a `WeatherReading` with string city and number temperature. Write a type guard and a fetch function that returns `Promise<WeatherReading>` only after validation.

## Exercise 4: Sequential or parallel

For each case, choose sequential or `Promise.all` and explain:

- load a user, then load orders using the user's id
- load unrelated weather and news panels
- save step 2 only after step 1 provides a generated id

## Exercise 5: Inspect all settlements

Create three Promises, one of which rejects. Use `Promise.allSettled` and print a clear line for every result.

## Completion checklist

- [ ] My async return types use `Promise<T>`.
- [ ] I handled rejection and HTTP status separately.
- [ ] I validated parsed response data.
- [ ] I used parallel work only for independent operations.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
