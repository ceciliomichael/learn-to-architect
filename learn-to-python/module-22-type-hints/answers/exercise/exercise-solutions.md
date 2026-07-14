# Exercise Solutions: Add Type Hints

```python
from collections.abc import Callable, Iterable
from typing import TypeAlias

def area(width: float, height: float) -> float:
    return width * height

def find_label(key: str) -> str | None:
    return {"a": "Active"}.get(key)

def normalize(text: str) -> str:
    return text.strip().casefold()

def positives(values: Iterable[int]) -> list[int]:
    return [value for value in values if value > 0]

Validator: TypeAlias = Callable[[int], bool]

label = find_label("missing")
if label is not None:
    print(label.upper())
```

Calling `area("wide", 2)` is not blocked by annotations. A type checker should flag it, while runtime behavior depends on the actual operations. External inputs still need validation.
