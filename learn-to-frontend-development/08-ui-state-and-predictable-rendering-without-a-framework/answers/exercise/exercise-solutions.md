# Exercise Solution: UI State and Predictable Rendering without a Framework

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

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

