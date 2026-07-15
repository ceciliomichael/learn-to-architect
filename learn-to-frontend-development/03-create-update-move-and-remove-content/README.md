# Module 03: Create, Update, Move, and Remove Content

## What you will learn

Create DOM nodes through APIs, insert plain text safely, and update the smallest necessary region.

## Contracts to understand

- It inserts text without parsing it as markup.
- It moves from its old parent rather than being copied.
- Create a new node or deliberately clone one, then repair any ids and state.
- It preserves unrelated focus, selection, media, and browser state.
- Focus, listener ownership, references, and whether the user can recover the removed data.

## Complete TypeScript example

```ts
const list = document.querySelector<HTMLUListElement>("#tasks");
if (list === null) throw new Error("Expected #tasks");

const item = document.createElement("li");
const label = document.createElement("span");
label.textContent = "Water seedlings";

const remove = document.createElement("button");
remove.type = "button";
remove.textContent = "Remove";
remove.addEventListener("click", () => item.remove());

item.append(label, " ", remove);
list.append(item);
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../04-events-event-objects-and-default-behavior/README.md).

