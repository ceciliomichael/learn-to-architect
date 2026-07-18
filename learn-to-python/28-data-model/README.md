# Module 28: Python's Data Model

## What you will learn

You will make custom objects cooperate with representation, equality, hashing, properties, containment, and operators.

## Special methods connect syntax to objects

Python syntax calls methods such as `__len__`, `__iter__`, `__eq__`, and `__add__`. Implement only operations that have a natural domain meaning.

## Developer and user representations

```python
class Money:
    def __init__(self, cents: int, currency: str) -> None:
        self.cents = cents
        self.currency = currency

    def __repr__(self) -> str:
        return f"Money(cents={self.cents!r}, currency={self.currency!r})"

    def __str__(self) -> str:
        return f"{self.currency} {self.cents / 100:.2f}"
```

`repr` should be unambiguous and useful for debugging. `str` is user-friendly. Never include secrets or sensitive personal data in either because logs and tracebacks may expose them.

## Equality and NotImplemented

```python
def __eq__(self, other: object) -> bool:
    if not isinstance(other, Money):
        return NotImplemented
    return (self.cents, self.currency) == (other.cents, other.currency)
```

Returning `NotImplemented` lets Python try reflected comparison or decide the result. It is not the same as raising `NotImplementedError`.

## Hashing requires stable equality

Equal objects must have equal hashes. Objects used as dictionary keys or set members must not change fields involved in equality while stored. Mutable value objects should normally remain unhashable. Frozen dataclasses are often easier for hashable values.

## Properties protect attribute syntax

```python
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
```

Properties keep simple attribute access while adding a stable invariant. Avoid hidden network, database, or expensive work in a property.

## Other natural protocols

```python
def __len__(self) -> int:
    return len(self._items)

def __contains__(self, item: object) -> bool:
    return item in self._items

def __call__(self, text: str) -> str:
    return text.strip()
```

Descriptors implement `__get__`, `__set__`, or `__delete__` and power methods and properties. They are useful for reusable attribute behavior but are advanced infrastructure. Prefer a property until reuse justifies a descriptor.

## Operator overloading needs domain meaning

Adding two Money values can be clear if currencies match. Adding a Money value to a user merely because Python permits `__add__` is confusing. Return `NotImplemented` for unsupported operand types and enforce invariants.

## Check your understanding

You are ready when you can state the equality-hash rule and implement only syntax with an unsurprising domain meaning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
