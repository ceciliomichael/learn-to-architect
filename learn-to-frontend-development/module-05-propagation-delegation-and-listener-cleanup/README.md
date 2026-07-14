# Module 05: Propagation, Delegation, and Listener Cleanup

## What you will learn

Use bubbling for dynamic collections while keeping ownership and cleanup explicit.

## Contracts to understand

- After reaching a target, many events propagate through ancestors.
- One ancestor listener handles events from matching descendants.
- closest can find an element outside the intended owned subtree in some nested contexts.
- Aborting the controller removes listeners registered with its signal.
- Only when the component contract truly owns and must stop that propagation, not as a default fix.

## Complete TypeScript example

```ts
const list = document.querySelector<HTMLUListElement>("#task-list");
if (list === null) throw new Error("Expected task list");

const controller = new AbortController();

list.addEventListener("click", (event) => {
  const target = event.target;
  if (!(target instanceof Element)) return;

  const button = target.closest<HTMLButtonElement>("button[data-task-id]");
  if (button === null || !list.contains(button)) return;

  console.log(button.dataset.taskId);
}, { signal: controller.signal });

// Call when the owning view is removed:
// controller.abort();
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../module-06-forms-formdata-and-submission/README.md).

