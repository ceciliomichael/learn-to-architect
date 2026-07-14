# Exercise Solutions: Protocols, Generics, and Typed Data

```python
from typing import Literal, NewType, NotRequired, Protocol, TypeVar, TypedDict

T = TypeVar("T")

def last(values: list[T]) -> T:
    if not values:
        raise ValueError("values must not be empty")
    return values[-1]

class Saver(Protocol):
    def save(self, text: str) -> None:
        pass

def store_message(destination: Saver, text: str) -> None:
    destination.save(text)

class ProductRow(TypedDict):
    product_id: int
    name: str
    price_cents: int
    description: NotRequired[str]

OrderId = NewType("OrderId", int)
OrderStatus = Literal["open", "paid", "cancelled"]
```

All constructs guide static analysis. Code must still verify decoded objects, required keys, types, ranges, and allowed values at runtime.
