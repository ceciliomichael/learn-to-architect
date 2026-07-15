# Exercise Solution: Propagation, Delegation, and Listener Cleanup

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

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

