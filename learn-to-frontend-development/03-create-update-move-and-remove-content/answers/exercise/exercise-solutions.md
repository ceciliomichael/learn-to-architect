# Exercise Solution: Create, Update, Move, and Remove Content

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

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

