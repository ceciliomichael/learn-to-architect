# Exercise Solution: Lifting State and One-Way Data Flow

```tsx
import { useState } from "react";
type SearchProps = { value: string; onChange: (value: string) => void };
function Search({ value, onChange }: SearchProps) { return <input aria-label="Search" value={value} onChange={event => onChange(event.target.value)} />; }
function Results({ query }: { query: string }) { return <p>Showing results for {query || "everything"}.</p>; }
export function SearchPage() {
  const [query, setQuery] = useState("");
  return <><Search value={query} onChange={setQuery} /><Results query={query} /></>;
}
```

## Why this works

Move shared state to the closest common owner and pass data down with actions up. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.