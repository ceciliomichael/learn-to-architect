# Module 10: URLs, Search Parameters, History, and Navigation

## What you will learn

Use URL APIs instead of string concatenation and keep browser history truthful.

## Contracts to understand

- They encode and parse URL components according to URL rules.
- It adds a same-origin history entry without navigating by itself.
- popstate.
- Usually no; replaceState or delayed commits may better represent meaningful navigation.
- No. The new URL must remain same-origin.

## Complete TypeScript example

```ts
const url = new URL(window.location.href);
url.searchParams.set("topic", "compost");
url.searchParams.set("page", "2");

history.pushState({ topic: "compost" }, "", url);

window.addEventListener("popstate", () => {
  const current = new URL(window.location.href);
  console.log(current.searchParams.get("topic"));
});
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../module-11-fetch-http-results-headers-and-content-types/README.md).

