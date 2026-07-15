# Exercise Solutions: Dataclasses and Enums

```python
from dataclasses import FrozenInstanceError, dataclass, field
from enum import Enum

@dataclass
class Product:
    product_id: int
    name: str
    price_cents: int

    def __post_init__(self) -> None:
        if not self.name.strip():
            raise ValueError("name is required")
        if self.price_cents < 0:
            raise ValueError("price must be nonnegative")

@dataclass
class Cart:
    items: list[str] = field(default_factory=list)

@dataclass(frozen=True, slots=True)
class Coordinate:
    latitude: float
    longitude: float

class OrderStatus(Enum):
    OPEN = "open"
    PAID = "paid"
    CANCELLED = "cancelled"

first = Cart()
second = Cart()
first.items.append("Book")
print(first.items, second.items)

for text in ("paid", "unknown"):
    try:
        print(OrderStatus(text))
    except ValueError:
        print(f"Unsupported status: {text}")

point = Coordinate(14.5995, 120.9842)
try:
    point.latitude = 0.0
except FrozenInstanceError:
    print("Frozen coordinates cannot be reassigned")
```

`default_factory` gives each cart a separate list. The frozen coordinate rejects normal field reassignment, while `slots=True` avoids a per-instance attribute dictionary and prevents adding undeclared fields.

Keep `Product` as a dataclass while it mainly carries validated values. If it gains a lifecycle, several coordinated state changes, or behavior that must preserve complex invariants, an ordinary class can make that API more deliberate.
