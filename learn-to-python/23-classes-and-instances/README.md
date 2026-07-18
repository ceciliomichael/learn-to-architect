# Module 23: Classes and Instances

## What you will learn

You will create objects that keep valid state with related behavior and distinguish instance from class attributes.

## A class creates a new type

```python
class BankAccount:
    def __init__(self, owner: str, balance_cents: int = 0) -> None:
        if not owner.strip():
            raise ValueError("owner is required")
        if balance_cents < 0:
            raise ValueError("opening balance must be nonnegative")
        self.owner = owner.strip()
        self.balance_cents = balance_cents

    def deposit(self, amount_cents: int) -> None:
        if amount_cents <= 0:
            raise ValueError("deposit must be positive")
        self.balance_cents += amount_cents
```

Calling `BankAccount("Ava")` creates an instance and runs `__init__` to initialize it. `self` is the current instance passed automatically by a method call.

```python
account = BankAccount("Ava", 1000)
account.deposit(250)
```

## Protect invariants through methods

An invariant is a rule that should remain true for every valid object. If balance must not become negative, a withdrawal method checks before mutation.

Python does not enforce private fields by access modifiers. A leading underscore communicates nonpublic implementation:

```python
self._balance_cents = balance_cents
```

Callers can still access it. Encapsulation depends on documented APIs, review, and cooperation.

## Class and instance attributes differ

```python
class Account:
    currency = "PHP"

    def __init__(self, owner: str) -> None:
        self.owner = owner
```

`currency` is found on the class and shared through lookup. `owner` belongs to each instance.

Never use a mutable class attribute for per-instance data:

```python
class WrongCart:
    items = []
```

All instances share that list. Create `self.items = []` in `__init__`.

## Instance, class, and static methods

Instance methods use `self`. A `@classmethod` receives `cls` and often provides an alternate constructor. A `@staticmethod` receives neither automatically and is useful only when behavior belongs in the class namespace but needs no class or instance state.

```python
@classmethod
def from_pesos(cls, owner: str, pesos: int):
    return cls(owner, pesos * 100)
```

## Do not turn every dictionary into a class

Use a class when identity, invariants, lifecycle, or related behavior benefit from one boundary. Simple data may be clearer as a tuple, dictionary with TypedDict, or dataclass.

## Custom exceptions are classes

Create a custom exception after ordinary class behavior is clear and only when callers need to distinguish a domain failure:

```python
class InsufficientStockError(Exception):
    def __init__(self, requested: int, available: int) -> None:
        self.requested = requested
        self.available = available
        super().__init__(
            f"requested {requested}, available {available}"
        )
```

It inherits standard exception behavior and adds domain fields. Raise a built-in `ValueError` when callers do not need a separate category.

## Check your understanding

You are ready when you can locate each attribute, explain `self`, keep invalid state out through method checks, and recognize a custom exception as a specialized class.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
