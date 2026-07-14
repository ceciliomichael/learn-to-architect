# Module 27 Quiz Answers

## Answer 1

`Promise<User>`.

## Answer 2

No. Fetch normally fulfills with a Response for HTTP error statuses. Check `response.ok` or status.

## Answer 3

The remote runtime data may not match the application's static shape. JSON parsing checks syntax, not domain properties.

## Answer 4

When the operations are independent, should start together, and the caller needs all results or one combined failure.

## Answer 5

It returns a fulfilled or rejected result for every input instead of rejecting the combined Promise at the first rejection.
