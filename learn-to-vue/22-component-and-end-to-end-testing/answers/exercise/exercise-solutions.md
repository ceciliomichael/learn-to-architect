# Exercise Solution: Component and End-to-End Testing

```ts
import { render, screen } from "@testing-library/vue";
import SaveButton from "./SaveButton.vue";
test("emits save", async () => {
  const view = render(SaveButton);
  await screen.getByRole("button", { name: "Save" }).click();
  expect(view.emitted().save).toHaveLength(1);
});
```

## Why this works

Component tests assert visible behavior through accessible queries, and end-to-end tests exercise critical browser flows against controlled data. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.