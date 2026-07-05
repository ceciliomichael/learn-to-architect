# Challenge 03: Generic Interface with Default Type

Build a reusable API response wrapper using a generic interface with a default type parameter.

## Scenario

In modern full-stack web applications, networking layers constantly exchange standardized JSON response payloads with backend servers. A standard response typically contains a success flag, an error message nullable field, and a data payload. While the data payload could be a complex domain object (such as a User or Invoice), many simple endpoints return basic text confirmation messages.

To prevent developers from repetitively typing `<string>` for standard text endpoints while retaining the ability to swap in complex domain models for data endpoints, you will utilize **Default Generic Types** (`<T = DefaultType>`).

## Your Tasks

1. Define a generic interface `ApiResponse<T = string>` with the following structural shape:
   * `success`: A boolean indicating whether the network request succeeded.
   * `data`: A generic payload slot of type `T`.
   * `errorMessage`: A string or `null` representing any server error details.
2. Create three typed variables utilizing this interface:
   * `textResponse`: Use the default type parameter by omitting angle brackets (`ApiResponse`). Assign a valid response object where `data` is a text string.
   * `numberResponse`: Override the default by specifying `ApiResponse<number>`. Assign a valid response object where `data` is a numeric code or metric.
   * `userResponse`: Override the default by specifying a custom inline object type: `ApiResponse<{ id: number; username: string }>`. Assign a valid response object containing user profile data.
3. For `textResponse`, document in a comment what TypeScript infers as the type of `.data`.
4. For `userResponse`, access and log `.data.username` to demonstrate deep type safety.

## Architectural Requirements

* Do not use the `any` keyword or type assertions (`as`).
* Utilize the syntax `= string` to establish the default type parameter.
* Do not use em-dashes anywhere in your code or comments.

## ANSWER HERE

```typescript
// Write your ApiResponse interface and three response variables below:
```
