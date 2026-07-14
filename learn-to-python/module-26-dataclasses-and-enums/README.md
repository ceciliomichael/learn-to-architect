# Module 26: Dataclasses and Enums

## What you will learn

You will remove repetitive data-class code, create safe defaults, and model fixed named choices.

## Dataclasses generate common methods

```python
from dataclasses import dataclass

@dataclass
class Product:
    product_id: int
    name: str
    price_cents: int
```

The decorator generates an initializer, representation, and value-based equality by default. Type annotations still are not runtime validation.

Use `__post_init__` for invariant checks:

```python
def __post_init__(self) -> None:
    if self.price_cents < 0:
        raise ValueError("price must be nonnegative")
```

## Use default_factory for mutable values

```python
from dataclasses import field

@dataclass
class Cart:
    items: list[str] = field(default_factory=list)
```

The factory runs for each instance. A direct list default would be shared and dataclasses reject common mutable built-in defaults.

## Frozen and slots are deliberate options

```python
@dataclass(frozen=True, slots=True)
class Coordinate:
    latitude: float
    longitude: float
```

Frozen prevents ordinary field assignment but does not deeply freeze nested objects. Slots can reduce per-instance memory and prevent arbitrary new attributes, but affect inheritance, weak references, and some introspection. Choose from measured or design needs.

Do not use unsafe hashing for mutable value objects. Hash keys must remain stable while stored in dictionaries or sets.

## Enums give choices names

```python
from enum import Enum

class OrderStatus(Enum):
    OPEN = "open"
    PAID = "paid"
    CANCELLED = "cancelled"
```

```python
status = OrderStatus.PAID
print(status.value)
```

Compare enum members with identity or equality. Convert external text explicitly:

```python
try:
    status = OrderStatus(user_text)
except ValueError:
    print("Unsupported status")
```

Use `IntEnum` only when compatibility with ordinary integers is a real requirement; it can blur type boundaries.

## Dataclass or ordinary class

Use a dataclass when the public value fields are central. Use an ordinary class when initialization, hidden state, lifecycle, and behavior dominate.

## Check your understanding

You are ready when you can create independent list defaults, explain shallow frozen behavior, and convert external text to an enum safely.
