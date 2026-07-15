# Exercise Solutions: Python's Data Model

```python
class Money:
    def __init__(self, cents: int, currency: str) -> None:
        self.cents = cents
        self.currency = currency

    def __repr__(self) -> str:
        return f"Money(cents={self.cents!r}, currency={self.currency!r})"

    def __str__(self) -> str:
        return f"{self.currency} {self.cents / 100:.2f}"

    def __eq__(self, other: object) -> bool:
        if not isinstance(other, Money):
            return NotImplemented
        return (self.cents, self.currency) == (other.cents, other.currency)

    def __add__(self, other: object):
        if not isinstance(other, Money):
            return NotImplemented
        if self.currency != other.currency:
            raise ValueError("currencies must match")
        return Money(self.cents + other.cents, self.currency)

class Temperature:
    def __init__(self, celsius: float) -> None:
        self.celsius = celsius

    @property
    def celsius(self) -> float:
        return self._celsius

    @celsius.setter
    def celsius(self, value: float) -> None:
        if value < -273.15:
            raise ValueError("below absolute zero")
        self._celsius = value

class Catalog:
    def __init__(self, names: list[str]) -> None:
        self._names = list(names)

    def __len__(self) -> int:
        return len(self._names)

    def __contains__(self, name: object) -> bool:
        return name in self._names

    def __iter__(self):
        return iter(self._names)

wallet = Money(500, "PHP") + Money(250, "PHP")
print(wallet)

try:
    Money(500, "PHP") + Money(100, "USD")
except ValueError as error:
    print(error)

temperature = Temperature(25.0)
try:
    temperature.celsius = -300.0
except ValueError as error:
    print(error)

catalog = Catalog(["Pen", "Book"])
print(len(catalog), "Book" in catalog, list(catalog))
```

The collection delegates length, membership, and iteration to its private list, so ordinary Python syntax remains predictable.

Money remains unhashable because equality is defined on mutable fields. If its cents or currency changed while it was a dictionary key, Python could search using a hash that no longer matches its stored location. A frozen value design would be a safer starting point if hashing were required.
