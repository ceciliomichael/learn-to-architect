# Exercise Solution: Unit and Component Testing

```tsx
import { render, screen } from "@testing-library/react";
import PageTitle from "./page-title";
test("shows the supplied title", () => {
  render(<PageTitle title="Projects" />);
  expect(screen.getByRole("heading", { name: "Projects" })).toBeVisible();
});
```

## Why this works

Unit tests cover isolated rules and component tests cover rendered behavior at the smallest useful boundary. Mock only the external boundary the test does not own. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.