# Exercise Solution: Component Testing and Accessible Queries

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { expect, test, vi } from "vitest";
import { SaveButton } from "./SaveButton";
test("calls onSave", async () => {
  const onSave = vi.fn();
  const user = userEvent.setup();
  render(<SaveButton onSave={onSave} />);
  await user.click(screen.getByRole("button", { name: "Save" }));
  expect(onSave).toHaveBeenCalledOnce();
});
```

## Why this works

Component tests should query by accessible role, name, label, and visible behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.