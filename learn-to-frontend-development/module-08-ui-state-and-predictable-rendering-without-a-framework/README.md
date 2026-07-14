# Module 08: UI State and Predictable Rendering without a Framework

## What you will learn

Keep application state in one typed value and render the view from that state instead of scattering hidden DOM truth.

## Contracts to understand

- Transitions become inspectable and rendering can derive visible output from known data.
- A value computed from existing state, such as a filtered list, which usually should not be stored separately.
- It encourages deliberate replacement instead of hidden mutation.
- Focus and node-local state inside the replaced region, so the render boundary must be chosen carefully.
- The same state and environment should produce the same intended view.

## Complete TypeScript example

```ts
type State = {
  readonly items: readonly string[];
  readonly filter: string;
};

let state: State = { items: ["Water", "Weed"], filter: "" };

function render(next: State): void {
  const list = document.querySelector<HTMLUListElement>("#items");
  if (list === null) throw new Error("Expected #items");

  list.replaceChildren(...next.items
    .filter((item) => item.toLowerCase().includes(next.filter.toLowerCase()))
    .map((text) => {
      const li = document.createElement("li");
      li.textContent = text;
      return li;
    }));
}

render(state);
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 09](../module-09-browser-modules-package-imports-and-build-output/README.md).

